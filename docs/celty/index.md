# Index

TODO: Picture of Celty (the server)


So why did I go with this setup ? I wanted to be able to transcode 4k so I don't have to keep 2 versions of every movies, and I wanted this upgrade to be my engame for a long time and at the same time, to still be upgradable if I need to, hence the single stick of ram and the Z490 chipset (that will be compatible with 11th gen intel core and their Xe iGPUs). This motherboard also has 2.5Gb ethernet which may be important for the future.
## Hardware

It's a [i3-10100](https://ark.intel.com/content/www/us/en/ark/products/199283/intel-core-i310100-processor-6m-cache-up-to-4-30-ghz.html) with 16Gb of DDR4 and a lot of storage. The OS is installed on a ZFS mirrored NVME drive for reliability.

One of the issue I faced is my motherboard disabling 2 SATA port when adding a second NVME drive. To fix this I used a passive m.2 to PCIe board [from Aliexpress](https://www.aliexpress.com/wholesale?SearchText=pci%20to%20m2).

I have a RAID card, but it's not in use at the moment

- CPU: [i3-10100](https://ark.intel.com/content/www/us/en/ark/products/199283/intel-core-i3-10100-processor-6m-cache-up-to-4-30-ghz.html)
- Motherboard: [MSI Z490-A PRO](https://www.msi.com/Motherboard/Z490-A-PRO)
- RAM: 1x16Go
- Boot drive: 2x [Sandisk Extreme Pro 500Gb](https://shop.westerndigital.com/en-ap/products/internal-drives/sandisk-extreme-pro-m2-nvme-3d-ssd)
- Cooler: Evo 212
- Case: Nanoxia Deep Silence 3

What I looked after when building this machine was:

- A good iGPU for Plex transcoding
- A lot of SATA port
- Expandable in the future:
  - Z490 chips that is compatible with 11th gen CPU (and Xe iGPUs)
   - 2.5Gbps Ethernet
   - lots of PCIe ports
   
### Hard Drives

I currently have 7 hard drives in this box:

- 2\*4To
- 2\*6To
- 2\*12To
- 1\*480Go SSD

I now shuck my hard drives
TODO: make a shucking explanation

## Software

It runs [Proxmox](proxmox.md), mainly because its one of the few server distro that allow for root on [ZFS](zfs.md) in the installer. I might use some of the VM capability one day, but for the moment everything runs on [Docker](docs/celty/host/docker.md) straight from the host.

## Story
### Hardware

Let's start with the story of how I started sefhosting. This was on a Raspberry Pi 2B with a 2Tb usb drive, the only thing it did back then was download files that I could access via SSHFS. This was really terrible, this setup could only withstand a few downloads at a time and I had to pause all downloads to access the files.

Then came Celty. I got her for 50€ from a acquaintance. She was only a 4th gen i5 with 8Gb of RAM and a few hard drives. She was going to stay in my bedroom so I had to make her as silent as possible. This is why I got an Evo 212 and a Nanoxia Deep Silence 3. At that point I installed FreeNAS on her and started playing with jails, I selfhosted a bunch of stuff, and started de-googlizing my life.

When I moved to my first apartment is was in my TV closet, so the silent factor was still really important.

### Software
The Software side of things had a lot more iterations than the hardware side.

Back on my Raspberry Pi I was on Open Media Vault and really didn't like it. Every update broke the system, but I didn't have a lot of experience back then so that may be my fault too 🤷.

On Celty I used FreeNAS for a long time. Back in the days it was basically the only way to have ZFS with good performances. I kept FreeNAS for a few years until the release of [OpenZFS](https://github.com/openzfs/zfs) 2.0.0 which made it possible to move to Linux.

At that time I a friend was setting up his server with OMV and docker and the simply of docker really intrigued me. That's why on December 2020 I moved to Ubuntu 20.04 with docker and [OpenZFS](https://github.com/openzfs/zfs). I loved it even if the [OpenZFS](https://github.com/openzfs/zfs) setup was quite messy because it was not yet officially supported by Ubuntu.

A few weeks later I upgraded my hardware and kind of broke my install. I decided to go with [Proxmox VE](https://www.proxmox.com/en/proxmox-ve) as it was supposed to have a really up to date [OpenZFS](https://github.com/openzfs/zfs) version. I discovered this was false and had to install the beta kernel to have it working.

On my latest setup I tried [TrueNAS SCALE](https://www.truenas.com/truenas-scale/) which just lacks too much docker features for me at the moment and Ubuntu server which I dumped because it doesn't support root on ZFS right now.

### Name
It's named after Celty Sturluson, a character from [Durarara!!](https://en.wikipedia.org/wiki/Durarara!!) who is black, mute, rides a noise-less bike and is literally headless.
![Celty Sturluson from Durarara](../assets/Celty.png)