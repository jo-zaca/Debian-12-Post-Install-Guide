# Debian 12 Post Install Guide

Things to do after installing Debian 12

## Non-free repositories

* The default installation of Debian 12 stable from https://www.debian.org/ comes with free repositories
* To add non-free repositories, add `non-free contrib` to each line in `/etc/apt/sources.list`
* `sudo nano /etc/apt/sources.list`
```
deb http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware

deb http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
deb-src http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware
```
* `sudo apt update && sudo apt upgrade`

## Install flatpak repositories

* To install flatpak applications you must install flatpak first and add the flathub repositories
```
sudo apt install flatpak -y
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
* For Gnome:
```
sudo apt install gnome-software-plugin-flatpak -y
```
* For KDE Plasma:
```
sudo apt install plasma-discover-backend-flatpak -y
```
* `sudo reboot`

## Remove Firefox ESR and install flatpak Browser

* The default version of Firefox in Debian 12 is Firefox ESR (Extended Support Release), which may be behind most updates, you can remove and install your favorite browser with:
```
sudo apt remove firefox-esr
```
* To install Mozilla Firefox's flatpak:
```
flatpak install flathub org.mozilla.firefox
```
* To install Google Chrome's flatpak:
```
flatpak install flathub com.google.Chrome
```

## NVIDIA Drivers

* If you have an NVIDIA GPU, you can install the drivers with
```
sudo apt install nvidia-driver -y
sudo reboot
```

## Multimedia Codecs

* Install multimedia codecs to stream videos and other media content
```
sudo apt install libavcodec-extra vlc -y
```

## Swapfile

* If you didn't create a swap partition, you can create a /swapfile, the following is for a 7.5GB /swapfile, is always recommended to use the same as your RAM
```
free -h
sudo swapon --show

sudo dd if=/dev/zero of=/swapfile bs=1M count=7680
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo bash -c 'echo "/swapfile swap swap defaults 0 0" >> /etc/fstab'

free -h
sudo swapon --show
```

## Backport support

* If you want to use backport packages, add the following lines at the end of `/etc/apt/sources.list`
* `sudo apt nano /etc/apt/sources.list`
```
# bookworm-backport
deb http://deb.debian.org/debian bookworm-backports main contrib non-free
deb-src http://deb.debian.org/debian bookworm-backports main contrib non-free
```
* `sudo apt update && sudo apt upgrade`

## Switch to Debian 12 Testing branch

* If you want to use the Debian 12 testing branch, replace `bookworm` with `testing` in `/etc/apt/sources.list`
* `sudo nano /etc/apt/sources.list`
```
deb http://deb.debian.org/debian/ testing main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ testing main contrib non-free non-free-firmware

deb http://security.debian.org/debian-security testing-security main contrib non-free non-free-firmware
deb-src http://security.debian.org/debian-security testing-security main contrib non-free non-free-firmware

deb http://deb.debian.org/debian/ testing-updates main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ testing-updates main contrib non-free non-free-firmware
```
* `sudo apt update && sudo apt upgrade`
* Same if you use backports:
```
# testing-backport
deb http://deb.debian.org/debian testing-backports main contrib non-free
deb-src http://deb.debian.org/debian testing-backports main contrib non-free
```
* `sudo apt update && sudo apt upgrade`
