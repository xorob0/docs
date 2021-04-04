# AdGuard Home

[AdGuard Home](https://github.com/AdguardTeam/AdGuardHome) is a dns that can block ads, cache queries and works with DoH and DoT.

## Compose

```
version: "3.3"
services:
  adguardhome:
    image: adguard/adguardhome
    container_name: adguardhome
    ports:
      - 53:53/tcp
      - 53:53/udp
      - 67:67/udp
      - 68:68/tcp
      - 68:68/udp
    volumes:
      - /configs/adguard/work:/opt/adguardhome/workdir
      - /configs/adguard/conf:/opt/adguardhome/confdir
    restart: unless-stopped
```
