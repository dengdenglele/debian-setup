## Check "Software & Updates" App if sources are missing e.g. contrib, non-free ...

Append additional sources the sources.list file

## Use "Settings" App to configure GNOME (deprecated, now using gsettings to set up everything, see next section)
<!---

- Mouse & Touchpad
  - Disable "Natural Scrolling"
  - Enable "Tap to Click"
- Multitasking
  - Disable "Hot Corner"
  - Disable "Active Screen Edges"
  - Set "Fixed number of workspaces" to 4
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
  - Accessibility
    - Super+Alt+/ < "Increase text size"
    - Super+Alt+. < "Decrease text size"
    - Disable all other options, as they might interfere in daily usage
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

-->

## Set up GNOME settings with terminal

```bash
# How to reset any gnome settings back to default value
gsettings reset org.gnome.desktop.input-sources xkb-options
gsettings reset org.gnome.desktop.peripherals.touchpad natural-scroll
gsettings reset org.gnome.desktop.interface show-battery-percentage

# Mouse & Touchpad
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
gsettings set org.gnome.desktop.peripherals.touchpad natural-scroll false
gsettings set org.gnome.desktop.peripherals.mouse accel-profile 'flat'

# Window focus
gsettings set org.gnome.desktop.wm.preferences focus-mode 'sloppy'
gsettings set org.gnome.desktop.wm.preferences focus-mode 'click'
## [Focus "mouse" or "sloppy" do the same thing on gnome-shell](https://unix.stackexchange.com/questions/49428/focus-mouse-or-sloppy-do-the-same-thing-on-gnome-shell)
gsettings set org.gnome.desktop.wm.preferences auto-raise true

# Multitasking
gsettings set org.gnome.mutter dynamic-workspaces false
gsettings set org.gnome.desktop.wm.preferences num-workspaces 3
gsettings set org.gnome.desktop.interface enable-hot-corners false

# Power
gsettings set org.gnome.settings-daemon.plugins.power idle-dim false
gsettings set org.gnome.settings-daemon.plugins.power power-saver-profile-on-low-battery false
gsettings set org.gnome.desktop.session idle-delay 900
gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout 0
gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout 0
gsettings set org.gnome.settings-daemon.plugins.power power-button-action 'nothing'
gsettings set org.gnome.desktop.interface show-battery-percentage 'true'

# Accessibility
gsettings set org.gnome.desktop.interface cursor-size 48
gsettings set org.gnome.desktop.interface text-scaling-factor 1.25
gsettings set org.gnome.desktop.interface locate-pointer true
gsettings set org.gnome.desktop.peripherals.keyboard repeat-interval 15
gsettings set org.gnome.desktop.peripherals.keyboard delay 250
gsettings set org.gnome.desktop.a11y.interface show-status-shapes true # new in Ubuntu 24.04 LTS

# Appearance
gsettings set org.gnome.desktop.interface color-scheme 'prefer-dark'
gsettings set org.gnome.Terminal.Legacy.Settings theme-variant 'dark'
gsettings set org.gnome.desktop.wm.preferences button-layout 'appmenu:minimize,maximize,close'

# Keyboard
gsettings set org.gnome.desktop.input-sources sources "[('xkb', 'us'), ('xkb', 'de')]"
gsettings set org.gnome.desktop.input-sources xkb-options "['caps:ctrl_modifier']"

# Shortcuts
## Window manager
gsettings set org.gnome.desktop.wm.keybindings switch-applications "['<Super>Tab']"
gsettings set org.gnome.desktop.wm.keybindings switch-applications-backward "['<Shift><Super>Tab']"
gsettings set org.gnome.desktop.wm.keybindings switch-windows "['<Alt>Tab']"
gsettings set org.gnome.desktop.wm.keybindings switch-windows-backward "['<Shift><Alt>Tab']"
gsettings set org.gnome.desktop.wm.keybindings show-desktop "['<Super>d']"

## Launchers
gsettings set org.gnome.settings-daemon.plugins.media-keys home "['<Super>e']"
gsettings set org.gnome.settings-daemon.plugins.media-keys calculator "['<Super>c']"
gsettings set org.gnome.settings-daemon.plugins.media-keys email "['<Super>b']"
gsettings set org.gnome.settings-daemon.plugins.media-keys help []
gsettings set org.gnome.settings-daemon.plugins.media-keys www "['<Super>f']"

## Volume
gsettings set org.gnome.settings-daemon.plugins.media-keys volume-down "['<Super><Alt>z']"
gsettings set org.gnome.settings-daemon.plugins.media-keys volume-up "['<Super><Alt>x']"
gsettings set org.gnome.settings-daemon.plugins.media-keys volume-mute "['<Super><Alt>space']"

## Text size
gsettings set org.gnome.settings-daemon.plugins.media-keys decrease-text-size "['<Super><Alt>period']"
gsettings set org.gnome.settings-daemon.plugins.media-keys increase-text-size "['<Super><Alt>slash']"

## Custom shortcut gnome-terminal
gsettings set org.gnome.settings-daemon.plugins.media-keys custom-keybindings "['/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/terminal/']"
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/terminal/ name 'Terminal'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/terminal/ command 'gnome-terminal'
gsettings set org.gnome.settings-daemon.plugins.media-keys.custom-keybinding:/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/terminal/ binding '<Control><Alt>t'


```
  
## gnome-tweaks

Install "gnome-tweaks" to get access to additional GNOME settings not available in "Settings" app

```bash
sudo apt install gnome-tweaks
```

- General > Turn off "Suspend when laptop lid is closed"
- Fonts > Increase "Scaling Factor" if necessary
- Keyboard & Mouse > Set "Acceleration Profile" to "Flat"
- Keyboard & Mouse > In "Additional Layout Options" > "Caps Lock behavior" select "Make Caps Lock an additional Esc, but Shift + Caps Lock is the regular Caps Lock"


## gnome-extensions

Get a list of enabled gnome extensions with gsettings
```bash
gsettings get org.gnome.shell enabled-extensions
```

Activate pre-installed extension "workspace indicator" from gnome-core
```
gnome-extensions enable workspace-indicator@gnome-shell-extensions.gcampax.github.com
```

Extract infos about installed & enabled [GNOME extensions](https://askubuntu.com/questions/1133782/command-to-list-installed-and-enabled-gnome-extensions):
```bash
gnome-extensions list --enabled > ~/installed_enabled_gnome_extensions.md

gnome-extensions list --enabled
```

Exemplary Output:
```
just-perfection-desktop@just-perfection
middleclickclose@paolo.tranquilli.gmail.com
trayIconsReloaded@selfmade.pl
tactile@lundal.io
weeks-start-on-monday@extensions.gnome-shell.fifi.org
drive-menu@gnome-shell-extensions.gcampax.github.com
nightthemeswitcher@romainvigier.fr
date-menu-formatter@marcinjakubowski.github.com
workspace-indicator@gnome-shell-extensions.gcampax.github.com
Vitals@CoreCoding.com
auto-move-windows@gnome-shell-extensions.gcampax.github.com
AlphabeticalAppGrid@stuarthayhurst
display-brightness-ddcutil@themightydeity.github.com
clipboard-indicator@tudmotu.com
ddterm@amezin.github.com
```

### gnome-extension bugs

- forge and ddterm do not work well together

## [Increase width of scrollbars in GTK3 and GTK4 applications](https://www.reddit.com/r/gnome/comments/152equt/change_scrollbar_width_gnome_434_adwaita/)

Create the following files in .config folder:

```bash
touch ~/.config/gtk-3.0/gtk.css
touch ~/.config/gtk-4.0/gtk.css
```

Write the following content into both .css files:

```bash
scrollbar slider {
 padding: 8px;
}
```
