<!--
.. title: tinit - tiny init for microvm
.. slug: tinit-tiny-init-for-microvm
.. date: 2022-12-24 23:22:15 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

tinit, a tiny but valid init for microvm

[Github repo](https://github.com/mofm/tinit)


## What is tinit?
tinit, basic and tiny init for microvm, it's a valid init, but it's not a full init, it's just a simple init, it's not a replacement for systemd, it's just a simple init for microvm.

- It mounts required filesystems.
- It configures the network.
- It configures the hostname.
- It runs the user specified command.

## Compile from source
- You need to install the following packages:
  - `make`
  - `gcc`
  - `git`

- Clone the repository:
```
git clone https://github.com/mofm/tinit.git
```

- You can edit the `Makefile` to change the installation directory or CFLAGS or etc.
- Compile:
```
make
```

