# Cadvisor
TODO
```
version: '3.3'
services:
  cadvisor:
    image: gcr.io/google-containers/cadvisor
    container_name: cadvisor
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:rw
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
    restart: always
    command: ["--docker_only=true"]

networks:
  default:
    external:
      name: external
```