## MT6768 downstream kernel blobs

### Open-source kernels:
#### 4.14
Not recommended due to poor code quality.

- [Xiaomi Redmi 9 (lancelot) / Helio G80](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/tree/lancelot-q-oss)
- [Xiaomi Redmi Note 9 (merlin) / Helio G85](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/tree/merlin-r-oss)

...and other 4.14 kernels

[Sample DTS](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/blob/merlin-r-oss/arch/arm64/boot/dts/mediatek/mt6768.dts)

#### 4.19
This is a good reference for devices that don't have newer, publicly available kernels.

A few Mediatek drivers (e.g., MMC) have switched to a mainline-like driver.

- [Xiaomi Redmi 12 (fire) / Helio G88](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/tree/fire-t-oss)
- [Xiaomi Redmi 13C (gale) / Helio G85](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/tree/gale-s-oss)

[Sample DTS](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/blob/gale-s-oss/arch/arm64/boot/dts/mediatek/mt6768.dts)

#### 5.10
The code quality has improved overall, though only for a few drivers.

- [Generic kernel](https://github.com/OnePlusOSS/android_kernel_5.10_oneplus_mt6983)

[Sample DTS](https://github.com/OnePlusOSS/android_kernel_5.10_oneplus_mt6983/blob/ff51a39c66a87f91d870bfff1611e2b36371c8a4/arch/arm64/boot/dts/mediatek/mt6768.dts)

#### 6.6
Recommended, (minor?) improvements over 5.10. Run `cd kernel/kernel_device_modules-6.6` to get a linux-like directory structure

- [Generic kernel](https://github.com/oppo-source/android_kernel_modules_and_devicetree_oppo_mt6991/blob/a98a9db1584a71c42919a78bfe2de7160f355ff9)
- [Samsung A05s / Helio G85](https://github.com/mt6768-mainline/android_kernel_samsung_mt6768)

[Sample DTS](https://github.com/mt6768-mainline/android_kernel_samsung_mt6768/blob/master/kernel/kernel_device_modules-6.6/arch/arm64/boot/dts/mediatek/mt6768.dts)

### Closed-source kernels:

#### 5.10.209
HyperOS 1 is known to use it with the Redmi 14C. Perhaps this is true for the whole MT6768 family.

#### 6.6.30
HyperOS 2 uses it.

- [Xiaomi Redmi 12 (fire) / Helio G88](./fire_global_images_OS2.0.5.0.VMXMIXM_15.0.dts)
- [Xiaomi Redmi 14C (lake) / Helio G81-Ultra (rebranded G85?)](./lake_global_images_OS2.0.3.0.VGTMIXM_15.0.dts)

Refer to DTS file names for HyperOS version

### Extracting DTB
1. Download fastboot HyperOS
2. Go to `images` directory
3. Get kernel version:
    - Run `binwalk -Me boot.img`
    - Run `strings extractions/boot.img.extracted/*/decompressed.bin | grep 'Linux version'`
4. `binwalk -M vendor_boot.img`
5. Find entry with Device tree blob entry and copy first value
6. Run `dd if=vendor_boot.img of=dtb bs=1 skip=*paste value here*`
7. Run `dtc -I dtb -O dts -o *put os version and codename here*.dts dtb`

### Extracting DTBO
1. Clone [extraction tool](https://github.com/cfig/Android_boot_image_editor), otherwise run `extract-dtb dtbo.img`, switch to directory with dtb and go to step 7 of [Extracting DTB](#extracting-dtb)
2. Copy `dtbo.img` to cloned directory
3. Run `./gradlew unpack`
4. Copy `build/unzip_boot/dt/dt.0.dts` somewhere and rename it to `*codename*-*version*-dtbo.dts`


Any DTS/DTBO PRs appreciated.
