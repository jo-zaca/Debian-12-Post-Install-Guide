# Debian 12 Post Install Guide

Things to do after installing Debian 12

## Non-free repositories

* The default installation of Debian 12 stable from debian.org comes with the free repositories preinstalled
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

## Install flatpak repositories

* To install flatpak applications you must install flatpak first and add the flathub repositories
* `sudo apt install flatpak -y`
* `flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo`
* For Gnome `sudo apt install gnome-software-plugin-flatpak`
* For KDE Plasma `sudo apt install plasma-discover-backend-flatpak`
* `sudo reboot`

## Remove Firefox ESR and install flatpak Browser

* The default version of Firefox in Debian 12 is Firefox ESR (Extended Support Release), which may be behind most updates, you can remove and install your favorite browser with:
* `sudo apt remove firefox-esr`
* To install Firefox's flatpak use `flatpak install flathub org.mozilla.firefox`
* To install Chrome's flatpak use `flatpak install flathub com.google.Chrome`

## NVIDIA Drivers

* If you have an NVIDIA GPU, you can install the drivers with
* `sudo apt install nvidia-driver`
* `sudo reboot`

## Multimedia Codecs

* Install multimedia codecs to stream videos and other media content
* `sudo apt install libavcodec-extra vlc`

## Add swapfile

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

## Add backport support
