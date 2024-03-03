# How to install plex media server with bash script on ubuntu server 22.04
##### 
> [!IMPORTANT]
> _Prerequisites: Docker and Docker Compose installed._ 
 
&nbsp;

### First step: Create a bash script file in Ubuntu.
```
sudo nano install-plex.sh
```

### Second step: Copy and Paste the following bash script:
```
#!/bin/bash

read -p "Press Enter to continue or Ctrl + C to Cancel."
mkdir -p docker/plex
wait
cd docker/plex
wait
# Create a new .yml file
cat <<EOF > docker-compose.yml
services:
  plex:
    image: lscr.io/linuxserver/plex:latest
    container_name: plex
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - VERSION=docker
      - PLEX_CLAIM= #optional
    volumes:
      - ./path/library:/config
      - ./path/tvseries:/tv
      - ./path/movies:/movies
    restart: unless-stopped
EOF
wait
sudo docker compose up -d
wait
echo "Done."
```

Press Ctrl + S to save and then Ctrl + X to close.

&nbsp;

### Third step: Run the bash script
```
sudo bash install-plex.sh
```

### Last step: Check if plex is running
```
sudo docker ps | grep plex
```

&nbsp;


If all went right you should see something like this:
```
 lscr.io/linuxserver/plex:latest   "/init"   1 minutes ago   1 minutes ago plex
```

&nbsp;

- [x] Success, plex is ready and running!

&nbsp;

You can now visit the plex web ui to finish setting up your media server.

http://yourip:32400/web
