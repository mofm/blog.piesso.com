<!--
.. title: meta-econ - openembedded/yocto layer
.. slug: meta-econ-openembeddedyocto-layer
.. date: 2022-12-24 23:08:50 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

meta-econ, OpenEmbedded/Yocto layer for minimal systemd-nspawn containers. (E-Con Linux Distribution)

[Github repo](https://github.com/mofm/meta-econ)


# e-Con Linux Distribution

e-Con Linux is an embedded Linux Distribution optimized for systemd-nspawn containers. It is built on OpenEmbedded. This distribution is focus on minimal and slim container image.

There are two different core image:

- e-Con Tiny Core Image
- e-Con Core Image

## e-Con Tiny Core Image

e-Con Tiny Core Image is really so tiny. It's built with musl and busybox. It works successfully with systemd-nspawn. Tested!
*(Recommended)*

e-Con Tiny Core Image packages:

````
base-files
busybox
busybox-inittab
init-ifupdown
libattr1
musl
netbase
os-release
packagegroup-core-boot
shadow-base
shadow-securetty
util-linux-sulogin
````

compressed rootfs size: ~660 KB :)
uncompressed rootfs size: ~1.2 MB

## e-Con Core Image

e-Con Core Image size is larger than e-Con Tiny Core. It is built with glibc and systemd. Natively, actually systemd-nspawn only supports systemd. So it is built with systemd.

e-Con Core Image packages:

````
base-files
busybox
dbus-1
dbus-common
dbus-tools
kmod
libacl1
libattr1
libblkid1
libc6
libcap
libcrypt2
libdbus-1-3
libexpat1
libkmod2
liblzma5
libmount1
libnss-myhostname2
libsystemd0
libz1
netbase
os-release
packagegroup-core-boot
shadow-base
shadow-securetty
systemd
systemd-compat-units
systemd-serialgetty
systemd-udev-rules
systemd-vconsole-setup
udev
util-linux-agetty
util-linux-fsck
util-linux-mount
util-linux-sulogin
util-linux-umount
volatile-binds
````

But even so its compressed rootfs size: 4.9 MB
uncompressed size: ~17MB

