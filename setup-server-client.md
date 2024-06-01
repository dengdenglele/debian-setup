- [Install SSH on a fresh Debian system](https://www.cyberciti.biz/faq/how-to-install-ssh-on-ubuntu-linux-using-apt-get/)
- [How to disable ssh password login on Linux to increase security](https://www.cyberciti.biz/faq/how-to-disable-ssh-password-login-on-linux/)
- [How to Fix “SSH Too Many Authentication Failures” Error](https://www.tecmint.com/fix-ssh-too-many-authentication-failures-error/)
- [How to recover from "Too many Authentication Failures for user root"](https://serverfault.com/questions/36291/how-to-recover-from-too-many-authentication-failures-for-user-root)
- [Only for background knowledge: Debian: How To Enable The Root User (Login & SSH)](https://raspberrytips.com/enable-root-debian/)
- [How to Enable and Disable Root User Account in Ubuntu](https://linuxize.com/post/how-to-enable-and-disable-root-user-account-in-ubuntu/)

Disable root account
```bash
$ sudo passwd -l root
```

Verify root account is disabled [(forum discussion)](https://ubuntuforums.org/archive/index.php/t-1884813.html)
```bash
$ sudo passwd -S root
# Expected output: "L" after root, then root is disabled
# Undesired output: if "P" after root, then root is enabled!!!
root L yyyy-mm-dd 99999 7 -1
```
Setup firewall
```bash
$ sudo apt install ufw
$ sudo ufw enable
```
