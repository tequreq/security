# Physcial

My Personal Checklist is as follows:

```
Common office attire
gates
fences
cameras
guard force
doors
badges (which door requires them / what do they look like)
hours
barriers
co-location (shared building)
night infiltration
cover infiltration
id cloning
google maps
online building info
```



Note if having issues cloning badges, make sure to update the firmware on the proxmark



\(abbreviated\) version

```
 sudo apt-get install git build-essential libreadline5 libreadline-dev gcc-arm-none-eabi libusb-0.1-4 libusb-dev libqt4-dev ncurses-dev perl pkg-config
 git clone https://github.com/Proxmark/proxmark3.git
 cd proxmark3
 ls
 make clean && make all
```

Plug in Proxmark3

```
dmesg | grep -i usb
cd client
make
./flasher /dev/ttyACM0 ../armsrc/obj/fullimage.elf 
./proxmark3 /dev/ttyACM0 
```

[https://github.com/Proxmark/proxmark3/wiki](https://github.com/Proxmark/proxmark3/wiki)



