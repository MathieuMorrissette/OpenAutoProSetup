# OpenAutoProSetup
In /boot/config.txt add the following line to rotate screen by 180 degrees
```
lcd_rotate=2
```

In /boot/config.txt add the following line to enable rtc ds3231
```
dtoverlay=i2c-rtc,ds3231
```
