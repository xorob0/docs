# Hardware

## Story

Let's start with the story of how I started sefhosting. This was on a Raspberry Pi 2B with a 2Tb usb drive, the only thing it did back then was download files that I could access via SSHFS. This was really terrible, this setup could only withstand a few downloads at a time and I had to pause all downloads to access the files.

Then came Celty. I got her for 50€ from a acquaintance. She was only a 4th gen i5 with 8Gb of RAM and a few hard drives. She was going to stay in my bedroom so I had to make her as silent as possible. So I got an Evo 212 and a Nanoxia Deep Silence 3 and was able to sleep next to the computer easily. At that point I installed FreeNAS on her and started playing with jails, I selfhosted a bunch of stuff, and started de-googlizing my life.

## Current config

When I started working I gave Celty some upgrades and she became what she is today:

- CPU: i3-10100
- Motherboard: MSI Z490-A PRO
- RAM: 1x16Go
- Cooler: Evo 212
- Case: Nanoxia Deep Silence 3

So why did I go with this setup ? I wanted to be able to transcode 4k so I don't have to keep 2 versions of every movies, and I wanted this upgrade to be my engame for a long time and at the same time, to still be upgradable if I need to, hence the single stick of ram and the Z490 chipset (that will be compatible with 11th gen intel core and their Xe iGPUs). This motherboard also has 2.5Gb ethernet which may be important for the future.

# Hard Drives

I currently have 6 hard drives in this box:

- 2*4To
- 2*6To
- 1*12To
- 1*480Go SSD

Everything is SATA for the moment. I hit a point now where I have as much drives as SATA ports, that means two important things:

- If I need all my drives at the same time, I don't have a port available to replace a disk if it starts behaving
- For my next upgrade I'll need a PCIe card which is either expensive or shitty
