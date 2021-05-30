# Calibre
TODO
```
version: '3.3'
services:
  calibre:
    image: ghcr.io/linuxserver/calibre
    container_name: calibre
    environment:
      - PASSWORD=password
    volumes:
      - /configs/calibre:/config
      - /HDD1/Media/Books:/books
    restart: unless-stopped
  calibre-web:
    image: ghcr.io/linuxserver/calibre-web
    container_name: calibre-web
    environment:
      - DOCKER_MODS=linuxserver/calibre-web:calibre
    volumes:
      - /configs/calibre/web:/config
      - /configs/calibre:/calibre
      - /HDD1/Media/Books:/books
    ports:
      - 8083:8083
    restart: unless-stopped
networks:
  default:
    external:
      name: external
```