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

## Install flatpak and flathub repositories

* To install flatpak applications you must install flatpak first:
```
sudo apt install flatpak -y
```
* Then add the flathub repositories:
```
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
```
* Wait at least 5 min for the driver to build, then reboot
* `sudo reboot`

## Multimedia Codecs

* Install multimedia codecs to stream videos and other media content
```
sudo apt install libavcodec-extra vlc -y
```

## Firewall

* Setting up a firewall on Debian can be done using UFW (Uncomplicated Firewall)
* Set up firewall with:
* `sudo apt install ufw -y`
* `sudo ufw enable`
* `sudo ufw status`

## Swapfile

* If you didn't create a swap partition, you can create a /swapfile, the following example is for adding a 7.5GB /swapfile, recommended for systems with 8GB of RAM:
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
* Modern recommendations vary based on use cases:
* Equal to RAM (1x RAM): common for general-purpose systems, ensuring adequate swap space without overcommitting storage
* Twice RAM (2x RAM): more useful for systems with low RAM (<4GB) or for applications requiring significant swap (e.g., hibernation, heavy multitasking)
* Less than RAM (<1x RAM): often fine for high-RAM systems (16GB+), where swap is rarely needed

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
