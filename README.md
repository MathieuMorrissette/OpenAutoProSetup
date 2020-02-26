# OpenAutoProSetup

This repo is to document my custom setup with open auto.

In /boot/config.txt add the following line to rotate screen by 180 degrees
```
lcd_rotate=2
```

In /boot/config.txt add the following line to enable rtc ds3231
```
dtoverlay=i2c-rtc,ds3231
```

## Chroot into Raspbian


```
pacman -S qemu

git clone https://aur.archlinux.org/proot.git && cd proot
makepkg -si

git clone https://aur.archlinux.org/glib2-static.git && cd glib2-static
makepkg -si

git clone https://aur.archlinux.org/pcre-static.git && cd pcre-static
makepkg -si

git clone https://aur.archlinux.org/qemu-user-static.git && cd qemu-user-static
makepkg -si

mount /dev/<device>2 /mnt
mount /dev/<device>1 /mnt/boot

cp /usr/bin/qemu-arm-static /mnt/usr/bin

echo ':arm:M::\x7fELF\x01\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x02\x00\x28\x00:\xff\xff\xff\xff\xff\xff\xff\x00\xff\xff\xff\xff\xff\xff\xff\xff\xfe\xff\xff\xff:/usr/bin/qemu-arm-static:' > /proc/sys/fs/binfmt_misc/register

mount -t proc /proc /mnt/proc
mount -o bind /dev /mnt/dev
mount -o bind /dev/pts /mnt/dev/pts
mount -o bind /sys /mnt/sys

chroot /mnt /bin/bash

export PATH=/sbin:/usr/sbin:/usr/bin:/bin

```


Then uninstall the fake-hwclock software and exit chroot

```
umount /mnt/{sys,proc,dev/pts,dev, boot}
umount /mnt

```

# Source
https://unix.stackexchange.com/questions/41889/how-can-i-chroot-into-a-filesystem-with-a-different-architechture
https://raspberrypi.stackexchange.com/questions/23675/install-raspbian-packages-directly-from-ubuntu-with-chroot-to-raspbian-file-syst
https://gist.github.com/mikkeloscar/a85b08881c437795c1b9
