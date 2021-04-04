# Jackett

[Jackett](https://github.com/Jackett/Jackett) is a proxy that translate *arr's request into tracker-specific queries. I use it to connect some trackers to my *arr's.

## Compose
```
version: '3.3'
services:
  jackett:
    image: ghcr.io/linuxserver/jackett
    container_name: jackett
    restart: unless-stopped
    volumes:
      - /configs/jackett:/config
```
I'm using [linuxserver.io's image](https://docs.linuxserver.io/images/docker-jackett)

## Tips

### Password
Don't forget to set a password if you're instance is available outside your LAN

### Don't add too much public trackers
When I started all this I used to add as much public trackers as I could. Not only this is a pain in the ass to add to my *arrs, but it also become really slow because it tries to query every websites before adding a movie. Just add the one you really use.