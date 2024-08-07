# [Installing ufw and SSH on Debian-based distros](https://www.cyberciti.biz/faq/how-to-install-ssh-on-ubuntu-linux-using-apt-get/)

Set up firewall (ufw) on both client and server:
```bash
sudo apt update
sudo apt upgrade
sudo apt install ufw

# allow port 22, otherwise SSH does not work
sudo ufw allow ssh

# check if open port 22 rule was successfully added
sudo ufw show added

# activate firewall, if and only if port 22 rule was allowed in previous command
sudo ufw enable

# check again if port 22 is open AND firewall is enabled
sudo ufw status
```

Set up client software:
```bash
sudo apt install openssh-client
```

Set up server software:
```bash
sudo apt install openssh-server
sudo systemctl enable ssh
```

**Background:** When ufw is setup without allowing SSH aka port 22 to be open, the "ssh user@ip-address" command will not work. A message such as "ssh: connect to host 192.123.456.789 port 22: Connection timed out" will be returned after a while.

When a VPN service such as Mullvad VPN is running on the server, SSH connection from a client will fail. A message such as "ssh: connect to host 192.123.456.789 port 22: Connection timed out" will be returned after a while.

More about ssh and port 22 [here](https://www.cyberciti.biz/faq/ufw-allow-incoming-ssh-connections-from-a-specific-ip-address-subnet-on-ubuntu-debian/) and [here](https://www.cherryservers.com/blog/how-to-configure-ubuntu-firewall-with-ufw)

# [Log in to the SSH server and set up pubkey](https://www.cyberciti.biz/faq/how-to-disable-ssh-password-login-on-linux/)

How to Fix “Too many authentication failures” Error / override pubkey identification / force password usage:
```bash
# if following command fails due to "Too many authentication failures"
ssh username@IpAddressOfServer

# force ssh to use password instead (=disable pubkey authentication)
ssh username@IpAdressOfServer -o PubkeyAuthentication=no
```

Set up pubkey on ssh server despite "Too many authentication failures" error:
```bash
# if following command fails
ssh-copy-id -i /client/path/to/keyFile.pub username@IpAddressOfServer

# use the command again with additional parameters to enforce password authentication
ssh-copy-id -i /client/path/to/keyFile.pub -o PubkeyAuthentication=no username@IpAddressOfServer

# keep the syntax, otherwise the pubkey copy process will fail
ssh-copy-id [-f] [-n] [-i identity file] [-p port] [-o ssh_option] [user@]hostname
```

**Background:** Ssh client machine will try out all available private keys stored in .ssh folder to get access to ssh server. When all of them fail (for example more than 30 private keys were used) and the server only accepts a given amount of attempts (e.g. max 3 attempts), the server will return "Too many authentication failures" and close the connection immediately. If this happens, the ssh client will also be unable to use password login.

- [Understanding ssh-copy-id command-line options](https://www.ssh.com/academy/ssh/copy-id)
- [How to Fix “SSH Too Many Authentication Failures” Error](https://www.tecmint.com/fix-ssh-too-many-authentication-failures-error/)
- [How to recover from "Too many Authentication Failures for user root"](https://serverfault.com/questions/36291/how-to-recover-from-too-many-authentication-failures-for-user-root)

# [How to disable ssh password login on Linux to increase security](https://www.cyberciti.biz/faq/how-to-disable-ssh-password-login-on-linux/)

Prerequisites:
- A user account with sudo rights is available on the ssh server
- Access to the SSH server is already set up correctly with pubkey authentication enabled

Disable password authentication:
```bash
# check if following line is present in sshd_config file
grep "Include /etc/ssh/sshd_config.d/\*.conf" /etc/ssh/sshd_config

# create a new file to disable password login/enforce pubkey authentication
sudo nano /etc/ssh/sshd_config.d/disable_root_login.conf

# copy the following lines into /etc/ssh/sshd_config.d/disable_root_login.conf and save it
## rename disable_root_login.conf to disable pubkey authentication / enable password authentcation
## delete the .conf file extension is sufficient
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
PermitRootLogin no

# reload or restart the ssh server
sudo systemctl reload ssh
```

Verify settings:
```bash
# try to log in as root
ssh root@ipAdressOfServer

# try to log in with password only
ssh userNameOnServer@ipAdressOfServer -o PubkeyAuthentication=no

# verify all settings at once on ssh server
sudo sshd -T | grep -E -i 'ChallengeResponseAuthentication|PasswordAuthentication|UsePAM|PermitRootLogin'
```

- [A note about troubleshooting issues](https://www.cyberciti.biz/faq/how-to-disable-ssh-password-login-on-linux/)
- [More on hardening SSH Server](https://download.asperasoft.com/download/docs/client/3.5.2/client_admin_linux/webhelp/dita/ssh_server.html)
- [Top 20 OpenSSH Server Best Security Practices](https://www.cyberciti.biz/tips/linux-unix-bsd-openssh-server-best-practices.html)

# Root account on SSH Server

Disable root account:
```bash
$ sudo passwd -l root
```

Verify root account is disabled [(forum discussion)](https://ubuntuforums.org/archive/index.php/t-1884813.html):
```bash
$ sudo passwd -S root
# Expected output: "L" after root, then root is disabled
# Undesired output: if "P" after root, then root is enabled!!!
root L yyyy-mm-dd 99999 7 -1
```

- [How to Enable and Disable Root User Account in Ubuntu](https://linuxize.com/post/how-to-enable-and-disable-root-user-account-in-ubuntu/)
- *Only for background knowledge*: [Debian: How To Enable The Root User (Login & SSH)](https://raspberrytips.com/enable-root-debian/)
