# [Install Flatpak](https://wiki.debian.org/Flatpak)

```bash
sudo apt install flatpak

# add flathub repo system-wide
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# add flathub repo user-only (recommended for multiple users, but takes up more space)
# must be activated for each user separately
flatpak remote-add --user --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# verify, "Options" column should state system or user
flatpak remotes
```

[More on flatpak options](https://askubuntu.com/questions/1078021/how-do-i-install-a-flatpak-for-a-specific-user)
[Flatpak documentation](https://docs.flatpak.org/en/latest/using-flatpak.html)
