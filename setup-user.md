## adduser

Add an additional user, stick with the defaults, will not have sudo rights:

```bash
sudo adduser username
```

## visudo

```bash
$ sudo visudo

# at the bottom of the sudoers file add following lines to enable non sudo users to update and upgrade system
username ALL = NOPASSWD: /usr/bin/apt update
username ALL = NOPASSWD: /usr/bin/apt upgrade -y

# at the bottom of the sudoers file add following line to enable non sudo users to turn of the system
username ALL = NOPASSWD: /usr/sbin/shutdown now

# commands must be exactly performed as written in sudoers file, e.g.:
$ sudo apt update
$ sudo apt upgrade -y
$ sudo shutdown now
```

## [Create a "guest" account with home directory in /tmp/home/guest](https://www.tutorialspoint.com/how-to-change-the-default-home-directory-of-a-user-on-linux)

Variant 1: Create a new user "guest" with home directory in /tmp/home/guest

```bash
sudo adduser guest --home /tmp/home/guest
```

Variant 2: Change the home directory for an already existing user "guest":

```bash
sudo usermod -d /tmp/home/guest guest

# erase the old home folder of user guest with rm if neccessary
```

Verify the changes:

```bash
grep guest /etc/passwd
```

The "temporary" home directory will be cleared after a reboot of the system.
