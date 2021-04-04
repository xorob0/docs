# Bazarr

[Bazarr](https://www.bazarr.media/) is a companion service to [Sonarr](/../sonarr) and [Radarr](/../radarr) that autmatically fetches subtitles from various sources

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
