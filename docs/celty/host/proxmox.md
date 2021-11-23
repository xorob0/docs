# Software

She runs [Proxmox](host/proxmox.md), mainly because its one of the few server distro that allow for root on [ZFS](zfs.md) in the installer. I might use some of the VM capability one day, but for the moment everything runs on [Docker](docs/celty/host/docker.md) straight from the host.

## Proxmox

### Setup

- Download [the latest image](https://www.proxmox.com/en/downloads/category/iso-images-pve)
- Flash on an usb stick
- Install from GUI

### Tips

#### Edge Kernel

EDIT: this is not needed anymore with PVE 7.1

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