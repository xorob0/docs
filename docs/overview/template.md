# Template

This is the template I base most of my docker compose on. It is valid for most of my sevices explaine below.

## Docker Compose Template

```
version: '3.3'
services:
  NAME:
    image: IMAGE
    container_name: NAME
    restart: unless-stopped
    volumes:
      - /configs/NAME:/config
      - /HDD1/foo:/foo
      - /HDD1/bar:/bar

networks:
  default:
    external:
      name: external
```

Let's go block by block:

## Version

```
version: '3.3'
```

I'm using 3.3 as it's widely supported and I might sometimes need some v3 features

## Name

```
  NAME:
    image: IMAGE
    container_name: NAME
```

Those lines shouldn't be surprinsing to anyone, I just prefer using the same name for the container and the `container_name`. I don't usually have multiple instances of the same container so that's not a problem. The only exception is for databases where I often removes the `container_name` line so I know what service the database is related to.

Whenever possible I use [linuxserver.io](https://linuxserver.io)'s images, they follow the same kind of standars as I do so it makes everything really easy. And being a community project, I also find them very thrustworthy.

## Restart

```
    restart: unless-stopped
```

This line is just magic, it makes the container behave exactly as I want it to. I use `always` only for a few very important containers that should never be down.

## Volumes

```
    volumes:
      - /configs/NAME:/config
      - /HDD1/foo:/foo
      - /HDD1/bar:/bar
```

All my configs are in `/configs`, for the moment it is still in my root partition but I plan to make it a ZFS dataset someday for easy backup and snapshots.
For my data I often follow this simple convention.

## Ports

I try to avoid using `ports` and do most of the routing internally with dockers's hostnames (as shown in [caddy](/services/caddy))

## Network
```
networks:
  default:
    external:
      name: external
```
This part is only needed if the service need to be accessed from caddy. It makes sur that this network and Caddy are in the same network and can access each others

```
networks:
  external:
    name: external
  internal:
    internal: true
  vlan200:
    driver: macvlan
    driver_opts:
      parent: bond0.200
    ipam:
      config:
        - subnet: "192.168.200.0/24"
          ip_range: "192.168.200.64/26"
          gateway: "192.168.200.1"
```
Sometimes I need specific network for some services, for exemple when I need to connect a database and a service I prefer to add them both to an `internal` network with only the two of them.

Also some services need to access internet through a specific vlan and this can be done with the `vlan200` settings.