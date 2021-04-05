# Caddy

[Caddy](https://caddyserver.com/) is my reverse proxy of choice. It manages Let's Encrypt on it's own and only needs a config file.

## Compose

```
version: '3.3'
services:
  caddy:
    image: caddy
    container_name: caddy
    restart: unless-stopped
    volumes:
      - /configs/caddy/data/:/data
      - /configs/caddy/Caddyfile:/etc/caddy/Caddyfile
    ports:
      - 443:443
      - 80:80
      - 8448:8448
```

I just need to expose every port I want to use in in the `ports` section.

## Config

```
{
  http_port 80
  https_port 443
  email letsencrypt@toum.me
}

(nobots) {
  @bot {
    header_regexp User-Agent Googlebot|aolbuild|baidu|bingbod|bingpreview|msnbot|duckduckbot|googlebot|adbot-google|mediapartners-google|teoma|slurp|yandex
  }
  respond @bot 403 {
    body "Not dank enough"
    close
  }
  respond /robots.txt 200 {
    body "User-agent: *
    Disallow: /"
  }
}

(private) {
  @external {
     not remote_ip 192.168.0.0/16 172.16.0.0/12 10.0.0.0/8 81.243.19.142
  }
  respond @external 403 {
    body "Only available on local network"
  }
}

metrics.gneee.tech {
  metrics /metrics
  import nobots
  import private
}
torrents.gneee.tech {
  reverse_proxy {
    to flood:3000
  }
  import nobots
  import private
}
ugly.torrents.gneee.tech {
  reverse_proxy {
    to qbittorrent:8080
  }
  import nobots
  import private
}
s3.gneee.tech {
  reverse_proxy {
    to minio:9000
  }
  import nobots
}
syncthing.gneee.tech {
  reverse_proxy {
    to 192.168.188.101:8384
  }
  import nobots
  import private
}
radarr.gneee.tech {
  reverse_proxy {
    to radarr:7878
  }
  import nobots
}
sonarr.gneee.tech {
  reverse_proxy {
    to sonarr:8989
  }
  import nobots
}
jackett.gneee.tech {
  reverse_proxy {
    to jackett:9117
  }
  import nobots
  import private
}
dns.gneee.tech {
  reverse_proxy {
    to adguard:444
  }
  import nobots
}
admin.dns.gneee.tech {
  reverse_proxy {
    to adguard:3000
  }
  import nobots
  import private
}
matrix.gneee.tech {
  reverse_proxy {
    to 192.168.188.101:8008
  }
  import nobots
}
gneee.tech:8448 {
  reverse_proxy {
    to 192.168.188.101:8008
  }
  import nobots
}
portainer.gneee.tech {
  reverse_proxy {
    to 192.168.188.101:9000
  }
  import nobots
  import private
}
proxmox.gneee.tech {
  reverse_proxy {
    to 192.168.188.101:8006
  }
  import nobots
  import private
}
fritz.gneee.tech {
  reverse_proxy {
    to 192.168.188.1
  }
  import nobots
  import private
}
stats.gneee.tech {
  reverse_proxy {
    to 192.168.188.101:3000
  }
  import nobots
}
print.gneee.tech {
  reverse_proxy {
    to 192.168.188.40:80
  }
  import nobots
  import private
}
ombi.gneee.tech {
  reverse_proxy {
    to ombi:3579
  }
  import nobots
}
code.gneee.tech {
  reverse_proxy {
    to vscode:8080
  }
  import nobots
  import private
}
assistant.gneee.tech {
  reverse_proxy {
    to 192.168.188.32:8000
  }
  import nobots
}
linx.gneee.tech {
  reverse_proxy {
    to linx-server:8080
  }
  import nobots
}
cloud.gneee.tech {
  reverse_proxy {
    to nextcloud:80
  }
  import nobots
}
photos.gneee.tech {
  reverse_proxy {
    to http://192.168.188.101:1231
  }
  import nobots
}
plex.gneee.tech {
  reverse_proxy {
    to plex:32400
  }
  import nobots
}
rss.gneee.tech {
  reverse_proxy {
    to miniflux:8080
  }
  import nobots
}
gneee.tech {
  reverse_proxy {
    to organizr:80
  }
  import nobots
}
organizr.gneee.tech {
  reverse_proxy {
    to organizr:80
  }
  import nobots
}
bazarr.gneee.tech {
  reverse_proxy {
    to bazarr:6767
  }
  import nobots
}
tautulli.gneee.tech {
  reverse_proxy {
    to tautulli:8181
  }
  import nobots
  import private
}
```
As much as possible I try to use docker's hostnames, this make this setup really portable and easy to maintain.

### Cool snippets

#### No bots

I wrote a small rule that can help decrease the risks of being indexed or scanned by script kiddies on every subdomains.

```
(nobots) {
  @bot {
    header_regexp User-Agent Googlebot|aolbuild|baidu|bingbod|bingpreview|msnbot|duckduckbot|googlebot|adbot-google|mediapartners-google|teoma|slurp|yandex
  }
  respond @bot 403 {
    body "Not dank enough"
    close
  }
  respond /robots.txt 200 {
    body "User-agent: *
    Disallow: /"
  }
}
```

What this does is answer with an error request made by common bots on every page and every subdomains.

It also atomatically add a `/robots.txt` that tells indexers not to index any page of this website.

#### Private

To simplify maintanance I put some services on the reverse proxy I do not wish to access from outside my lan. This rule blocks access to those subdomains if the IP is not in my local network.

```
(private) {
  @external {
     not remote_ip 192.168.0.0/16
  }
  respond @external 403 {
    body "Only available on local network"
  }
}
```
