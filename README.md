# Null Linux
A GNU/Linux distribution based off precompiled Linux From Scratch.
## About
Null Linux is an independent GNU/Linux distribution aiming to provide complete installs based off Linux From Scratch without the need to compile anything. As such, it has no package manager, no desktop environment, no window manager and no extra packages nor configurations installed, requiring the user to compile any packages they wish to install and configure everything themselves (NOTE: Instructions for compiling a multitude of packages can be found in [Beyond Linux From Scratch](https://www.linuxfromscratch.org/blfs/)).
## Installation
 1. Boot into a GNU/Linux LiveCD of your choice.
 2. Partition your disk using a tool like `fdisk` to create a `/boot` partition of about 200 MB, a root partition of at least 10 GB and a swap partition double the size of your RAM. Suggestions for other partitions can be found [here](https://www.linuxfromscratch.org/lfs/view/stable/chapter02/creatingpartition.html).
 3. Format the root partition , the `/boot` partition and any eventual additional ones with a Linux filesystem like ext4 using `mkfs.ext4 /dev/<xxx>` and format the swap partition with `mkswap /dev/<yyy>`. If a `/boot/efi` partition has been made, it will have to be formatted with `mkfs.vfat /dev/<zzz>`.
 4. Create a directory to mount the root partition with `mkdir -p /mnt/null`, a directory for `/boot` with `mkdir -p /mnt/null/boot` and directories for additional partitions with `mkdir -p /mnt/null/<xxx>`.
 5.  Mount the root partition with `mount /mnt/null /dev/<xxx>`, the `/boot` partition with `mount /mnt/null/boot /dev/<yyy>` and any extra partitions with `mount /mnt/null/<zzz> /dev/<zzz>`.
 6. Change to the root directory of the system with `cd /mnt/null`.
 7. Download the rootfs tarball for Null Linux from the [releases page](https://github.com/MymeType/null-linux/releases) with `wget <LINK TO CURRENT RELEASE TARBALL>`.
 8. Extract the system to the disk from the rootfs tarball using `tar xpf <ROOTFS TARBALL NAME>.tar.xz`.
 9. Mount the virtual kernel filesystems using the following commands:<br>`mount --bind /dev /mnt/null/dev`<br>`mount -t devpts devpts -o gid=5,mode=0620 /mnt/null/dev/pts`<br>`mount -t proc proc /mnt/null/proc`<br>`mount -t sysfs sysfs /mnt/null/sys`<br>`mount -t tmpfs tmpfs /mnt/null/run`
 10. On some GNU/Linux distributions, `/dev/shm` is a mount point for a tmpfs. In that case the mount of `/dev` above will only create `/dev/shm` as a directory in the chroot environment. In this situation you must run the following:<br> `if [ -h /mnt/null/dev/shm ]; then`<br>`install -d -m 1777 /mnt/null$(realpath /dev/shm)`<br>`else`
  `mount -t tmpfs -o nosuid,nodev tmpfs /mnt/null/dev/shm`<br>`fi`
 11. Enter the system using `chroot /mnt/null /bin/bash`.
 12. Replace the password for the root account with a different one using `passwd`.
 13. Edit `/etc/sysconfig`, `/etc/resolv.conf`, `/etc/hostname` and `/etc/hosts` to your liking following the instructions [here](https://www.linuxfromscratch.org/lfs/view/stable/chapter09/network.html). 
 14. edit `/etc/fstab` using the instructions from [here](https://www.linuxfromscratch.org/lfs/view/stable/chapter10/fstab.html).
 15. Install the GRUB bootloader using the instructions [here](https://www.linuxfromscratch.org/lfs/view/stable/chapter10/grub.html).
 16. Optionally remove the rootfs tarball with `rm <ROOTFS TARBALL NAME>.tar.xz` and the /sources directory containing the tarballs for everything installed on the system with `rm -rf /sources`.
 17. Exit the chroot environment with `logout`.
 18. Unmount the system from the LiveCD with the following commands:<br>`cd`<br>`umount /mnt/null/dev/pts`<br>`mountpoint -q /mnt/null/dev/shm && umount /mnt/null/dev/shm`<br>`umount /mnt/null/dev`<br>`umount /mnt/null/run`<br>`umount /mnt/null/proc`<br>`umount /mnt/null/sys`
 19. Unmount any extra partitions with `umount /mnt/null/<xxx>` and then the main root partition with `umount /mnt/null`
 20. Reboot the system into the GRUB bootloader.<br>
 
***Congratulations! Null Linux is now installed on your computer!***<br>
**For more resources on how to compile additional packages, see [Beyond Linux From Scratch](https://www.linuxfromscratch.org/blfs/).**
