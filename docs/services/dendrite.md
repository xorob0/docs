# Dendrite

[Dendrite](https://github.com/matrix-org/dendrite) is the new reference server for the matrix protocol. In a nutshell it's my personal [Element](https://element.io) server that can communicate with other [Element](https://element.io) servers.

It is still in beta and is not recommended for daily use but I'm a thug.

## Compose

```
version: "3.4"
services:
  monolith:
    hostname: monolith
    image: matrixdotorg/dendrite-monolith:latest
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
    environment:
      POSTGRES_PASSWORD: password
      POSTGRES_USER: dendrite

  # Zookeeper is only needed for polylith mode!
  zookeeper:
    hostname: zookeeper
    image: zookeeper

  # Kafka is only needed for polylith mode!
  kafka:
    container_name: dendrite_kafka
    hostname: kafka
    image: wurstmeister/kafka
    environment:
      KAFKA_ADVERTISED_HOST_NAME: "kafka"
      KAFKA_DELETE_TOPIC_ENABLE: "true"
      KAFKA_ZOOKEEPER_CONNECT: "zookeeper:2181"
    depends_on:
      - zookeeper
```

I can probably remove zookeeper and kafka but I did not look into it at the moment.

## Config

Apart from the database password there is not a lot of things to change. After creating your account(s) I still recommend disabling registration. You could enable the shared secret if you still want users you know to register later.

```
client_api:
  registration_disabled: true
  registration_shared_secret: "yolo"
```
