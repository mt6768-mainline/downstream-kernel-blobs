## MT6768 downstream kernel blobs

### Open-source kernels:
#### DTS from 2018 (4.14)
- [Xiaomi Redmi 9 (lancelot)](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/tree/lancelot-q-oss)
- [Xiaomi Redmi Note 9 (merlin)](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/tree/merlin-r-oss)
...and other 4.14 kernels

[Sample DTS](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/blob/merlin-r-oss/arch/arm64/boot/dts/mediatek/mt6768.dts)
### DTS from 2019 (4.19)
- [Xiaomi Redmi 12 (fire)](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/tree/fire-t-oss)
- [Xiaomi Redmi 13C (gale)](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/tree/gale-s-oss)

[Sample DTS](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/blob/gale-s-oss/arch/arm64/boot/dts/mediatek/mt6768.dts)

### Closed-source kernels (6.6.30):
- [Xiaomi Redmi 12 (fire)](./fire_global_images_OS2.0.5.0.VMXMIXM_15.0.dts)
- [Xiaomi Redmi 14C (lake)](./lake_global_images_OS2.0.3.0.VGTMIXM_15.0.dts)

Refer to DTS file names for HyperOS version

### Extracting DTB
1. Download fastboot HyperOS
2. Go to `images` directory
3. Get kernel version:
  - `binwalk -Me boot.img`
  - `strings extractions/boot.img.extracted/*/decompressed.bin | grep 'Linux version'`
4. `binwalk -M vendor_boot.img`
5. Find entry with Device tree blob entry and copy first value
6. `dd if=vendor_boot.img of=dtb bs=1 skip=*paste value here*`
7. `dtc -I dtb -O dts -o *put os version and codename here*.dts dtb`
