# ZFS

With my latest disk upgrade I started managing 2 pools, a stripped pool with most of my disks (badly named `HDD1`) and an other stripped pool with the disks I don't want in my main pool (named `extra`).

As explained above, I don't want my main pool to ever get too big, this reduces the risk that one of my disk would fail and also let me keep one SATA port available at all time in case I need to replace a drive.

I only have a few datasets:

- `HDD1/Media`: with all my medias (and my download folder). This needs to be on the same dataset so I can hardlink my movies from my download folder to my Movies folder (and avoid duplicates)
- `HDD1/Documents`: with my NextCloud storage, including my pictures
- `HDD1/Backups`: with some old unorganized backups and some new Time Machine backups
- `HDD1/Public`: with data from linx, it's limited to 200Go

I also have a ZFS root (`rpool`) partition with a few datasets

- `rpool/configs`: all my configs folders that I mount on my docker containers
  - `rpool/configs/plex`: some of my container have their own datasets so it's easier to backup
  
  `extra` is only used as a backup pool locally, all the dataset there are created from ZFS send/recv.

### Migration

To migrate from an existing [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) to a new install, all I have to do is:

```
rsync -av /mnt/old/configs /configs
rsync -av /mnt/old/var/lib/docker /docker
```
