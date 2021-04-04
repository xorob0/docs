# Miniflux

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

```
docker-compose exec miniflux /usr/bin/miniflux -migrate
```

```
docker-compose exec miniflux /usr/bin/miniflux -create-admin
```
