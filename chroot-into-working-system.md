### unlock luks volume

```
cryptsetup luksOpen /dev/sda3 luks
```

### Mount installed gentoo root

```
mount /dev/carrot-vg/root /mnt/gentoo
cd /mnt/gentoo
```

### mount installed system dirs

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

### chroot into the mounted system

```
chroot /mnt/gentoo /bin/bash 
source /etc/profile
export PS1="(chroot) $PS1"
mount /dev/sda1 /boot
```

### /etc/portage/make.conf

```
CHOST="x86_64-pc-linux-gnu"
COMMON_FLAGS="-march=sandybridge -O2 -pipe"

MAKEOPTS="-j5"
GRUB_PLATFORM="efi-64"
USE="X systemd gtk gnome -qt5 -kde -plasma xft networkmanager dhclient pulseaudio bash-completion samba"
ACCEPT_LICENSE="* -@EULA"
VIDEO_CARDS="nvidia intel"
GENTOO_MIRRORS="http://mirror.leaseweb.com/gentoo/ https://mirror.leaseweb.com/gentoo/"
```

### gentoo-style prompt with git-prompt
```
source $GITPROMPT
export GIT_PS1_SHOWDIRTYSTATE=1
PROMPT_COMMAND='__git_ps1 "$NORMALGREEN\u $BRIGHTBLUE\w$BRIGHTMAGENTA" " $RESETCOLOR\\\$ "'
```
