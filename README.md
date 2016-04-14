# How setup a Beaglebone Black and tweak to fast development
# Como configurar a Beaglebone Black e tweaks para desenvolvimento rápido

## Install new system http://elinux.org/BeagleBoardDebian
### Download
```
wget https://rcn-ee.com/rootfs/2016-03-11/elinux/debian-8.3-console-armhf-2016-03-11.tar.xz
tar xf debian-8.3-console-armhf-2016-03-11.tar.xz
cd debian-8.3-console-armhf-2016-03-11
```
### Insert SD-Card to your computer
```
sudo ./setup_sdcard.sh --probe-mmc
sudo ./setup_sdcard.sh --mmc /dev/sdX --dtb beaglebone
```
### Uncomment last line ()
```
sudo nano uEnv.txt
```
### Unplug everything from the board, insert the SDCard, press and hold S2 switch and plug the power source. Keep holding the switch S2 through the sequence of blinks 4 LEDS ON -> 4 LEDS OFF -> LEDS STARTS TO BLINK, now you can release the switch. After some seconds you should see this pattern https://youtu.be/o885-0BmEpo

## First connect
You can connect with ssh via ethernet:
```
ssh debian@ip
```

or usb (https://learn.adafruit.com/ssh-to-beaglebone-black-over-usb/overview):
* Installing Drivers (Linux)
```
wget http://beagleboard.org/static/Drivers/Linux/FTDI/mkudevrule.sh
sudo ./mkudevrule.sh
```
This script will create a new file called 73-beaglebone.rules in /etc/udev/rules.d/You will probably need to run the script as superuser."

* Connecting
```
ssh debian@192.168.7.2
```


## Config
### Change hostname (arm->name) "name" is the name of the board that you want to connect via network without knowing the ip
```
sudo nano /etc/hosts
sudo nano /etc/hostname
```
### Change password
```
sudo passwd debian
sudo passwd root
```

### SSH (after that you don't need input your password anymore)
```
ssh debian@name.local
ssh-keygen -t dsa
nano ~/.ssh/authorized_keys
```
#### Paste the key from your computer into the beagle (cat .ssh/id_dsa.pub)

### BlackLib (Test code by tfmiranda)
#### Downgrade Kernel
```
git clone https://github.com/beagleboard/bb.org-overlays
cd ./bb.org-overlays
./dtc-overlay.sh
./install.sh
```
#### Download
```
git clone https://github.com/tfmiranda/BlackLib-Modificada
```
#### Commands
```
make
make clean
```
## Commands (Edit the files of the beagle as they were local)
### Mount Folder
```
nautilus sftp://root@name.local
```
