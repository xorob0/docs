# Organizr

[Organizr](https://organizr.app/) can agregate all my selfhosted web ui into one and generate a cool dashboard with widget from some of them.

## Compose

```
version: "3.3"
services:
  organizr:
    image: organizr/organizr
    container_name: organizr
    volumes:
      - /configs/organizr:/config
    restart: unless-stopped
```
