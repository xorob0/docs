# Torrents

TODO

## QbitTorrent

[QbitTorrent](https://www.qbittorrent.org/download.php) is a simple torrent client that has an "OK" web UI.

### Compose

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

## Flood

[Flood](https://flood.js.org/) is an alternative frontend for torrent clients (in this case [QbitTorrent](/services/qbittorrent/))

### Compose

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
