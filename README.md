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
NOT TESTED : https://raspberrypi.stackexchange.com/questions/23675/install-raspbian-packages-directly-from-ubuntu-with-chroot-to-raspbian-file-syst

Use the following script :
https://gist.github.com/htruong/7df502fb60268eeee5bca21ef3e436eb

Make sure to install the required packages :
```
(sudo) pacman -S qemu

git clone https://aur.archlinux.org/glib2-static.git && cd glib2-static
makepkg -si

cd ..

git clone https://aur.archlinux.org/pcre-static.git && cd pcre-static
makepkg -si

cd ..

git clone https://aur.archlinux.org/qemu-user-static.git && cd qemu-user-static
makepkg -si
```

