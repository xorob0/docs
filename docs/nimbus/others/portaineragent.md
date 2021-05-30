# Portainer Agent

TODO to fix

```
version: '3.3'
services:
  portainer:
    image: portainer/agent
    container_name: portainer_agent
    restart: always
    volumes:
      - /var/lib/docker/volumes:/var/lib/docker/volumes
      - /var/run/docker.sock:/var/run/docker.sock
      - /:/host
      - /configs/portainer-agent:/data
    environment:
      - EDGE=1
      - EDGE_ID=fb885ca7-24cb-4c95-9db5-2aab2d101d52
      - EDGE_KEY=aHR0cHM6Ly9wb3J0YWluZXIuZ25lZWUudGVjaHxwb3J0YWluZXIuZ25lZWUudGVjaDo4MDAwfDNmOjU2OmNmOjg4OjAxOjI0OmVkOmY1OmYwOmZlOjJjOjliOjU5OjJiOmUzOmQ1fDU
      - CAP_HOST_MANAGEMENT=1
```
