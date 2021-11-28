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
    header_regexp User-Agent Googlebot|aolbuild|baidu|bingbod|bingpreview|msnbot|duckduckbot|googlebot|adbot-google|mediapartners-google|teoma|slurp|yandex|Indy*Library|libwww-perl|GetRight|GetWeb!|Go!Zilla|Download*Demon|Go-Ahead-Got-It|TurnitinBot|GrabNet
  }

  @badwords {
    path_regexp \b(ultram|unicauca|valium|viagra|vicodin|xanax|ypxaieo|erections|hoodia|huronriveracres|impotence|levitra|libido|ambien|blue\spill|cialis|cocaine|ejaculation|erectile|lipitor|phentermin|pro[sz]ac|sandyauer|tramadol|troyhamby)\b
  }

  @sql {
    path_regexp \b(union.*select.*\(|union.*all.*select.*|concat.*\()\b
  }

  @block {
    path_regexp \b([a-zA-Z0-9_]=http://|[a-zA-Z0-9_]=(\.\.//?)+|[a-zA-Z0-9_]=/([a-z0-9_.]//?)+)\b
  }

  @exploits {
    path_regexp \b((<|%3C).*script.*(>|%3E)|GLOBALS(=|\[|\%[0-9A-Z]{0,2})|_REQUEST(=|\[|\%[0-9A-Z]{0,2})|proc/self/environ|mosConfig_[a-zA-Z_]{1,21}(=|\%3D)|base64_(en|de)code\(.*\))\b
 }

  respond @bot 403 {
    body "Not dank enough"
    close
  }
  respond @badwords 403 {
    body "Not dank enough"
    close
  }
  respond @sql 403 {
    body "Not dank enough"
    close
  }
  respond @block 403 {
    body "Not dank enough"
    close
  }
  respond @exploits 403 {
    body "Not dank enough"
    close
  }

  header Permissions-Policy "interest-cohort=()"

  respond /robots.txt 200 {
    body "User-agent: *
    Disallow: /"
  }
}

(management) {
  @external {
     not remote_ip 10.200.0.0/24
  }
  respond @external 503 {
    body "Server is having issues"
  }
  tls internal
}

caddy.celty {
  metrics /metrics
  import management
}
cadvisor.celty {
  reverse_proxy {
    to cadvisor:8080
  }
  import management
}
nodeexporter.celty {
  reverse_proxy {
    to nodeexporter:9100
  }
  import management
}
nodeexporter.bifrost {
  reverse_proxy {
    to 192.168.2.1:9100
  }
  import management
}
cadvisor.aida {
  reverse_proxy {
    to 192.168.2.65:8080
  }
  import management
}
nodeexporter.aida {
  reverse_proxy {
    to 192.168.2.65:9100
  }
  import management
}
torrents.celty {
  reverse_proxy {
    to flood:3000
  }
  import management
}
ugly.torrents.celty {
  reverse_proxy {
    to qbittorrent:8080
  }
  import management
}
s3.gneee.tech {
  reverse_proxy {
    to minio:9000
  }
  import nobots
}
radarr.celty {
  reverse_proxy {
    to radarr:7878
  }
  import management
}
sonarr.celty {
  reverse_proxy {
    to sonarr:8989
  }
  import management
}
lidarr.celty {
  reverse_proxy {
    to lidarr:8686
  }
  import management
}
print.celty {
  reverse_proxy {
    to 192.168.2.37:80
  }
  import management
}
linx.gneee.tech {
  reverse_proxy {
    to linx-server:8080
  }
  import nobots
}
plex.gneee.tech {
  reverse_proxy {
    to plex:32400
  }
  import nobots
}
bazarr.celty {
  reverse_proxy {
    to bazarr:6767
  }
  import management
}
tautulli.celty {
  reverse_proxy {
    to tautulli:8181
  }
  import management
}
ebooks.celty {
  reverse_proxy {
    to calibre-web:8083
  }
  import management
}
calibre.celty {
  reverse_proxy {
    to calibre:8080
  }
  import management
}
dupeguru.celty {
  reverse_proxy {
    to dupeguru:5800
  }
  import management
}
photos.celty {
  reverse_proxy {
    to librephotos:80
  }
  import management
}
cloud.celty {
  reverse_proxy {
    to nextcloud:80
  }
  import management
}
```
As much as possible I try to use docker's hostnames, this make this setup really portable and easy to maintain.

### Cool snippets

#### No bots

I wrote a few rules that can help decrease the risks of being indexed or scanned by script kiddies on every subdomains.
They are inspired from the nginx no bot config.

```
(nobots) {
  @bot {
    header_regexp User-Agent Googlebot|aolbuild|baidu|bingbod|bingpreview|msnbot|duckduckbot|googlebot|adbot-google|mediapartners-google|teoma|slurp|yandex|Indy*Library|libwww-perl|GetRight|GetWeb!|Go!Zilla|Download*Demon|Go-Ahead-Got-It|TurnitinBot|GrabNet
  }

  @badwords {
    path_regexp \b(ultram|unicauca|valium|viagra|vicodin|xanax|ypxaieo|erections|hoodia|huronriveracres|impotence|levitra|libido|ambien|blue\spill|cialis|cocaine|ejaculation|erectile|lipitor|phentermin|pro[sz]ac|sandyauer|tramadol|troyhamby)\b
  }

  @sql {
    path_regexp \b(union.*select.*\(|union.*all.*select.*|concat.*\()\b
  }

  @block {
    path_regexp \b([a-zA-Z0-9_]=http://|[a-zA-Z0-9_]=(\.\.//?)+|[a-zA-Z0-9_]=/([a-z0-9_.]//?)+)\b
  }

  @exploits {
    path_regexp \b((<|%3C).*script.*(>|%3E)|GLOBALS(=|\[|\%[0-9A-Z]{0,2})|_REQUEST(=|\[|\%[0-9A-Z]{0,2})|proc/self/environ|mosConfig_[a-zA-Z_]{1,21}(=|\%3D)|base64_(en|de)code\(.*\))\b
 }

  respond @bot 403 {
    body "Not dank enough"
    close
  }
  respond @badwords 403 {
    body "Not dank enough"
    close
  }
  respond @sql 403 {
    body "Not dank enough"
    close
  }
  respond @block 403 {
    body "Not dank enough"
    close
  }
  respond @exploits 403 {
    body "Not dank enough"
    close
  }

  header Permissions-Policy "interest-cohort=()"

  respond /robots.txt 200 {
    body "User-agent: *
    Disallow: /"
  }
}


```

These rules respond with error for commonly used bad word, exploit and for all bots (based on their user agent).
It also automatically add a `/robots.txt` that tells indexers not to index any page of this website.

#### Management

For services that do not need to be accessed by other people I restrict access to only the IPs from my nebula setup. I also use a self signed tls to be able to use `.celty` domains.

```
(management) {
  @external {
     not remote_ip 10.200.0.0/24
  }
  respond @external 403 {
    body "Not dank enough"
  }
  tls internal
}
```
