# Storage

# Configure 3Ware LSI card on Proxmox 6.4

This was only tested on 9750-4i and 9750-8i

## Install the repositories

```
cd /tmp
wget http://hwraid.le-vert.net/debian/hwraid.le-vert.net.gpg.key
apt-key add hwraid.le-vert.net.gpg.key
rm hwraid.le-vert.net.gpg.key
```

## Install tw-cli

```
apt update
apt install tw-cli
```

## Setup disk