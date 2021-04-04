# Miniflux

[Miniflux](https://miniflux.app/) is simply the best rss reader that can be selfhosted. I use it in combinasion with [Reeder](https://www.reederapp.com/) on my Mac and my iPhone and it's just perfect !

## Compose

```
version: '3.3'
services:
  miniflux:
    image: miniflux/miniflux:latest
    container_name: miniflux
    depends_on:
      web_miniflux-db:
        condition: service_healthy
    environment:
      - DATABASE_URL=postgres://miniflux:password@miniflux-db/miniflux?sslmode=disable
  miniflux-db:
    image: postgres:latest
    container_name: miniflux-db
    environment:
      - POSTGRES_USER=miniflux
      - POSTGRES_PASSWORD=password
    volumes:
      - web_miniflux-db:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD", "pg_isready", "-U", "miniflux"]
      interval: 10s
      start_period: 30s
volumes:
  miniflux-db:
```

I don't usualy setup healthchecks but since it was in the official documentation I let it there

## Setup

### Database init/migration

This command needs to be ran before the service can start. It will initialize the database if it never was and migrate it if the datase was created on an older/newer version.

```
docker-compose exec miniflux /usr/bin/miniflux -migrate
```

### Create admin

No account exist by default so we need to create one.

```
docker-compose exec miniflux /usr/bin/miniflux -create-admin
```

## Config
### Fever API
If you want to enable the Fever API (for exemple to comunicate with Reeder), login on the web UI and go to Settings > Integrations