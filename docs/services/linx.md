# Linx

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

#TODO: config file
