# PERLEN Airplay

raspi B+ airplay

## -Shairport

### install on sd-card

> diskutil list

> diskutil unmountDisk /dev/disk2

> sudo dd if=/Users/user/Downloads/raspbian-jessie-lite.img of=/dev/disk2 bs=1m

## -Login

user : pi

Passwort :   raspberry

## -Install

login as root

> sudo su -

update and upgrade :)

> apt-get update && apt-get upgrade

> amixer cset numid=3 1

> aptitude install git libao-dev libssl-dev libcrypt-openssl-rsa-perl libio-socket-inet6-perl libwww-perl avahi-utils

> git clone https://github.com/abrasive/shairport.git

> cd shairport
> make install
> cp shairport.init.sample /etc/init.d/shairport
> cd /etc/init.d
> chmod a+x shairport
> update-rc.d shairport defaults






