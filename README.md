# debian-setup
How to setup a minimal debian installation without bloat



## Setup [SourcesList](https://wiki.debian.org/SourcesList#Example_sources.list)
Edit the sources.list file:

```bash
sudo nano /etc/apt/sources.list
```

add the following lines:

```bash
deb http://deb.debian.org/debian bookworm main non-free-firmware
deb-src http://deb.debian.org/debian bookworm main non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security main non-free-firmware
deb-src http://deb.debian.org/debian-security/ bookworm-security main non-free-firmware

deb http://deb.debian.org/debian bookworm-updates main non-free-firmware
deb-src http://deb.debian.org/debian bookworm-updates main non-free-firmware
```

## Install [GNOME minimal](https://wiki.debian.org/Gnome) version

```bash
sudo apt install gnome-core
```

## Remove unnecessary packages

```bash
sudo apt remove yelp totem gnome-software -y
```

