# Linx

[Linx](https://github.com/andreimarcu/linx-server) is a file host with an api that's compatible with `wget`

## Compose

```
version: '3.3'
services:
  linx-server:
    container_name: linx-server
    image: andreimarcu/linx-server
    command: -config /data/linx-server.conf
    volumes:
      - /HDD1/:/HDD1/Public
      - /configs/linx/meta:/data/meta
      - /configs/linx/linx-server.conf:/data/linx-server.conf
    restart: unless-stopped
```

## Config
```
siteurl = https://linx.gneee.tech/
sitename = Linx
maxsize = 4294967296
maxexpiry = 2592000
```