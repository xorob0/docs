# Syncthing

## Compose

```
version: "3.3"
services:
  syncthing:
    image: ghcr.io/linuxserver/syncthing
    container_name: syncthing
    hostname: celty
    volumes:
      - /configs/syncthing:/config
      - /HDD1/Docs:/docs
      - /HDD1/Documents/nextcloud/tim/files:/tim
    ports:
      - 8384:8384
      - 22000:22000
      - 21027:21027/udp
    restart: unless-stopped
```
