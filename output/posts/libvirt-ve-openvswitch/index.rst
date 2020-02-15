.. title: Libvirt ve OpenvSwitch
.. slug: libvirt-ve-openvswitch
.. date: 2018-01-15 00:13:52 UTC+03:00
.. tags: libvirt, openvswitch, kvm, qemu
.. category:
.. link: 
.. description: 
.. type: text

Bu yazimda libvirt ile openvswitch entegrasyonu hakkinda giris seviyesinde adim atacagiz. Kurulum ve entegrasyona gecmeden 
once bu iki yazilim nedir, ne degildir onlari taniyalim.


**Libvirt** [1]_ , Redhat tarafindan 2005'ten bu yana gelistirilmeye devam eden sanallastirma ortamlari icin daemon, API ve 
yonetim aracidir. 

.. image:: /images/libvirt_hypervisors.png


Libvirt bilinen bir cok hypervisor'u desteklemektedir. Iste bunlardan bazilari:

- KVM
- LXC
- OpenVZ
- Xen
- User-mode Linux (UML)
- Virtualbox
- VMware ESX
- VMware Workstation
- Hyper-V
- PowerVM
- Parallels Workstation
- Bhyve


**OpenvSwitch** [2]_ , kisaca sanal multilayer network switchtir. OpenvSwitch, bir SDN switch olarak hypervisor uzerindeki sanal makineleri 
fiziksel olarak ayri bulunan network switchler ile entegre calisarak yonetebilir. 

.. image:: /images/Distributed_Open_vSwitch_instance.png


Birden fazla protokolu desteklemektedir:

- NetFlow
- sFlow
- SPAN
- RSPAN
- CLI
- LACP
- 802.1ag

Kurulum:
--------


Paket yoneticiniz ile libvirt ve openvswitch kurulumunu yapalim. Siz kendi dagitiminiza ve paket yoneticinize gore kurulumu yapabilirsiniz.
Gentoo uzerinde, libvirt icin gerekli "USE FLAG"lari aktif edip kurulumunu yapalim.Binary dagitimlar icin buna gerek yoktur. Siz direk paket yoneticiniz ile kurulumu yapin.

/etc/portage/package.use/libvirt:
:: 

   app-emulation/libvirt macvtap vepa qemu virt-network


Simdi kurulumu yapabiliriz.


.. code:: bash

   # emerge -av libvirt
   

OpenvSwitch kurulumunu yapalim.


.. code:: bash

   # emerge -av openvswitch


Sistem baslangici icin bu servisleri enable edelim.


.. code:: bash

   # rc-update add ovsdb-server default
   # rc-update add ovs-vswitchd default 
   # rc-update add libvirtd default
   # rc-update add libvirt-guests default


.. note::  openvswitch ve kvm kernel modullerinin yuklendiginden emin olunuz. Kernel uzerinde aktif etmek icin openvswitch_ , qemu_.



Sistem acilisinda bu modullerin yuklenmesi icin

/etc/conf.d/modules::

        modules_4="openvswitch kvm kvm_intel tun"


Servisleri baslatalim.

.. code:: bash

   # /etc/init.d/ovsdb-server start
   # /etc/init.d/ovs-vswitchd start
   # /etc/init.d/libvirtd start
   # /etc/init.d/libvirt-guests start





.. [1] https://libvirt.org/
.. [2] http://openvswitch.org
.. _openvswitch: https://wiki.gentoo.org/wiki/QEMU_with_Open_vSwitch_network
.. _qemu: https://wiki.gentoo.org/wiki/QEMU
