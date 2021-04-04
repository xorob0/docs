# WireGuard

Wireguard is a performant vpn with client on almost all platforms.

# Compose

```
---
version: "3.3"
services:
  wireguard:
    image: ghcr.io/linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - SERVERURL=wireguard.gneee.tech
      - PEERS=laptop,phone
    volumes:
      - /configs/wireguard:/config
      - /lib/modules:/lib/modules
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```

Nothing to add here, this is basicaly pasted from [linuxserver.io](https://linuxserver.io).

Keep in mind that you have to add the port forwarding in you router.

NOTE: As this is udp on port 51820 this can be blocked by some the firewall on some company networks.

# Usage

To show the configs for your phone, use:

```
docker exec -it wireguard /app/show-peer phone
```

and scan the QR code

If you need to access the config file you can find it at `/configs/wireguard/peer_laptop/peer_laptop.conf` or you can upload it to [linx](services/linx) by typing:

```
curl -T /configs/wireguard/peer_laptop/peer_laptop.conf https://linx.gneee.tech/upload
```
