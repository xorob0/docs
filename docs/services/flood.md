# Flood

[Flood](https://flood.js.org/) is an alternative frontend for torrent clients (in this case [QbitTorrent](/services/qbittorrent/))

## Compose

```
version: "3.3"
services:
  flood:
    container_name: flood
    image: jesec/flood
    restart: unless-stopped
    environment:
      HOME: /config
    volumes:
      - /configs/flood:/config
      - /configs/flood/data:/data
      - /HDD1/Media:/media:ro
```
