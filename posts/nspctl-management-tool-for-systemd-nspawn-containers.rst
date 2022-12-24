.. title: nspctl for systemd-nspawn containers
.. slug: nspctl-management-tool-for-systemd-nspawn-containers
.. date: 2022-12-24 23:04:28 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

nspctl, management tool for systemd-nspawn containers.

`Github repo <https://github.com/mofm/nspctl>`_


Why nspctl?
###########

There are different tools for systemd-nspawn containers. You can use native tools ('machinectl' command) to manage for containers.
But systemd-nspawn, machinectl or other tools do not support non-systemd containers.
(non-systemd containers: containers with another init system from systemd. Such as systemv, openrc, upstart, busybox init, etc.)

nspctl supports containers with any init system. nspctl provides almost all of the features that machinectl provides.

**Currently implemented features are:**

* Lists

  - running containers
  - stopped containers
  - all containers

* Containers info
* Containers status
* Start the container
* Stop the container
* Reboot the container
* Remove the container
* Enable the container (the container to be launched at boot)
* Disable the container at startup
* Copy files from host in to a container
* Login the container shell
* Pull and register containers(raw, tar and docker images)
* Bootstrap **Debian** container ("jessie" and newer are supported)
* Bootstrap **Ubuntu** container ("xenial" and newer are supported)
* Bootstrap **Arch Linux** container
* Bootstrap **Alpine Linux** container("v3.13" and newer are supported)
* Remove hidden VM or container images
* Remove all VM and container images
* Run a new command in a running container (non-interactive shell)
* Renames a container or VM image
* import raw, tar and directory container images

Installation
############

Requirements:
*************

- Python >=3.8

Dependencies:
*************

- systemd-container package

For Debian and Ubuntu:

.. code-block::

  $ apt-get install systemd-container

For Centos, Fedora or Redhat Based Distributions:

.. code-block::

  $ yum install systemd-container

or

.. code-block::

 $ dnf install systemd-container

.. note::

  Gentoo with systemd and Arch Linux users don't need to install any packages.

Install:
********

**From Github:**

* Clone this repository:

.. code-block::

    $ git clone https://github.com/mofm/nspctl

* and install via pip:

.. code-block::

    $ pip install nspctl/

If you would like to install for your user:

.. code-block::

    $ pip install --user nspctl/

and you need to add '.local/bin' directory to your path

.. code-block::

    $ export PATH="~/.local/bin/:$PATH"

Usage:
######

**Synopsis:**

.. code-block::

  nspctl [ arguments ] [ options ] [ container name | URL | distribution ] [ ... ]

Commands:
*********

- *list* : List currently running (online) containers.

.. code-block::

  $ nspctl list

- *list-stopped* : List stopped containers.( shortopts: 'lss')

.. code-block::

  $ nspctl list-stopped
  $ nspctl lss

- *list-running* : List currently running containers.(alias: 'list', shortopt: 'lsr')

.. code-block::

  $ nspctl list-running
  $ nspctl lsr

- *list-all* : List all containers.(shortopt: 'lsa')

.. code-block::

  $ nspctl list-all
  $ nspctl lsa

- *info NAME* : Show properties of container.

.. code-block::

  $ nspctl info ubuntu-20.04

- *start NAME* : Start a container as system service.

.. code-block::

  $ nspctl start ubuntu-20.04

- *reboot NAME* : Reboot a container.

.. code-block::

  $ nspctl reboot ubuntu-20.04

- *stop NAME* : Stop a container. Shutdown cleanly.(alias: 'poweroff')

.. code-block::

  $ nspctl stop ubuntu-20.04

- *terminate NAME* : Immediately terminates container without cleanly shutting it down.

.. code-block::

  $ nspctl terminate ubuntu-20.04

- *poweroff NAME* : Poweroff a container. Shutdown cleanly.

.. code-block::

  $ nspctl poweroff ubuntu-20.04

- *enable NAME* : Enable a container as a system service at system boot.

.. code-block::

  $ nspctl enable ubuntu-20.04

- *disable NAME* : Disable a container as a system service at system boot.

.. code-block::

  $ nspctl disable ubuntu-20.04

- *remove NAME* : Remove a container completely.

.. code-block::

  $ nspctl remove ubuntu-20.04

- *shell NAME* : Open an interactive shell session in a container.

.. code-block::

  $ nspctl shell ubuntu-20.04

- *copy-to NAME SOURCE DESTINATION* : Copies files from the host system into a running container.

.. code-block::

    $ nspctl copy-to ubuntu-20.04 /home/hostuser/magicfile /home/containeruser/

- *clean* : Remove hidden VM or container images. This command removes all hidden machine images from /var/lib/machines/.

.. code-block::

    $ nspctl clean

- *clean-all* : Remove all VM or container images. This command removes all machine images from /var/lib/machines/.

.. code-block::

    $ nspctl clean-all

- *exec NAME 'COMMAND'* : Runs a new command in a running container.

.. code-block::

    $ nspctl exec ubuntu-20.04 'cat /etc/os-release'

- *rename NAME NEWNAME* : Renames a container or VM image.

.. code-block::

    $ nspctl rename ubuntu-20.04 ubuntu-newimage

- *usage* : nspctl usage page

.. code-block::

    $ nspctl usage

- *--help* : display help page and exit

.. code-block::

    $ nspctl --help or -h


Container Operations:
*********************

- *pull-tar URL NAME* : Downloads a .tar container image from the specified URL.(tar, tar.gz, tar.xz, tar.bz2)

.. code-block::

    $ nspctl pull-tar https://github.com/mofm/meta-econ/releases/download/v0.3.0-r2/econ-tiny-nginx-20220123-qemux86-64.tar.xz econ-nginx

- *pull-raw URL NAME* : Downloads a .raw container from the specified URL.(qcow2 or compressed as gz, xz, bz2)

.. code-block::

    $ nspctl pull-raw https://download.fedoraproject.org/pub/fedora/linux/releases/35/Cloud/x86_64/images/Fedora-Cloud-Base-35-1.2.x86_64.raw.xz fedora-cloud-base-35


- *import-raw IMAGE NAME* : Execute a ``machinectl import-raw`` to import a .qcow2 or raw disk image.

.. code-block::

    $ nspctl import-raw Fedora-Cloud-Base-35-1.2.x86_64.raw.xz fedora-cloud-base-35

- *import-tar IMAGE NAME* : Execute a ``machinectl import-tar`` to import a .tar container image.

.. code-block::

    $ nspctl import-tar econ-tiny-nginx-20220123-qemux86-64.tar.xz econ-nginx

- *import-fs DIRECTORY NAME* : Execute a ``machinectl import-fs`` to import a directory image.

.. code-block::

    $ nspctl import-fs econ-tiny-nginx-20220123 econ-httpd


- *bootstrap NAME DIST VERSION* : Bootstrap a container from package servers. Supported Distributions are Debian, Ubuntu, Arch Linux and Alpine Linux.

.. code-block::

    $ nspctl bootstrap alpine-3.15 alpine latest-stable
    $ nspctl bootstrap ubuntu-20.04 ubuntu focal
    $ nspctl bootstrap debian-latest debian stable
    $ nspctl bootstrap arch-test arch

