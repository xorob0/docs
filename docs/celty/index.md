# Index

TODO: Picture of Celty (the server)

[hardware](host/hardware.md)

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