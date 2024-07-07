# Null Linux
A GNU/Linux distribution based off precompiled Linux From Scratch.
## About
Null Linux is an independent GNU/Linux distribution aiming to provide complete installs based off Linux From Scratch without the need to compile anything. As such, it has no package manager, no desktop enviroment, no window manager and no extra packages nor configurations installed, requiring the user to compile any packages they wish to install and configure everything themselves (NOTE: Instructions for compiling a multitude of packages can be found in [Beyond Linux From Scratch](https://www.linuxfromscratch.org/blfs/)).
## Installation
 1. Boot into a GNU/Linux LiveCD of your choice.
 2. Log in as root with `sudo su` in a terminal window.
 3. Partition your disk using a tool like `fdisk` to create a `/boot` partition of about 200 MB, a root partition of at least 10 GB and a swap partition double the size of your RAM. Suggestions for other partitions can be found [here](https://www.linuxfromscratch.org/lfs/view/stable/chapter02/creatingpartition.html).
 4. Format the root partition , the `/boot` partition and any eventual additional ones with a Linux filesystem like ext4 using `mkfs.ext4 /dev/<xxx>` and format the swap partition with `mkswap /dev/<yyy>`. If a `/boot/efi` partition has been made, it will have to be formatted with `mkfs.vfat /dev/<zzz>`.
 5. Create a directory to mount the root partition with `mkdir -p /mnt/null`, a directory for `/boot` with `mkdir -p /mnt/null/boot` and directories for additional partitions with `mkdir -p /mnt/null/<xxx>`.
 6.  Mount the root partition
