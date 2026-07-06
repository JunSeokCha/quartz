
Because I am not a company, I don't have a signed software certificate. So running the installers for the programs I wrote will trigger a warning on your computer. Especially, on MacOS, you might have to go through a complex process of configuring the settings to allow my program to run.

If you don't trust my programs or do not know how to configure the settings to execute my program, you can sandbox it by downloading the installers inside a docker container. You can run the installer there.

Run the following to make an ubuntu container:
```
docker run -it ubuntu /bin/bash
```

Within the ubuntu container, access this site through the internet and download the program.

If you want even more security, run a virtual machine and download the program there.