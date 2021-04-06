# Dendrite

[Dendrite](https://github.com/matrix-org/dendrite) is the new reference server for the matrix protocol. In a nutshell it's my personal [Element](https://element.io) server that can communicate with other [Element](https://element.io) servers.

It is still in beta and is not recommended for daily use but I'm a thug.

## Compose

```
version: "3.3"
services:
  monolith:
    hostname: monolith
    image: matrixdotorg/dendrite-monolith:latest
        restart: unless-stopped
    command: [
      "--tls-cert=server.crt",
      "--tls-key=server.key"
    ]
    ports:
      - 8008:8008
    volumes:
      - /configs/dendrite:/etc/dendrite
      - /configs/dendrite/media:/var/dendrite/media
  postgres:
    hostname: postgres
    image: postgres:11
    restart: always
    volumes:
      - /configs/dendrite/postgres/create_db.sh:/docker-entrypoint-initdb.d/20-create_db.sh
      - /configs/dendrite/postgres/data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: password
      POSTGRES_USER: dendrite
```

## Initial Setup
Before starting any container, you need to generate some keys with
```
go get github.com/matrix-org/dendrite/cmd/generate-keys
go run github.com/matrix-org/dendrite/cmd/generate-keys \
  --private-key=matrix_key.pem \
  --tls-cert=server.crt \
  --tls-key=server.key
```
## Config

Apart from the database password there is not a lot of things to change. 

Enable nafka for monolith:

```
  kafka:
    use_naffka: false
```

After creating your account(s) I still recommend disabling registration. You could enable the shared secret if you still want users you know to register later.

```
  client_api:
    registration_disabled: true
    registration_shared_secret: "yolo"
```
