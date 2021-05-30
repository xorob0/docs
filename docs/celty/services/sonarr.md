# Sonarr

[Sonarr](https://wiki.servarr.com/Sonarr) is a TV Shows manager that can grab episodes using torrents.

## Compose

```
  sonarr:
    image: ghcr.io/linuxserver/sonarr
    container_name: sonarr
    restart: unless-stopped
    volumes:
      - /configs/sonarr:/config
      - /HDD1/Media:/media
```

I'm using [linuxserver.io's image](https://docs.linuxserver.io/images/docker-sonarr)

## Tips
### Settings
#### Profiles

I like to create a `Best` profile that will only take movies in quality >= 720p and keep upgrading until it's a 4k remux

1080p Remuxes are better than 2160p Web-DL (especially with the Shield's AI upscaling) so don't forget to change the order.

#### Indexers

Don't bother with Sonarr's built in indexers support, use jackett for everything. It has better search and rss support and get updated more often.

#### Connect

It might look dumb to enable connect at first since Plex automatically scan new files. But if you've got a upgrade Plex will only scan your episodes if the name changes, it's always better to have it enabled.

#### General

Don't forget to enable security and disable analytics.