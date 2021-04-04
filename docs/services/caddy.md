# Caddy
[Caddy](https://caddyserver.com/) is my reverse proxy of choice. It manages Let's Encrypt on it's own and only needs a config file.

## Compose 
```
version: '3.3'
services:
  caddy:
    image: caddy
    container_name: caddy
    restart: unless-stopped
    volumes:
      - /configs/caddy/data/:/data
      - /configs/caddy/Caddyfile:/etc/caddy/Caddyfile
    ports:
      - 443:443
      - 80:80
      - 8448:8448
```