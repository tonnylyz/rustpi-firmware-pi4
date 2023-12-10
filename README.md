# Rustpi on Raspberry Pi 4

This repo is the content of the first FAT32 partition.

It contains:

* DTB, bootloaders from https://github.com/raspberrypi/firmware
* Prebuilt u-boot from https://source.denx.de/u-boot/u-boot
* Prebuilt ATF(secure monitor/bl31 only) from https://github.com/ARM-software/arm-trusted-firmware

Example command to boot native Linux:

```
fatload mmc 0:1 0x200000 kernel8.img
fatload mmc 0:1 ${ramdisk_addr_r} initramfs-linux.img
booti 0x200000 ${ramdisk_addr_r} ${fdt_addr}
```

Example command to boot Rustpi
```
setenv ipaddr 192.168.110.2
setenv netmask 255.255.255.0
saveenv
tftp 0x1000000 192.168.110.1:rustpi.ubi; bootm start 0x1000000 - ${fdt_addr}; bootm loados; bootm go
```
