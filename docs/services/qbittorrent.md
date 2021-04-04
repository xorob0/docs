# QbitTorrent
## Compose
```
version: "3.3"
services:
  qbittorrent:
    image: ghcr.io/linuxserver/qbittorrent
    container_name: qbittorrent
    volumes:
      - /configs/qbitorrent:/config
      - /HDD1/Media/:/media
    ports:
      - 6881:6881
      - 6881:6881/udp
    restart: unless-stopped
```