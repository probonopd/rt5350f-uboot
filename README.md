# rt5350f-uboot

This is a modified bootloader for the [A5 V11 Router](https://wiki.openwrt.org/toh/unbranded/a5-v11). It allows openWRT to be flashed. This is merely a Backup of wertwert4pda/rt5350f-uboot which disappeared on Dec 22, 2016. I do not have the source code.

More information at http://tech.scargill.net/a5-v11-router/

```
# 32 MB flash router with "Qualcomm" firmware GUI

telnet 192.168.xxx.xxx -l admin

Trying 192.168.xxx.xxx...
Connected to 192.168.xxx.xxx.
Escape character is '^]'.

M1 login: admin
Password: admin

BusyBox v1.12.1 (2012-08-27 10:10:44 CST) built-in shell (ash)
Enter 'help' for a list of built-in commands.

# Mount the USB thumbdrive on which the firmware resides
# mount /dev/sda1 /mnt

# cat /proc/meminfo 
MemTotal:        28616 kB
MemFree:          5052 kB
(...)

# mtd_write write /mnt/uboot_usb_256_03.img Bootloader
Unlocking Bootloader ...
Writing from /mnt/uboot_usb_256_03.img to Bootloader ...  [w]
# 

# mtd_write write /mnt/openwrt-15.05-ramips-rt305x-a5-v11-squashfs-sysupgrade.bin Kernel
Unlocking Kernel ...
Writing from /mnt/aaaatemp_openwrt/openwrt-15.05-ramips-rt305x-a5-v11-squashfs-sysupgrade.bin to Kernel ...  [w]
#

reboot
```

I can now put a new sysupgrade image named `firmware.bin` to the root directory of a FAT formatted USB stick and boot the router with the reset button pressed. It should flash the firmware image during which it binks the blue LED, or, if it cannot, open a TFTP server.

In OpenWrt I seem to have an empty MAC address... not sure if this is related to the bootloader.
