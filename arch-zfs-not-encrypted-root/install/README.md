### How to Use

Boot latest archiso

```bash
$ loadkeys us

# Init ZFS module and install git
$ curl -s https://raw.githubusercontent.com/eoli3n/archiso-zfs/master/init | bash
$ git clone --recursive https://github.com/SuperGaleb/arch-zfs.git
$ cd arch-zfs/arch-zfs-not-encrypted-root/install
$ chmod +x 01-configure.sh
$ chmod +x 02-install.sh
$ ./01-configure.sh
$ ./02-install.sh

When asked enter root and user password do it very carefully (slowly), script will NOT warn you if passwords did not match and it will keep going till end.
System will not boot after install.
I choose password 123 for root and for user, once system is up, running and "happy please change both to your liking. 
```

### DualBoot Support

After installing Void Linux with [void-config](https://github.com/eoli3n/void-config/tree/master/scripts/install), run ``01-configure.sh`` and select ``dualboot`` in the menu.

### EFI install

- sda1  
  /efi  
  FAT used as esp
- sda2  
  ZFS pool

``01-configure.sh`` will 
- Create partition scheme
- Format everything
- Mount partitions

``02-install.sh`` will
- Configure mirrors
- Install Arch Linux and kernel
- Generate initramfs
- Configure hostname, locales, keymap, network
- Install and configure bootloader
- Generate users and passwords

### Debug

```bash
$ ./01-configure.sh debug
$ ./02-install.sh debug
$ pacman -S pastebinit
$ pastebinit -b sprunge.us configure.log
$ pastebinit -b sprunge.us install.log
```

##### Check EFI content
```bash
$ pacman -S dracut
$ lsinitrd /efi/EFI/ZBM/*
```
