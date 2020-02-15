.. title: IPA Client Kurulumu
.. slug: ipa-client-kurulumu
.. date: 2017-01-22 16:24:47 UTC+03:00
.. tags: ipa, ipa-client, centos 
.. category: 
.. link: 
.. description: 
.. type: text

**Kullanilan yazilimlar:**
        - Centos Linux 7.2

                - ipa-client
                - ipa-admin-tools

**Kurulum Oncesi Hazirlik:**

.. code-block:: bash

        FQDN = ipaclient.piesso.local
        IP = 172.16.183.135/24
        IPA Server = ipa.piesso.local
        IPA DOMAIN = piesso.local
        IPA NETBIOS = PIESSO


Kuruluma  baslamadan once kontrol edilmesi gerekenler;

        #. Hostname
        #. /etc/hosts

        #. Sistem update


*Hostname:*

.. code-block:: bash

        # hostnamectl set-hostname ipaclient.piesso.local


*/etc/hosts:*

.. code-block:: bash

        172.16.183.135 ipaclient.piesso.local ipaclient
        172.16.183.128 ipa.piesso.local

*Sistem update:*

.. code-block:: bash

        # yum update -y

**Kurulum:**

- ipa-client ve ipa-admintools yazilimlarinin repodan kurulmasi;

.. code-block:: bash 

        # yum install ipa-client ipa-admintools


- ipa-client kurulumu;

.. code-block:: bash

        # ipa-client-install --domain PIESSO.LOCAL --server ipa.piesso.local --realm PIESSO -p host/ipa.piesso.local --enable-dns-updates --force-ntpd


**IPA Client ve Kerberos Ticket Testi:**

- FreeIpa sunucusundaki admin kullanicisi ve parolasi ile giris yapin;

.. code-block:: bash 

        # getent passwd admin
        # getent group admins

- Kerberos'tan ticket alimi;

.. code-block:: bash

        # kinit admin

- Ticketin basarili alinip alinmadigi kontrolu;

.. code-block:: bash

        # klist

- Hersey saglam gorunuyorsa client dns'lerini FreeIPA Server adresine donusturulmesi;

*/etc/resolv.conf:*

.. code-block:: bash

        search piesso.local
        nameserver 172.16.183.128

