# background

- [Cursor keys belong at the center of your keyboard, DEPRECATED due to Xorg](https://tonsky.me/blog/cursor-keys/)
- TL;DR Remap CapsLock + IJKL to act as cursor keys and teach yourself to use it

# setup 60% keyboard

- [install keyd (wayland) from source](https://github.com/rvaiya/keyd)
- [use the "sample config" for capslock=overload(symbols, esc)](https://github.com/rvaiya/keyd)
- [remap j, k, l, i to left, down, right, up. EXAMPLE](https://foosel.net/til/how-to-remap-keys-under-linux-and-wayland/)
- my config file can be found in directory "keyd_config_file"

## setup virtual keyboard mouse with keyd
- Enable "Mouse Keys" in "GNOME Settings" > "Accessibility" > "Pointing & Clicking"
- [Use gsettings to change the speed parameters keys.](https://askubuntu.com/questions/195000/mouse-arrow-moving-slowly-using-keyboard-keys/1234995#1234995)
- my parameters:

    ``` bash
    # print out current settings:
    $ gsettings list-recursively | grep keyboard | grep mouse

    # output:
    org.gnome.desktop.a11y.keyboard mousekeys-accel-time 1500
    org.gnome.desktop.a11y.keyboard mousekeys-enable true
    org.gnome.desktop.a11y.keyboard mousekeys-init-delay 10
    org.gnome.desktop.a11y.keyboard mousekeys-max-speed 3000

    
    # set these parameters:
    gsettings set org.gnome.desktop.a11y.keyboard mousekeys-accel-time 1500
    gsettings set org.gnome.desktop.a11y.keyboard mousekeys-enable true
    gsettings set org.gnome.desktop.a11y.keyboard mousekeys-init-delay 10
    gsettings set org.gnome.desktop.a11y.keyboard mousekeys-max-speed 3000
    ```



    
