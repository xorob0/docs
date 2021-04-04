# LibrePhotos
[LibrePhotos](https://github.com/LibrePhotos/librephotos) is a really powerful web gallery application. I use it alongside [NextCloud](services/nextcloud) as a google photo alternative. The upload and management of the pictures is handled by [NextCloud](services/nextcloud), while LibrePhoto takes care of organizing it, matching faces and creating albums using A.I.
# Compose
```
version: '3.3'
services:
  proxy:
    image: reallibrephotos/librephotos-proxy:dev
    restart: always
    volumes:
      - /HDD1/Documents/nextcloud/tim/files/Photos/:/data
      - /configs/librephotos/proxy/protected_media:/protected_media
    depends_on:
      - backend
      - frontend

  db:
    image: postgres
    restart: always
    environment:
      - POSTGRES_USER=docker
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=librephotos
    volumes:
      - /configs/librephotos/db:/var/lib/postgresql/data
    command: postgres -c fsync=off -c synchronous_commit=off -c full_page_writes=off -c random_page_cost=1.0

  frontend:
    image: reallibrephotos/librephotos-frontend:dev
    restart: always
    depends_on:
      - backend

  backend:
    image: reallibrephotos/librephotos:dev
    restart: always
    volumes:
      - /HDD1/Documents/nextcloud/tim/files/Photos/:/data
      - /configs/librephotos/proxy/protected_media:/protected_media
      - /configs/librephotos/logs:/logs
      - /configs/librephotos/cache:/root/.cache

    environment:
      - SECRET_KEY=secret
      - BACKEND_HOST=backend
      - ADMIN_EMAIL=admin@example.com
      - ADMIN_USERNAME=admin
      - ADMIN_PASSWORD=admin
      - DB_BACKEND=postgresql
      - DB_NAME=librephotos
      - DB_USER=docker
      - DB_PASS=password
      - DB_HOST=db
      - DB_PORT=5432
      - REDIS_HOST=redis
      - REDIS_PORT=6379
      - MAPBOX_API_KEY=${KEY}
      - WEB_CONCURRENCY=4
      - TIME_ZONE=Europe/Brussels
      - SKIP_PATTERNS=
      - DEBUG=0

    # Wait for Postgres
    depends_on:
      - db

  redis:
    image: redis
    restart: always
```
This one is a bit more tricky as it require a backend, a frontend, a database and a proxy.

Of course if you're going to copy-paste this compose you should change the user names, the password and the keys.