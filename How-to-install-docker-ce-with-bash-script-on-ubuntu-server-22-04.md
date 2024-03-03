# How to install docker ce with bash script on ubuntu server 22.04

### First step: Create a bash script file in Ubuntu.
```
sudo nano install.sh
```

### Second step: Copy and Paste the following bash script:

```
#!/bin/bash

read -p "Press enter to continue or Control + C to cancel."
sudo apt update
wait
sudo apt upgrade -y
wait
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
wait
sudo sudo apt-get install ca-certificates curl
wait
sudo install -m 0755 -d /etc/apt/keyrings
wait
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
wait
sudo chmod a+r /etc/apt/keyrings/docker.asc
wait
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
wait
sudo apt-get update
wait
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
wait
echo "Done."
```

Press Ctrl + S to save and then Ctrl + X to close.

&nbsp;

> [!NOTE]
> The script will:
> - Update the package list from the repositories.
> - Upgrade installed packages to their latest versions.
> - Remove old versions of docker.
> - Install additional dependencies.
> - Install docker components.

&nbsp;

### Third step: Run the bash script
```
sudo bash install.sh
```

### Last step: Check if Docker is running.
```
sudo docker ps
```

&nbsp;

If all went right you should see something like this:
```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

&nbsp;

- [x] Success, docker is ready and running!

&nbsp;

---
&nbsp;

### Useful commands:
| Description  | Command |
| ------------- | ------------- |
| List containers running | `docker ps` |
| List all containers | `docker ps -a` |
| Start a container | `docker start ID` or `docker start container-name` |
| Pause a container | `docker pause ID` or `docker pause container-name` |
| Unpause a container | `docker unpause ID` or `docker unpause container-name` |
| Restart a container | `docker restart ID` or `docker restart container-name` |
| Stop a container | `docker stop ID` or `docker stop container-name` |
| Remove a stopped container | `docker rm ID` or `docker rm container-name` |
| Rename a container | `docker rename container-name new-name` |
| View container resources usage | `docker stats ID` or `docker stats container-name`|
| Inspect a container | `docker inspect ID` or `docker inspect container-name`|
| Run a command inside a running container | `docker exec -it ID bash` or `docker exec -it container-name bash`|
| Create a docker network | `docker network create network-name` |
