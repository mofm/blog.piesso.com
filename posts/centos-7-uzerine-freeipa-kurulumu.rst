.. title: Centos 7 uzerine FreeIPA Kurulumu
.. slug: centos-7-uzerine-freeipa-kurulumu
.. date: 2017-01-21 22:15:13 UTC+03:00
.. tags: freeipa, centos
.. category: 
.. link: 
.. description: 
.. type: text

**Kullanilan yazilimlar:**

- Centos Linux 7.2
- ipa-server 4.2.0
- ipa-server-dns 4.2.0
- bind-dyndb-ldap 8.0

- bind 9.9.4
 
**Kurulum Oncesi Hazirlik:**

:FQDN: ipa.piesso.local

:IP: 172.16.183.128/24

:IPA DOMAIN: piesso.local

:IPA NETBIOS: PIESSO


Kuruluma  baslamadan once kontrol edilmesi gerekenler;

#. Hostname
#. /etc/hosts
#. Statik IP 

#. Sistem update

*1. Hostname:*

.. code-block:: bash

        # hostnamectl set-hostname ipa.piesso.local

*2. /etc/hosts:*

.. code-block:: bash
        :name: /etc/hosts

        172.16.183.128 ipa.piesso.local ipa

*3. Statik IP:*

Ornek statik ip konfigurasyonu "/etc/sysconfig/network-scripts/ifcfg-xxxx"

.. code-block:: bash

        ONBOOT= yes
        BOOTPROTO= none
        IPADDR= 172.16.183.128
        PREFIX= 24
        GATEWAY= 172.16.183.2
        DNS1= 8.8.8.8
        DNS2= 8.8.4.4
        DEFROUTE= yes

*4. Sistem update:*

.. code-block:: bash

        # yum update -y

**Kurulum:**

- ipa-server, integrated dns, ad trust  ve ldap back-end plugin yazilimlarinin repodan kurulmasi;

.. code-block:: bash

        # yum install ipa-server ipa-server-dns bind-dyndb-ldap ipa-server-trust-ad


-  ipa-server kurulumu;

.. code-block:: bash 

        # ipa-server-install -a IpaAdminpassword -p IpaManagerpassword --domain=piesso.local --realm=piesso.local --setup-dns --no-forwarders -U


- ipa-server kurulumu asagidaki sekilde basari ile biterse firewalld daemonuna gerekli port izinlerinin verilmesi;

.. code-block:: console

  Restarting the web server
  ==============================================================================
  Setup complete

  Next steps:
        1. You must make sure these network ports are open:
                   TCP Ports:
                     * 80, 443: HTTP/HTTPS
                     * 389, 636: LDAP/LDAPS
                     * 88, 464: kerberos
                     * 53: bind
                   UDP Ports:
                     * 88, 464: kerberos
                     * 53: bind
                     * 123: ntp
        2. You can now obtain a kerberos ticket using the command: 'kinit admin'
           This ticket will allow you to use the IPA tools (e.g., ipa user-add)
           and the web user interface.

  Be sure to back up the CA certificate stored in /root/cacert.p12
  This file is required to create replicas. The password for this
  file is the Directory Manager password


.. code-block:: bash

        # firewall-cmd --permanent --add-service={http,https,ldap,ldaps,kerberos,dns,kpasswd,ntp}
        # firewall-cmd --reload

- Firewall kurallarinin kontrol edilmesi;

.. code-block:: bash
        
        # firewall-cmd --list-services

**IPA Server ve Kerberos Ticket Testi:**

- Kerberos'tan ticket alimi;

.. code-block:: bash

        # kinit admin

- Ticketin basarili alinip alinmadigi kontrolu;

.. code-block:: bash

        # klist

- ipa-server servislerinin kontrolu;

.. code-block:: bash

        # ipactl status

- Hersey saglam gorunuyorsa sunucu dnslerini local adrese donusturulmesi;

*/etc/resolv.conf:*

.. code-block:: bash 

        search piesso.local
        nameserver 127.0.0.1

