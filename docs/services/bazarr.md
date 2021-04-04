# Bazarr

## Compose

```
version: "3.3"
services:
  bazarr:
    image: ghcr.io/linuxserver/bazarr
    container_name: bazarr
    volumes:
      - /configs/bazarr:/config
      - /HDD1/Media:/media
    restart: unless-stopped
```
