## Servers

### Nimbus

Nimbus is a VPS, hosted on [Hetzner](https://hetzner.com/). It's the cheapest VPS they offer with a single CPU core, 2Gb of RAM and 20Gb of SSD. I added two 10Gb volumes for my ZFS pool.

I went with a VPS over a true selfhosted solution for the better availability. More and more people around me depend on my services so I need some reliability.

[[hetzner_nimbus_specs_screenshot.png]]

It runs ubuntu server and docker for the few services on there.

It's named Nimbus because it's in the cloud.
TODO: picture of nimbus from dragon ball


## Tinker (Bell)

TODO: Picture of Tinker (server)

Tinker is my remote backup server. It's a simple Raspberry Pi 4 with 4Gb or RAM strapped to a 4To WD blue in a seagate usb enclosure.

It runs ubuntu server with ZFS and docker.

I made a deal with a friend, I could put a server in her appartment for my backup if the server also serves as a google photo replacement for her.

It's named after the disney character whom my friend like and I needed a name ¯\_(ツ)\_/¯. I often use `tinker` because it's shorter.

TODO: Picture of Tinker bell

## AIDA

TODO: Picture of AIDA (home assistant)

AIDA is my Home Assistant box. It's again a simple Raspberry Pi, this time with 8Gb of RAM and no hard drive. I needed an onsite dedicated box for my home automation because I never want it to be down for any reason. Ever.

It's running Ubuntu Server and not Home Assistant OS. This is because I wanted more control over the device (to add exporters, install custom containers,...)

It's named after AIDA from Agent of Shield, a robot that read the Darkhold and became an overpowered evil AI trying to become human.

![Picture of AIDA from Agents of Shield](../assets/AIDA.jpg)