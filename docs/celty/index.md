# Index

TODO: Picture of Celty (the server)
## Hardware

It's a [i3-10100](https://ark.intel.com/content/www/us/en/ark/products/199283/intel-core-i310100-processor-6m-cache-up-to-4-30-ghz.html) with 16Gb of DDR4 and a lot of storage. The os is installed on a ZFS mirrored NVME drive for reliability.

One of the issue I faced is my motherboard disabling 2 SATA port when adding a second NVME drive. To fix this I used a passive m.2 to pcie board from aliexpress.

I have a RAID card, but it's not in use at the moment

TODO: part list

What I looked after when building this machine was:

- A good iGPU for  

## Software

It runs [Proxmox](proxmox.md), mainly because its one of the few server distro that allow for root on [ZFS](zfs.md) in the installer. I might use some of the VM capability one day, but for the moment everything runs on [Docker](docs/celty/host/docker.md) straight from the host.

## Story

Celty is my "Media" server, I used to host everything there, but that meant that during maintenance everything went down.
It was initially in my bedroom, about 2 meters from my bed when I was lived with my parents, that's why I tried to make it as silent as possible. And this quietness is still useful today as it is currently in my living room, hidden in plain sigh in my TV cabinet.

It's named after Celty Sturluson, a character from [Durarara!!](https://en.wikipedia.org/wiki/Durarara!!) who is black, mute, rides a noise-less bike and is literally headless.
![Celty Sturluson from Durarara](../assets/Celty.png)