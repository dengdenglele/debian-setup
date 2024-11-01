## Check "Software & Updates" App if sources are missing e.g. contrib, non-free ...

Append additional sources the sources.list file

## Use "Settings" App to configure GNOME

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
   
## Set up GNOME settings with terminal

```bash
gsettings set org.gnome.desktop.interface show-battery-percentage 'true'
gsettings set org.gnome.desktop.interface color-scheme 'prefer-dark'

gsettings set org.gnome.desktop.wm.keybindings switch-applications "['<Super>Tab']"
gsettings set org.gnome.desktop.wm.keybindings switch-windows "['<Alt>Tab']"
```
  
## gnome-tweaks

Install "gnome-tweaks" to get access to additional GNOME settings not available in "Settings" app

```bash
sudo apt install gnome-tweaks
```

- General > Turn off "Suspend when laptop lid is closed"
- Fonts > Increase "Scaling Factor" if necessary
- Keyboard & Mouse > Set "Acceleration Profile" to "Flat".
- Keyboard & Mouse > In "Additional Layout Options" > "Caps Lock behavior" select "Make Caps Lock an additional Esc, but Shift + Caps Lock is the regular Caps Lock"


## gnome-extensions

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
