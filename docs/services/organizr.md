# Organizr

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
