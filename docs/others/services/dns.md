# DynDNS

TODO

```
version: "3.3"
services:
  ddns:
    image: oznu/cloudflare-ddns
    container_name: ddns
    environment:
      - API_KEY=key
      - ZONE=gneee.tech
      - SUBDOMAIN=celty
    restart: unless-stopped
```
