
# How to install WireGuard Easy with bash script on ubuntu server
#### WireGuard VPN + Web-based Admin UI.
---

> [!IMPORTANT]
> _Prerequisites: Docker and Docker Compose installed._

&nbsp;

### First step: Create a bash script file in Ubuntu.
```
sudo nano install-wgeasy.sh
```

### Second step: Copy and Paste the following bash script:
```
#!/bin/bash

read -p "Press Enter to continue or Ctrl + C to Cancel."
mkdir -p docker/wg-easy
wait
cd docker/wg-easy
wait
# Create a new .yml file
cat <<EOF > docker-compose.yml
version: '3'
services:
  wg-easy:
    container_name: wg-easy
    environment:
      - LANG=en
      - WG_HOST=YourVpsIp
      - PASSWORD=SuperSecurePassword
    volumes:
      - ./wg-easy:/etc/wireguard
    ports:
      - 51820:51820/udp
      - 51821:51821/tcp
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
      - net.ipv4.ip_forward=1
    restart: unless-stopped
    image: ghcr.io/wg-easy/wg-easy
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
sudo bash install-wgeasy.sh
```

### Last step: Check if wg easy is running
```
sudo docker ps | grep wg-easy
```

&nbsp;

If all went right you should see something like this:
```
 1 minutes ago   Up 1 minutes   0.0.0.0:51820->51820/udp, :::51820->51820/udp
```

&nbsp;

- [x] Success, wg easy is ready and running!

&nbsp;

You can now visit the wg easy web ui to finish setting up wireguard.

http://yourip:51821
