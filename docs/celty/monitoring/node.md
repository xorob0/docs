# Node Exporter

TODO

```
version: '3.3'
services:
  nodeexporter:
    container_name: nodeexporter
    image: prom/node-exporter
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /var/run:/var/run:rw
      - /var/lib/docker/:/var/lib/docker:ro
      - /:/rootfs:ro,rslave
      - /HDD1/:/media/data:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.ignored-mount-points=^/(sys|proc|dev|host|etc)($$|/)'
      - '--collector.textfile.directory=/var/lib/node_exporter/textfile_collector/'
    restart: always

networks:
  default:
    external:
      name: external
```