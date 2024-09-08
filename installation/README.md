## NixOS Installation

The goal of this is a stable, partially encrpyted and somewhat flexible initial NixOS setup to build upon. In order to include a full description, large parts are not specific to NixOS and can be adopted for other systems as well. The process consists of the following steps:

#### Preparing

Assuming a system capable of USB booting, the following describes how to create a bootable USB flash drive from the terminal.

1. Obtain the minimal installation image from [this](https://nixos.org/download/) download page. It is saved to `path/to/image` in this example.
2. Plug in the flash drive and use the `lsblk` command to identify the correct device by its size. In this example, it is called `sdX` with any partitions being denoted by an additional number.
3. Make sure all partitions are properly unmounted using the `*` wildcard:
```
sudo umount /dev/sdX*
```
4. Then use the `dd` utility to write the image to the boot medium:
```
sudo dd bs=4M conv=fsync oflag=direct status=progress if=path/to/image of=/dev/sdX
```

*To be bootable on BIOS and UEFI devices, the ISO image has to be written verbatim to the USB drive. The `of` and `if` flags replace the default input `stdin` and output `stdout` with the specified files, while `status=progress` shows transfer statistics. Use of `oflag=direct` avoids using RAM as writeback cache, with `conv=fsync` ensuring the file is written fully and without errors before finishing. Reasonable speeds are achieved by setting `bs=4M` for a larger simultaneously accessed block size.*

#### Booting

Assuming a UEFI system, the following describes a UEFI installation process via the terminal.

1. Plug in the flash drive and turn on or restart the computer.
2. Open the boot menu by pressing the appropriate key.
3. Select the correct boot device and proceed with the default installer option.
5. As the `nixos` user has no password, enter the `root` user by typing:
```
sudo -i
```
5. If required, switch the keyboard layout, in this case to german language:
```
loadkeys de-latin1
```
*Available options can be found by searching `/run/current-system/etc/kbd/keymaps/` subdirectories. Both keyboard layout and time zone location also use `configuration.nix` after the initial installation.*

#### Networking

#### Partitioning

##### BOOT (UEFI)
##### SWAP
##### EXT4 (LVM)

#### Encrypting

##### LUKS

#### Installing
