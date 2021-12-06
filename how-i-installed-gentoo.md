# gentoo with systemd stage 3 with UEFI LUKS on LVM

## disk configuration

### partitioning
```
parted /dev/sda 

(parted) print                                                            

(parted) mklabel gpt

(parted) mkpart primary fat32 1MiB 3MiB
(parted) mkpart primary fat32 3MiB 803MiB
(parted) mkpart primary 803MiB -1

(parted) name 1 grub                                                      
(parted) name 2 boot                                                      
(parted) name 3 luks

(parted) set 1 bios_grub on                                               
(parted) set 2 boot on                                                    

(parted) print                                                            
Model: Unknown (unknown)
Disk /dev/sda: 256GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End     Size    File system  Name  Flags
 1      1049kB  3146kB  2097kB  fat32        grub  bios_grub
 2      3146kB  842MB   839MB   fat32        boot  boot, esp
 3      842MB   256GB   255GB                luks
 
(parted) quit
```

### grub and boot filesystems

```
mkfs.vfat /dev/sda1 
mkfs.vfat -F32 /dev/sda2
```

### LUKS volume group

#### physical volume

```
cryptsetup luksFormat -c aes-xts-plain64 -s 512 /dev/sda3 
cryptsetup luksOpen /dev/sda3 lvm
```

#### volume group

```
vgcreate -s 16M carrot-vg /dev/mapper/lvm
```

#### logical volumes

```
lvcreate -L 8G -n swap carrot-vg
lvcreate -l 100%FREE -n root carrot-vg
```

### root filesystem

```
mkfs.ext4 -m1 /dev/carrot-vg/root
mount /dev/carrot-vg/root /mnt/gentoo
```

### swap filesystem

```
mkswap /dev/carrot-vg/swap
swapon /dev/carrot-vg/swap
```

## gentoo installation

### install systemd stage 3

```
cd /mnt/gentoo
links gentoo.org
(navigate to downloads and find the latest systemd stage 3 tarball)
tar xpvf stage3-*.tar.xz --xattrs-include='*.*' --numeric-owner
```

### configure basic compile options for i5-2400

```
vi /mnt/gentoo/etc/portage/make.conf
```

```
/mnt/gentoo/etc/portage/make.conf

COMMON_FLAGS="-march=native -O2 -pipe"
CFLAGS="${COMMON_FLAGS}"
CXXFLAGS="${COMMON_FLAGS}"
FCFLAGS="${COMMON_FLAGS}"
FFLAGS="${COMMON_FLAGS}"

MAKEOPTS="-j5"
GRUB_PLATFORM="efi-64"
L10N="en-US"
USE="X systemd cryptsetup bash-completion samba"
INPUT_DEVICES="libinput"
ACCEPT_LICENSE="* -@EULA"
VIDEO_CARDS="nvidia"
GENTOO_MIRRORS="http://mirror.leaseweb.com/gentoo/ https://mirror.leaseweb.com/gentoo/"
```

### mount and chroot

#### copy DNS config

```
cp --dereference /etc/resolv.conf /mnt/gentoo/etc/
```

#### mount proc, dev, and shm filesystems

```
mount -t proc /proc /mnt/gentoo/proc
mount --rbind /sys /mnt/gentoo/sys
mount --make-rslave /mnt/gentoo/sys
mount --rbind /dev /mnt/gentoo/dev
mount --make-rslave /mnt/gentoo/dev
test -L /dev/shm && rm /dev/shm && mkdir /dev/shm
mount -t tmpfs -o nosuid,nodev,noexec shm /dev/shm
chmod 1777 /dev/shm
```

#### chroot into /mnt/gentoo

```
chroot /mnt/gentoo /bin/bash 
source /etc/profile
export PS1="(chroot) $PS1"
```

#### mount the boot partition

```
mount /dev/sda2 /boot
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
echo America/New_York > /etc/timezone
emerge --config sys-libs/timezone-data
```

### locales

```
vi /etc/locale.gen
(add en_US.UTF-8 UTF-8)
locale-gen
eselect locale list
(select C.UTF8)
eselect locale set <locale number>
env-update && source /etc/profile && export PS1="(chroot) $PS1"
```

## update world

```
mkdir -p /etc/portage/package.{accept_keywords,license,mask,unmask,use}
time emerge -avuD --with-bdeps=y --newuse @world
```

2021-04-08 build time: 5.05 hours

## install a good text editor

```
emerge -av app-editors/neovim
```

```
eselect editor list
eselect editor set <vim number>
eselect editor list vi
eselect editor set <neovim number>
```

## configure fstab

```
blkid | grep boot >> /etc/fstab
blkid | grep carrot--vg-swap >> /etc/fstab
blkid | grep carrot--vg-root >> /etc/fstab

nvim /etc/fstab

# /etc/fstab: static file system information.
UUID=<boot uuid>	/boot	vfat	noatime	0	1
UUID=<carrot--vg-swap uuid>	none	swap	sw	0	0
UUID=<carrot--vg-root uuid>	/	ext4	defaults,acl	0	1
# tmps
tmpfs	/tmp	tmpfs	defaults,size=4G	0	0
tmpfs	/run	tmpfs	size=100M	0	0
# shm
shm	/dev/shw	tmpfs	nodev,nosuid,noexec	0	0
```

## install and build kernel sources

```
emerge -av sys-kernel/gentoo-sources
emerge -av sys-kernel/genkernel
emerge -av sys-fs/cryptsetup
```

### install firmware (optional)

```
emerge -av sys-kernel/linux-firmware
```

### install intel microcode

```
mkdir -p /etc/portage/package.use
echo "sys-firmware/intel-microcode initramfs" > /etc/portage/package.use/intel-microcode
emerge -av sys-firmware/intel-microcode
```

### configure genkernel.conf

```
cp -p /etc/genkernel.conf /etc/genkernel.conf.default
nvim /etc/genkernel.conf

...
MAKEOPTS="$(portageq envvar MAKEOPTS)"
...
LVM="yes"
...
LUKS="yes"
...
```

### build kernel

```
time genkernel --luks --lvm all
```

2021-04-08 build time: 61 minutes

## install and configure grub

### install

```
mkdir -p /etc/portage/package.use
echo "sys-boot/grub device-mapper" > /etc/portage/package.use/grub
emerge -av sys-boot/grub
grub-install --target=x86_64-efi --efi-directory=/boot
```

### configure

```
cp /etc/default/grub /etc/default/grub.default
blkid | grep crypto_LUKS >> /etc/default/grub
nvim /etc/default/grub

GRUB_CMDLINE_LINUX="init=/usr/lib/systemd/systemd dolvm crypt_root=UUID=<carrot crypto_LUKS uuid> root=/dev/mapper/carrot--vg-root scsi_mod.use_blk_mq=1"
```

```
cd
grub-mkconfig -o /boot/grub/grub.cfg
```
## set root pw

```
passwd
useradd -m -G users,wheel,audio,video,portage,usb,cdrom,plugdev -s /bin/bash choro
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

## Using the live usb to mount and chroot

```
cryptsetup luksOpen /dev/sda3 lvm
mount /dev/carrot-vg/root /mnt/gentoo
mount -t proc /proc /mnt/gentoo/proc
mount --rbind /sys /mnt/gentoo/sys
mount --make-rslave /mnt/gentoo/sys
mount --rbind /dev /mnt/gentoo/dev
mount --make-rslave /mnt/gentoo/dev
mount -t tmpfs -o nosuid,nodev,noexec shm /dev/shm

chroot /mnt/gentoo /bin/bash 
source /etc/profile
export PS1="(chroot) $PS1"

mount /dev/sda2 /boot
```
