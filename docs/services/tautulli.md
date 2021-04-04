# Tautulli

[Tautulli](https://tautulli.com/) is a tool monitor you [Plex](/services/plex) server, it can give you stats, a dashboard and notifications.

## Compose

```
version: '3.3'
services:
  tautulli:
    container_name: tautulli
    image: tautulli/tautulli
    restart: unless-stopped
    volumes:
      - /configs/tautulli:/config
      - /configs/plex/Library/Application Support/Plex Media Server/Logs/:/plex_logs:ro
```

## Tips

### Downtime notification

Tautulli can monitor you Plex Media Server state and alert you if it goes down, on playback error and more. It's a good idea to enable this if you share your server.
