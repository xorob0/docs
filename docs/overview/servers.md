# Servers

## Nimbus

Nimbus is a VPS, hosted on [Hetzner](https://hetzner.com/). It's the cheapest VPS they offer with a single CPU core, 2Gb of RAM and 20Gb of SSD. I added two 10Gb volumes for my ZFS pool.

The reason I went with a VPS over a true selfhosted solution was mainly the availability. More and more people around me depend on my services so I need some reliability.

TODO: screenshot of hetzner

It runs ubuntu server and docker for the few services on there.

It's named Nimbus because it's in the cloud.
TODO: picture of nimbus from dragon ball

## Celty

TODO: Picture of Celty (the server)

Celty is my "Media" server, I used to host everything there, but that meant that during maintenances everything went down.
It's a i3-10100 with 16Gb of DDR4 and a lot of storage. The os is installed on a mirrored NVME drive for better reliability.

It was initially in my bedroom, about 2 meters from my bed when I was lived with my parents, that's why I tried to make it as silent as possible. And this silenceness is still usefull today as it is currently in my living room, hidden in plain sigh in my TV cabinet.

It runs Proxmox, mainly because its one of the few server distro that allow for root on ZFS in the installer. I might use some of the VM capability one day, but for the moment everything runs on docker straight from the host.

It's named after Celty Sturluson, a character from [Durarara!!](https://en.wikipedia.org/wiki/Durarara!!) who is black, mute, rides a noise-less bike and is litteraly headless.
TODO: Picture of Celty

## Tinker (Bell)

TODO: Picture of Tinker (server)

Tinker is my remote backup server. It's a simple Raspberry Pi 4 with 4Gb or RAM strapped to a 4To WD blue in a seagate usb enclosure.

It runs ubuntu server with ZFS and docker.

I made a deal with a friend, I could put a server in her appartment for my backup if the server also serves as a google photo replacement for her.

It's named after the disney character whom my friend like and I needed a name ¯\_(ツ)\_/¯. I often use `tinker` because it's shorter.

TODO: Picture of Tinker bell

## Ultron

TODO: Picture of ultron (home assistan)

Ultron is my Home Assistant box. It's again a simple Raspberry Pi, this time with 8Gb of RAM and no hard drive. I needed an onsite dedicated box for my home automation because I never want it to be down for any reason.

It's running Home Assistant OS with was not the smartest choice to integrate it with my network but I'll live with it for the time being.

Do I really need to explain why it's named Ultron ?
TODO: Picture of ultron
