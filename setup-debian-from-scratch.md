# Debian minimal setup

How to setup a minimal debian installation without bloat

# During graphical installation process

- [Follow this guide to setup full disk encryption in combination with dual boot Windows 10/11](https://blog.cyberethical.me/dual-boot-windows-11-encrypted-kali)
- Skip network configuration
- Select "No" for any questions asked
- Do not install anything additionally

# [TTY environment](https://askubuntu.com/questions/66195/what-is-a-tty-and-how-do-i-access-a-tty)

Not much to see, only darkness. And a command line.

## [Configure a Device Dynamically with DHCP](https://www.cyberciti.biz/faq/howto-configuring-network-interface-cards-on-debian/)

Get the name of your network interface and write down its name:

```bash
ip address
```

Open the /etc/network/interfaces file as the root user:

```bash
sudo nano /etc/network/interfaces
```

Add the following lines to /etc/network/interfaces , replace \<networkInterface\> with respective name, save the file:

```bash
auto <networkInterface>
iface <networkInterface> inet dhcp
```

Start the interface:

```bash
ifup <networkInterface>
```

## [Setup apt SourcesList](https://wiki.debian.org/SourcesList#Example_sources.list)

Edit the sources.list file:

```bash
sudo nano /etc/apt/sources.list
```
Add the following lines:

```bash
deb http://deb.debian.org/debian bookworm main non-free-firmware
deb http://deb.debian.org/debian-security/ bookworm-security main non-free-firmware
deb http://deb.debian.org/debian bookworm-updates main non-free-firmware
```

Update and upgrade packages:

```bash
sudo apt update && sudo apt upgrade -y
```

## [Install GNOME core (minimal setup)](https://wiki.debian.org/Gnome)

```bash
sudo apt install gnome-core
sudo reboot
```
# Enter GNOME Desktop environment

Now it's getting colorful

## [Remove interfaces file and let GNOME handle network settings](https://www.reddit.com/r/debian/comments/162gpdg/debian_12_minimal_install_no_network_card_in_gnome/)

```bash
sudo rm /etc/network/interfaces
sudo reboot
```

## [Fix missing time synchronization service](https://manpages.debian.org/unstable/systemd-timesyncd/systemd-timesyncd.service.8.en.html)

```bash
sudo apt install systemd-timesyncd
```

## [Fix incorrect time in Windows when using dual-boot](https://itsfoss.com/wrong-time-dual-boot/)

```bash
timedatectl set-local-rtc 1
```

## Remove unnecessary packages

```bash
sudo apt remove yelp totem gnome-software gnome-characters gnome-contacts firefox-esr -y
```


## Check Debian version

```bash
cat /etc/debian_version
```

## [How to Set or Change Hostname in Linux](https://linuxize.com/post/how-to-change-hostname-in-linux/)

```bash
# check current hostname
echo $HOSTNAME
hostnamectl
# change hostname
sudo hostnamectl set-hostname newHostname
```

## Customize boot manager menu of GRUB

Remove os-prober, if Windows shall be hidden from grub menu

```bash
sudo apt remove os-prober
```

Add custom background to grub boot manager menu

```bash
sudo cp /path/to/picture /boot/grub
```

Customize grub file

```bash
sudo nano /etc/default/grub
```

Make the boot process look nice with following line in /etc/default/grub

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
# "quiet" lets all command line text between "grub menu" and "decrytion prompt" disappear.
# "splash" makes the decryption prompt look nice.
```

Always update grub settings and make them active:

```bash
sudo update-grub
```
