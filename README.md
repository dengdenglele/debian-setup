# Debian minimal setup

How to setup a minimal debian installation without bloat

# During graphical installation process

- Skip network configuration
- "No" to everything
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
# GNOME Desktop environment

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

## Remove unnecessary packages

```bash
sudo apt remove yelp totem gnome-software gnome-characters gnome-contacts firefox-esr -y
```

## Check "Software & Updates" App if sources are missing e.g. contrib, non-free ...

Append additional sources the sources.list file

## Use "Settings" App to configure GNOME

- Mouse & Touchpad
  - Disable "Natural Scrolling"
  - Enable "Tap to Click"
- Power
  - Turn of "Automatic Suspend"
  - Set "Power Button Behavior" to "Nothing"
  - Enable "Show Battery Percentage"
- Date & Time
  - Select correct "Time Zone"
  - Check if "Automatic Date & Time" is available and enabled
- Accessibility
  - Enable "Large Text"
  - Increase "Cursor Size" e.g. "Large"
  - In "Repeat Keys": decrease "Delay", increase "Speed"
  - Enable "Locate Pointer" (not visible/weak effect, when "Enable animations" is disabled)
- Keyboard
  - Launcher
    - Super+E < "Home folder"
    - Super+C < "Launch calculator"
    - Super+B < "Launch email client"
    - Disabled < "Launch help browser"
    - Super+F < "Launch web browser"
  - Navigation
    - Super+D < "Hide all normal windows"
    - Super+Tab < "Switch applications"
    - Alt+Tab < "Switch windows"
  - Custom Shortcuts
    - Ctrl+Alt+T < gnome-terminal

## More advanced stuff

### grub

Remove os-prober, if Windows shall be hidden from grub menu

```bash
sudo apt remove os-prober
```

Add custom background to grub menu

```bash
sudo cp /path/of/picture /boot/grub
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


Always update grub settings and make them active

```bash
sudo update-grub
```

### visudo

### adduser

### [Undervolt Intel Core CPUs until 9th Generation](https://cryptosingh1337.medium.com/how-to-under-volt-intel-i-series-cpu-in-ubuntu-abc9283f4760)

### [TLP Optimizing Guide](https://linrunner.de/tlp/support/optimizing.html)

```bash
sudo apt install tlp
sudo tlp start

# edit settings in
sudo nano /etc/tlp.conf

# nice GUI for beginners
flatpak install flathub com.github.d4nj1.tlpui
```

### gnome-tweaks

Install "gnome-tweaks" to get access to additional GNOME settings not available in "Settings" app

```bash
sudo apt install gnome-tweaks
```

- General > Turn off "Suspend when laptop lid is closed"
- Fonts > Increase "Scaling Factor" if necessary
- Keyboard & Mouse > Set "Acceleration Profile" to "Flat".
- Keyboard & Mouse > In "Additional Layout Options" > "Caps Lock behavior" select "Make Caps Lock an additional Esc, but Shift + Caps Lock is the regular Caps Lock"
