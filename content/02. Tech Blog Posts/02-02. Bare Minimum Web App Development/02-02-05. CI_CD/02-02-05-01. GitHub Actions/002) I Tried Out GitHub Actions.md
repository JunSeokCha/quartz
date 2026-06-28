
Date: 2026.06.24

I set GitHub Actions so Pushing to my repository would lead to pushing to my AWS lightsail instance. The process required some troubleshooting. 

First, I built my Quartz site locally. The static files in the "public" folder are the static files to be published.

```
npx quartz build
```

Second, I created a AWS lightsail instance with Amazon Linux 2023. I downloaded the default SSH key pair (.pem file) from my account. I opened Port 22 (SSH), Port 80 (HTTP), and Port 443 (HTTPS) in the networking tab.

Third, I went to the Github repository and went to "Settings -> Secrets and variables -> Actions". I added the repository secret "LIGHTSAIL_SSH_KEY" and pasted the contents of the .pem file. I added the repository secret "LIGHTSAIL_HOST" with my instance's public IP. I added the repository secret "LIGHTSAIL_USER" as 'ec2-user' (Because I selected Amazon Linux 2023). I created a file (".github/workflows/deploy.yml") inside the repository with the following:

```
name: Deploy Quartz to Lightsail

on:
  push:
    branches: main

jobs:
  deploy:
    runs-on: ubuntu-latest # Keep this as ubuntu-latest for the GitHub builder
    steps:
      - uses: actions/checkout@v6

      - name: Setup Node.js
        uses: actions/setup-node@v6
        with:
          node-version: '22'

      - name: Install dependencies and Build
        run: |
          npm ci
          npx quartz plugin install
          npx quartz build

      - name: Deploy to AWS Lightsail
        uses: easingthemes/ssh-deploy@main
        env:
          SSH_PRIVATE_KEY: ${{ secrets.LIGHTSAIL_SSH_KEY }}
          ARGS: -rltgoDzvO --delete
          SOURCE: public/
          REMOTE_HOST: ${{ secrets.LIGHTSAIL_HOST }}
          REMOTE_USER: ${{ secrets.LIGHTSAIL_USER }} # This will use 'ec2-user' from your secrets
          TARGET: /usr/share/nginx/html/ # Default web root folder for AL2023 Nginx

```

Fourth, I went to my AWS Lightsail Console and connected using SSH. To see the owner and permission settings of the web folder, I did the following:

```
ls -ld /usr/share/nginx/html/
```

It said root root, so it was locked. So, I did the following:

```
sudo chown -R ec2-user:ec2-user /usr/share/nginx/html/
```

I verified if it worked

```
ls -ld /usr/share/nginx/html/
```

Now it says ec2-user ec2-user.

Fifth, I modified the baseUrl setting in my quartz config file.

```
baseUrl: (my IP provided in Lightsail)
```

Sixth, I pushed my code to GitHub

```
git pull origin main
git commit -m "deployment"
git push origin main
```

However, the push from GitHub to Lightsail did not work. The problem was that Amazon Linux 2023's OpenSSH engine blocks older SHA-1 RSA keys by default. So, we need the modern ED25519 keys.

```
ssh-keygen -t ed25519 -f ~/.ssh/lightsail_github_key -N ""
cat ~/.ssh/lightsail_github_key.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

I copied the private key
```
cat ~/.ssh/lightsail_github_key
```

Then I updated the GitHub repository secrets "LIGHTSAIL_SSH_KEY".

Then I triggered the action again
```
git commit --allow-empty -m "Deploy using new EDD25519 key"
git push origin main
```

