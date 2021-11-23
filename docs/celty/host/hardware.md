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
- 9750-8i

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
