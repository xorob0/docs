# Proxmox

## Setup

I did my first [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) install for the ZFS support, which happened to be not as good as I hoped. But right now I am still rocking [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) for it root on ZFS support and I really like it. I have a dual NVME boot drive in ZFS mirror and I can easily do snapshot of anything on my OS disk.

## Tips

### Edge Kernel

I had to install the [edge kernel](https://github.com/fabianishere/pve-edge-kernel) to get my ethernet card working:

```
cd /tmp
wget $(curl -s https://api.github.com/repos/fabianishere/pve-edge-kernel/releases/latest | grep 'browser_' | cut -d\" -f4 | grep headers)
wget $(curl -s https://api.github.com/repos/fabianishere/pve-edge-kernel/releases/latest | grep 'browser_' | cut -d\" -f4 | grep kernel | head -1)
apt install pve-edge-*.deb
```

### PVE Test Repository

To have a recent enough version of ZFS on Linux I needed to install the [PVE Test Repository](https://pve.proxmox.com/wiki/Package_Repositories#sysadmin_test_repo).

```
echo "deb http://download.proxmox.com/debian/pve buster pvetest" >> /etc/apt/sources.list
apt update
apt upgrade
```

