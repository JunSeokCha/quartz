Because of security concerns, I sandboxed Hermes Agent in a docker container.

Docker containers are virtual OSes, kind of similar to virtual machines, but different. Virtual machines virtualize the hardware, which is further below the OS. So, dockers containers are shallower than a virtual machine.

I focus in this post on using docker to sandbox a Hermes-Agent.

1. to check running containers
in your host's terminal,
```
docker ps -a
```

2. to make a container
```
docker run --name hermes_01 -it -v C:\Users\user/.hermes:/opt/data nousresearch/hermes-agent
```

3. to restart a container
```
docker start -i hermes_01
```

4. to copy a file or folder to a running container
file:
```
docker cp /path/to/local/file.txt container_name:/path/inside/container/
```
folder:
```
docker cp /path/to/local/folder container_name:/path/inside/container/
```

5. to stop the container
In the hermes chat,
```
\exit
```

