.. title: Gentoo kernel build script
.. slug: gentoo-kernel-build-script
.. date: 2021-12-28 01:48:49 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Automating the kernel compile, configuration copying, systemd-boot and grub2 configuration updating, old kernel cleaning script for Gentoo Linux.


Usage:
*******

- First, clone this repository and change directory:

  
.. code-block:: bash

  git clone https://github.com/mofm/kernel-build.git
  cd kernel-build


- Change script permissons:

  
.. code-block:: bash

  chmod +x build-kernel.sh


- If you are using systemd-boot you should first learn rootfs disk UUID or LVM partition and then add it to the script::

  
        UUID="dfc588c0-edd4-8543-a3fe-d7d49bd8f141"


**Optional:** *You can add specific kernel parameters to ROOTFLAGS.*


- Now you execute the script like so:

.. code-block:: bash

   ./build-kernel.sh systemd-boot


- If you are using **grub2**:

.. code-block:: bash

  ./build-kernel.sh grub2



  
.. warning::
   ``This script only cleans the previous kernel!``

