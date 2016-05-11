# PERLEN Airplay


**airplay**  on  **raspi B+**  with  **USB-Soundkarte**



## 1. install on sd-card 

rename FILE `raspbian-jessie-lite.img`

[RASPBIAN JESSIE LITE](https://www.raspberrypi.org/downloads/raspbian/)

Open Terminal

`diskutil list`

`diskutil unmountDisk /dev/disk2`

`sudo dd if=/Users/user/Downloads/raspbian-jessie-lite.img of=/dev/disk2 bs=1m`

## 2. Login

user : pi

Passwort : raspberry

## 3. Install

login as root

`sudo su -`

update and upgrade :)

`apt-get update && apt-get upgrade`

Analog Klinke 

`amixer cset numid=3 1`

Debian/Raspbian users can get the basics with 

`aptitude install git libao-dev libssl-dev libcrypt-openssl-rsa-perl libio-socket-inet6-perl libwww-perl avahi-utils`

Clone from github repository

`git clone https://github.com/abrasive/shairport.git`

`cd shairport `
    
`make install `    

`cp shairport.init.sample /etc/init.d/shairport `    

`cd /etc/init.d `    

`chmod a+x shairport `    

`update-rc.d shairport defaults`    

## 4. Edit rooms

`nano /etc/init.d/shairport`

`DAEMON_ARGS=”-w $PIDFILE -a Room-7 -p <passwort>”`

## 5. Start Shairport

`service shairport start`

## 6. USB-Soundcard Config

``nano /etc/modprobe.d/alsa-base.conf``

```ssh
# autoloader aliases
install sound-slot-0 /sbin/modprobe snd-card-0
install sound-slot-1 /sbin/modprobe snd-card-1
install sound-slot-2 /sbin/modprobe snd-card-2
install sound-slot-3 /sbin/modprobe snd-card-3
install sound-slot-4 /sbin/modprobe snd-card-4
install sound-slot-5 /sbin/modprobe snd-card-5
install sound-slot-6 /sbin/modprobe snd-card-6
install sound-slot-7 /sbin/modprobe snd-card-7
# Cause optional modules to be loaded above generic modules
install snd /sbin/modprobe --ignore-install \
  snd && { /sbin/modprobe --quiet snd-ioctl32 ;\
  /sbin/modprobe --quiet snd-seq ; : ; }
install snd-rawmidi /sbin/modprobe --ignore-install \
  snd-rawmidi && { /sbin/modprobe --quiet \
  snd-seq-midi ; : ; }
install snd-emu10k1 /sbin/modprobe --ignore-install \
  snd-emu10k1 && { /sbin/modprobe --quiet \
  snd-emu10k1-synth ; : ; }
# Keep snd-pcsp from beeing loaded as first soundcard
options snd-pcsp index=-2
# Keep snd-usb-audio from beeing loaded as first soundcard
options snd-usb-audio index=0
# Prevent abnormal drivers from grabbing index 0
options bt87x index=-2
options cx88_alsa index=-2
options snd-atiixp-modem index=-2
options snd-intel8x0m index=-2
options snd-via82xx-modem index=-2
```

Download Install  *debian-edu-config* it take 15-30min to install
   
`aptitude install debian-edu-config`

edit file ***asound.conf***

`nano /etc/asound.conf`

```ruby
pcm.!default {
    type hw
    card 1
    device 0
    }
```

Edit start Modul ***snd-usb-audio***

```ruby
# /etc/modules: kernel modules to load at boot time.
#
# This file contains the names of kernel modules that should be loaded
# at boot time, one per line. Lines beginning with "#" are ignored.
# Parameters can be specified after the module name.

#snd-bcm2835
snd-usb-audio
```
Modul ***snd-usb-audio*** einige Log-file

`options snd-usb-audio nrpacks=1`

***And now Reboot***

`reboot`

## Troubleshooting

``./shairport --buffer=300``
