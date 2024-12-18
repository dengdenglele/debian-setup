# [Undervolt Intel Core CPUs up to 9th generation](https://cryptosingh1337.medium.com/how-to-under-volt-intel-i-series-cpu-in-ubuntu-abc9283f4760)
- [Git repository](https://github.com/georgewhewell/undervolt)
- Requires python and pip
- Modern Intel CPUs starting with generation 10th and newer do not have any firmware parameters for undervolting/overclocking
- Read more about the Plundervolt vulnerability [here](https://plundervolt.com/)
- A modest starting point is to set -50 mV for each CPU, CPU cache and iGPU
- Still testing the stability of 8th Gen U-series CPU with CPU and CPU cache set to -100 mV and iGPU set to -50 mV

# [TLP Optimizing Guide](https://linrunner.de/tlp/support/optimizing.html)

```bash
sudo apt install tlp
sudo tlp start

# edit settings in
sudo nano /etc/tlp.conf

# reinstall tlp with default settings
sudo apt remove tlp --purge && sudo apt install tlp

# nice GUI for beginners
flatpak install flathub com.github.d4nj1.tlpui
```
Do not disable 
- "CPU_BOOST_ON_BAT=1" and
- "CPU_HWP_DYN_BOOST_ON_BAT=1",

otherwise Intel CPU (8th gen?) will not get pass 800MHz when 
- "CPU_ENERGY_PERF_POLICY_ON_BAT=balance_power" is set to "balance_power"

[Restoring TLP default settings - how?](https://www.reddit.com/r/linux4noobs/comments/yv1yim/restoring_tlp_default_settings_how/)

# Hardware acceleration
How to activate hardware support for video playback and energy consumption reduction

## Enable hardware acceleration for mpv player
```bash
echo "hwdec=auto" >> ~/.config/mpv/mpv.conf
```
or toggle it with shortcut: `Ctrl` + `h`

show file, video and audio infos: `Shift` + `i`

## Disable unsupported modern codecs on Firefox
Unsupported codecs running on old devices are accelerated via software / CPU only.
This can cause high energy consumption and stuttering video playback with high video resolutions.
YouTube and other sites do not check if modern codecs are supported, so they will not fall back to older hardware-accelerated codecs.

- Install [h264ify](https://addons.mozilla.org/de/firefox/addon/h264ify/) add-on to enforce usage of supported H.264 codec on all YouTube videos
- Disable AV1 support: enter "about:config" in address bar, search for "media.av1.enabled" and set it to false

# Diagnostics

```bash
# Monitoring GPU and usage of hardware acceleration for videos played in Firefox etc
sudo apt install intel-gpu-top
sudo intel_gpu_top

# Monitor CPU frequency, voltage settings and temperatures
sudo apt install i7z
sudo i7z

# Stress test CPU cores after undervolting / overclocking adjustments
sudo apt install stress
## stress test the cpu with 8 threads (e.g. 4 pyhsical cores + 4 virtual cores)
sudo stress --cpu 8

# btop, an even nicer looking htop
sudo apt install btop
```

# Check battery health and set charging thresholds for laptops

```bash
# Check battery health
upower -i /org/freedesktop/UPower/devices/battery_BAT0

# Print out current battery charging threshold
cat /sys/class/power_supply/BAT0/charge_start_threshold
cat /sys/class/power_supply/BAT0/charge_stop_threshold

# Set the charging thresholds to 60/80
echo 60 | sudo tee /sys/class/power_supply/BAT0/charge_start_threshold
echo 80 | sudo tee /sys/class/power_supply/BAT0/charge_stop_threshold
```

# Setup network interfaces in server environment
An example of the contents of the /etc/network/interfaces file:
```bash
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug enp0s31f6
iface enp0s31f6 inet dhcp
```

# Manage Logitech devices on Linux

Logitech Unifying Software for Windows is no longer available for download anymore.
Solaar is an open source alternative with GUI.

```bash
sudo apt install solaar
```

