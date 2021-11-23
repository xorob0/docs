# Proxmox



# Hard Drives

I currently have 6 hard drives in this box:

- 2\*4To
- 2\*6To
- 1\*12To
- 1\*480Go SSD

I am now saturating my motherboard's SATA connectors, which is not a good thing.

# Software

## Story

The Software side of things had a lot more iterations than the hardware side.

Back on my Raspberry Pi I was on Open Media Vault and really didn't like it. Every update broke the system, but I didn't have a lot of experience back then so that may be my fault too 🤷.

On Celty I used FreeNAS for a long time. Back in the days it was basically the only way to have ZFS with good performances. I kept FreeNAS for a few years until the release of [OpenZFS](https://github.com/openzfs/zfs) 2.0.0 which made it possible to move to Linux.

At that time I a friend was setting up his server with OMV and docker and the simply of docker really intrigued me. That's why on December 2020 I moved to Ubuntu 20.04 with docker and [OpenZFS](https://github.com/openzfs/zfs). I loved it even if the [OpenZFS](https://github.com/openzfs/zfs) setup was quite messy because it was not yet officially supported by Ubuntu.

A few weeks later I upgraded my hardware and kind of broke my install. I decided to go with [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) as it was supposed to have a really up to date [OpenZFS](https://github.com/openzfs/zfs) version. I discovered this was false and had to install the beta kernel to have it working.

On my latest setup I tried [TrueNAS SCALE](https://www.truenas.com/truenas-scale/) which just lacks too much docker features for me at the moment and Ubuntu server which I dumped because it doesn't support root on ZFS right now.

## Current config

### Operating System

#### Setup

I did my first [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) install for the ZFS support, which happened to be not as good as I hoped. But right now I am still rocking [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) for it root on ZFS support and I really like it. I have a dual NVME boot drive in ZFS mirror and I can easily do snapshot of anything on my OS disk.

#### Tips

#### Edge Kernel

I had to install the [edge kernel](https://github.com/fabianishere/pve-edge-kernel) to get my ethernet card working:

```
cd /tmp
wget $(curl -s https://api.github.com/repos/fabianishere/pve-edge-kernel/releases/latest | grep 'browser_' | cut -d\" -f4 | grep headers)
wget $(curl -s https://api.github.com/repos/fabianishere/pve-edge-kernel/releases/latest | grep 'browser_' | cut -d\" -f4 | grep kernel | head -1)
apt install pve-edge-*.deb
```

#### PVE Test Repository

To have a recent enough version of ZFS on Linux I needed to install the [PVE Test Repository](https://pve.proxmox.com/wiki/Package_Repositories#sysadmin_test_repo).

```
echo "deb http://download.proxmox.com/debian/pve buster pvetest" >> /etc/apt/sources.list
apt update
apt upgrade
```

### ZFS

With my latest disk upgrade I started managing 2 pools, a stripped pool with most of my disks (badly named `HDD1`) and an other stripped pool with the disks I don't want in my main pool (named `extra`).

As explained above, I don't want my main pool to ever gets bigger than 5 disks, this reduces the risk that one of my disk would fail and also let me keep one SATA port available at all time in case I need to replace a drive.

I only have a few datasets:

- `HDD1/Media`: with all my medias (and my download folder). This needs to be on the same dataset so I can hardlink my movies from my download folder to my Movies folder (and avoid duplicates)
- `HDD1/Documents`: with my NextCloud storage, including my pictures
- `HDD1/Backups`: with some old unorganized backups and some new Time Machine backups
- `HDD1/Public`: with data from linx, it's limited to 200Go

I also have a ZFS root (`rpool`) partition with a few datasets

- `rpool/configs`: all my configs folders that I mount on my docker containers
  - `rpool/configs/plex`: some of my container have their own datasets so it's easier to backup

### Migration

To migrate from an existing [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) to a new install, all I have to do is:

```
rsync -av /mnt/old/configs /configs
rsync -av /mnt/old/var/lib/docker /docker
```

### Docker installation

I install docker directly on the [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) host as I probably won't ever use LXC or KVM.

```
apt remove docker docker-engine docker.io containerd runc
apt update
apt install apt-transport-https ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
apt update
apt install docker-ce docker-ce-cli containerd.io
systemctl start docker
systemctl enable docker
```

For raspberry pi:

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo bash get-docker.sh
```

#### Portainer Setup

As I do almost everything from portainer I just fire it up and do everything from the commandline.

```
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /configs/portainer:/data portainer/portainer-ce
```

If I ran the migration lines this part should not even be needed.
