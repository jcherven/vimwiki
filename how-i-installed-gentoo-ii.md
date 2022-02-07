# gentoo with systemd stage 3 with systemd-boot and dist-kernel

Installation from official Gentoo media.

Use `lsblk` to check disk assignments. `/dev/sda` is used as the root disk here.

## chroot into installed system from liveusb

```
mount /dev/sda3 /mnt/gentoo
mount -t proc /proc /mnt/gentoo/proc
mount --rbind /sys /mnt/gentoo/sys
mount --make-rslave /mnt/gentoo/sys
mount --rbind /dev /mnt/gentoo/dev
mount --make-rslave /mnt/gentoo/dev
mount --bind /run /mnt/gentoo/run
mount --make-slave /mnt/gentoo/run

chroot /mnt/gentoo /bin/bash 
source /etc/profile
export PS1="(chroot) $PS1"

mount /dev/sda1 /boot
```

## disk configuration

### partitioning
```
fdisk /dev/sda 

(print current partition strategy) p
(new GPT) g

# create efi system partition
(new partition) n
(partition number) 1
(start sector) 2048
(end sector) +256M

(filesystem type) t
(partition number) 1
(type) 1

# create swap partition
(new partition) n
(partition number) 2
(start sector) enter for default first sector
(end sector) +8G

(filesystem type) t
(partition number) 2
(type) 19

# create root partition
(new partition) n
(partition number) 3
(start sector) enter for default
(end sector) enter for default (end of disk)

# write changes
w
```

### efi and root filesystems

```
mkfs.vfat -F 32 /dev/sda1 
mkfs.ext4 /dev/sda3
```

### swap filesystem

```
mkswap /dev/sda2
swapon /dev/sda2
```

## gentoo installation

### install systemd stage 3

```
mount /dev/sda3 /mnt/gentoo
cd /mnt/gentoo
links gentoo.org
(navigate to downloads and find the latest systemd stage 3 tarball)
(this installation used the desktop profile systemd tarball)
tar xpvf stage3-*.tar.xz --xattrs-include='*.*' --numeric-owner
```

### configure make.conf

```
mirrorselect -c USA -s3 -b10 -D -o >> /mnt/gentoo/etc/portage/make.conf
```

```
mkdir -p /mnt/gentoo/etc/portage/repos.conf
cp /mnt/gentoo/usr/share/portage/config/repos.conf /mnt/gentoo/etc/portage/repos.conf/gentoo.conf
```

```
vi /mnt/gentoo/etc/portage/make.conf
```

```
/mnt/gentoo/etc/portage/make.conf

...
COMMON_FLAGS="-march=native -O2 -pipe"
CFLAGS="${COMMON_FLAGS}"
CXXFLAGS="${COMMON_FLAGS}"
FCFLAGS="${COMMON_FLAGS}"
FFLAGS="${COMMON_FLAGS}"

MAKEOPTS="-j5"
L10N="en-US"
USE="X systemd dist-kernel bash-completion samba libinput pulseaudio -games"
INPUT_DEVICES="libinput"
ACCEPT_LICENSE="* -@EULA"
VIDEO_CARDS="intel"
...

```

#### copy DNS config

```
cp --dereference /etc/resolv.conf /mnt/gentoo/etc/
```

### mount and chroot

#### mount proc, dev, and run filesystems

```
mount -t proc /proc /mnt/gentoo/proc
mount --rbind /sys /mnt/gentoo/sys
mount --make-rslave /mnt/gentoo/sys
mount --rbind /dev /mnt/gentoo/dev
mount --make-rslave /mnt/gentoo/dev
mount --bind /run /mnt/gentoo/run
mount --make-slave /mnt/gentoo/run
```

#### chroot into /mnt/gentoo

```
chroot /mnt/gentoo /bin/bash 
source /etc/profile
export PS1="(chroot) $PS1"
```

#### mount the boot partition

```
mkdir /boot
mount /dev/sda1 /boot
```

### update gentoo ebuild repository

```
emerge --sync
```

### select profile

```
eselect profile list
(select desktop/systemd)
eselect profile set <profile number>
```

### timezone

```
echo "America/New_York" > /etc/timezone
emerge --config sys-libs/timezone-data
```

### locales

```
nano /etc/locale.gen
(add en_US.UTF-8 UTF-8)
locale-gen
eselect locale list
(find en_US.utf8)
eselect locale set <locale number>
env-update && source /etc/profile && export PS1="(chroot) $PS1"
```

## update world

```
mkdir -p /etc/portage/package.{accept_keywords,license,mask,unmask,use}
time emerge --ask --verbose --update --deep --with-bdeps=y --newuse @world
```

2022-02-06 build time: 1.45 hours

## install a good text editor

```
emerge --ask app-editors/neovim
```

```
eselect editor list
eselect editor set <vim number>
eselect editor list vi
eselect editor set <neovim number>
```

### install firmware (optional)

```
emerge --ask sys-kernel/linux-firmware
```

## install dist-kernel

### install correct installkernel

```
emerge -av sys-kernel/installkernel-systemd-boot
```

### install intel microcode

```
echo "sys-firmware/intel-microcode initramfs" > /etc/portage/package.use/intel-microcode
emerge --ask sys-firmware/intel-microcode
```

### install dist-kernel package
```
emerge -av sys-kernel/gentoo-kernel-bin
```

### clean up kernels provided by profile
```
emerge --depclean
```

## configure systemd-boot

### rebuild systemd with the gnuefi flag

```
echo "sys-apps/systemd gnuefi" >> /etc/portage/package.use/systemd
emerge -uDU @world
```

## set up UEFI boot manager

### Verify that efivarfs is mounted

```
mount -t efivarfs efivarfs /sys/firmware/efi/efivars
```

### Install the boot entry

```
bootctl --path /boot install
```

### fix /boot/efi/loader/entries

```
# get the root partition uuid from blkid
blkid | grep sda1 >> /boot/efi/loader/entries/<os entry>.conf

# change root=/dev/ram0 to:
root=PARTUUID=<partition uuid>

# change init=/initrc to:
init=/lib/systemd/systemd

# don't forget to delete the blkid output that you appended
```

## configure fstab

```
blkid | grep sda >> /etc/fstab

vi /etc/fstab

# /etc/fstab: static file system information.
UUID=<boot uuid>	/boot	vfat	noatime	0	1
UUID=<swap uuid>	none	swap	sw	0	0
UUID=<root uuid>	/	ext4	noatime	0	1
```

## set root pw

```
passwd
useradd -m -G users,wheel,audio,video,portage,usb,cdrom -s /bin/bash choro
passwd choro
```
## install some basic stuff

```
emerge -av app-admin/sudo app-misc/tmux dev-vcs/git
```

## reboot system

```
exit
shutdown -r now
```

# first run

## networking

```
systemd-machine-id-setup
hostnamectl set-hostname <hostname>
timedatectl set-timezone America/New_York
env-update && source /etc/profile
```

```
/etc/systemd/network/50-dhcp.network
[Match]
Name=en*

[Network]
DHCP=yes
```

```
systemctl enable --now systemd-networkd
systemctl enable --now systemd-resolved
```

```
systemctl daemon-reexec
```

## basic environment software

* Install sudo
	* uncomment wheel permissions with visudo
* install git
* install pip
* pull dotfiles and make symlinks
* install xorg-server and DE
* configure SSH

