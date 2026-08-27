# How to set up virtual machines

## Install packages
```
sudo dnf install cloud-utils virt-manager libvirt qemu-kvm
```

## Debian cloud images
- Get the correct image [here](https://cloud.debian.org/images/cloud/)
  - &rarr; generic: Should run in any environment using cloud-init, for e.g. OpenStack, DigitalOcean and also on bare metal.
  - ~~nocloud~~: Does not run cloud-init and boots directly to a root prompt. Useful for local VM instantiation with tools like QEMU.
- Copy the .qcow2 file into desired locations
- Enlarge the disk space
  - ```
    qemu-img resize debian-xxx.qcow2 +20G
    ```


## Create a `user-data` file
- In the following file, no `passwd` is set
- `sudo` can be used directly without `passwd`
- Server is only accessible via `ssh` connection &rarr; check IP

```
hostname: <my-hostname>
users:
  - name: <my-name>
    groups: sudo
    shell: /bin/bash
    lock_passwd: false
    ssh_authorized_keys:
      - <ssh-ed25519 AAAA... your-key-here from .pub file>
    sudo: 'ALL=(ALL) NOPASSWD:ALL'
ssh_pwauth: false
chpasswd:
  expire: false
```

## Create a `meta-data` file (optional)

## Build the seed ISO (contains the cloud-init settings)
```
cloud-localds cloud-init.iso user-data meta-data
```

## Create a Virtual Machine in virt-manager
1. `Create a new virtual machine`
1. `Import existing disk image`
1. Select path to `.qcow2` image and select correct `operating system`
1. Assign `Memory` and `CPU`
1. Assign `Name`, check the box `Customize configuration before install`
1. `Add Hardware` &rarr; `Storage`
1. `Device type` is `CDROM device`
1. `Select or create custom storage` &rarr; use the `cloud-init.iso`
1. `Boot Options` &rarr; check `SATA CDROM 1` and move to top
