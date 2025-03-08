# Debian 12 Post Install Guide

Things to do after installing Debian 12 (stable)

## Non-free repositories

<ul>
  <li>The default installation of Debian 12 stable from debian.org comes with the free repositories preinstalled</li>
  <li>To add non-free repositories, add <strong>non-free contrib</strong> to each line in <strong>/etc/apt/sources.list</strong></li>
  <li><strong>sudo nano /etc/apt/sources.list</strong></li>
  <li><strong>deb http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware</strong></li>
  <li><strong>deb-src http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware</strong></li>
  <li><strong>deb http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware</strong></li>
  <li><strong>deb-src http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware</strong></li>
  <li><strong>deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware</strong></li>
  <li><strong>deb-src http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware</strong></li>
</ul>

## Install flatpak repositories

<ul>
  <li>To install flatpak applications you must install flatpak first and add the flathub repositories</li>
  <li><strong>sudo install flatpak -y</strong></li>
  <li><strong>flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo</strong></li>
  <li>For Gnome <strong>sudo apt install gnome-software-plugin-flatpak</strong></li>
  <li>For KDE Plasma <strong>sudo apt install plasma-discover-backend-flatpak</strong></li>
  <li><strong>sudo reboot</strong></li>
</ul>

## Remove Firefox ESR and install flatpak Browser

<ul>
  <li><strong>sudo apt remove firefox-esr</strong></li>
  <li>To install Firefox's flatpak use <strong>flatpak install flathub org.mozilla.firefox</strong></li>
  <li>To install Chrome's flatpak use <strong>flatpak install flathub com.google.Chrome</strong></li>
</ul>

## NVIDIA Drivers

<ul>
  <li>If you have an NVIDIA GPU, you can install the drivers with</li>
  <li><strong>sudo apt install nvidia-driver</strong></li>
  <li>sudo reboot</li>
</ul>

## Multimedia Codecs

<ul>
  <li>Install multimedia codecs to stream videos and other media content</li>
  <li><strong>sudo apt install libavcodec-extra vlc</strong></li>
</ul>

## Add swapfile

## Add backport support
