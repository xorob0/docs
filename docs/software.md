# Software

## Story

The Software side of things had a lot more iterations than the hardware side.

Back on my Raspberry Pi I was on Open Media Vault and really didn't like it. Every update broke the system, but I didn't have a lot of experience back then so that may be my fault too 🤷.

On Celty I used FreeNAS for a long time. Back in the days it was basically the only way to have ZFS with good performances. I kept FreeNAS for a few years until the release of OpenZFS 2.0.0 which made it possible to move to Linux.

At that time I a friend was setting up his server with OMV and docker and the simply of docker really intrigued me. That's why on December 2020 I moved to Ubuntu 20.04 with docker and OpenZFS. I loved it even if the OpenZFS setup was quite messy because it was not yet officially supported by Ubuntu.

## Current config

### Operating System

A few weeks later I upgraded my hardware and kind of broke my install. I decided to go with Proxmox as it was supposed to have a really up to date OpenZFS version. I discovered this was false and had to install the beta kernel to have it working.

In hindsight, Proxmox is really not the best OS for me, but I'll stick to it until I get my hand on 2 NVME drive and _need_ to re-install everything. I'll probably go with an Ubuntu install again but this time with ZFS for my SSD to use snapshots on my configs.

### ZFS

With my latest disk upgrade I started managing 2 pools, a stripped pool with most of my disks (badly named `HDD1`) and an other stripped pool with the disks I don't want in my main pool (named `extra`).

As explained above, I don't want my main pool to ever gets bigger than 4 disks, this reduces the risk that one of my disk would fail and also let me keep one SATA port available at all time in case I need to replace a drive. That maximun number of disk might increase to 5 when I get some NVME drives for my OS.

#TODO: datasets

https://github.com/fabianishere/pve-edge-kernel
https://pve.proxmox.com/wiki/Package_Repositories
https://github.com/jimsalterjrs/sanoid/blob/master/INSTALL.md
rsync /configs
rsync /var/lib/docker

https://raw.githubusercontent.com/portainer/templates/master/templates-2.0.json
