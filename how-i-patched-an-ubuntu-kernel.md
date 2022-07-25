# how i patched an ubuntu kernel

instructions for ubuntu 20.04 lts (kernel 5.4)

## prerequisites

```sh
sudo apt install -y build-dep linux linux-image-$(uname -r)
sudo apt install -y libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf
```

in `/etc/apt/sources.list` add:
```
deb-src http://us.archive.ubuntu.com/ubuntu focal main
deb-src http://us.archive.ubuntu.com/ubuntu focal-updates main
```

## obtain the source for the current ubuntu release

as a non-root user:

```sh
mkdir ~/build && cd ~/build
git clone <necessary patches>
apt source linux-image-unsigned-$(uname -r)

# on debian, you might have to extract the tarball yourself with:
tar -xvf linux-*.tar.whatever

```


## patching

```sh
cd linux-<version that was obtained earlier>

patch -p1 < /path/to/filename.patch
```

## configuring and building

copy the generic config from the current installation. in the kernel source root folder:

```sh
cp /boot/config-<tab complete kernel version> .config
```

edit this config file to comment out this line:

```sh
CONFIG_SYSTEM_TRUSTED_KEYS=y
```

update the config for the new kernel:

```sh
make oldconfig
```

build the kernel:

```sh
make -j7 deb-pkg LOCALVERSION=-customkernel
```

## install the new kernel

the new kernel's deb packages will be in the parent folder of the linux source root.

```sh
cd ..
dpkg -i *.deb
```

## reboot and test

```sh
uname -a
```
