.. title: FreeIPA ve Active Directory Entegrasyonu
.. slug: freeipa-ve-active-directory-entegrasyonu
.. date: 2017-01-22 17:20:37 UTC+03:00
.. tags: freeipa, active directory
.. category: 
.. link: 
.. description: 
.. type: text

**Kurulum oncesi hazirlik:**
        #. FreeIPA Server 4.4.0-14 ( CentOS 7 )
               - IPA Server IP Adresi: 172.16.183.128
               - IPA Server Hostname: ipaserver.piesso.local
               - IPA Domain: piesso.local
               - IPA Netbios: PIESSO
               - IPA Kerberos realm: PIESSO.LOCAL

        #. Windows Server 2012 R2
               - Active Directory IP Adresi: 172.16.183.132
               - Active Directory Hostname: ad.pencere.local
               - Active Directory Domain: pencere.local
               - Active Directory Netbios: PENCERE

Windows Server 2012 R2 ve FreeIPA icin kerberos ticket vs gibi sorunlar yasanmamasi icin ntp ile zaman esitlemesi mutlaka baslatilmalidir. FreeIPA kurulumunda ontanimli olarak ntp client "time sync" islemini ntp pool'larindan alarak esitlemektedir. Fakat Windows Server 2012 R2 uzerinde de bunu yapmak icin manuel ntp pool sunucularini girip zaman servisini yeniden baslatilmasi gerekmektedir.

.. warning::
        2016 Bakanlar Kurulu karari ile yaz saati uygulamasi sona erdigi icin zaman diliminin "+3" oldugunu kontrol edin.

*(Powershell uzerinde)*

.. code-block:: powershell

        > net stop w32time
        > w32tm /config /syncfromflags:manual /manualpeerlist:0.centos.pool.ntp.org, 1.centos.pool.ntp.org, 2.centos.pool.ntp.org”
        > w32tm /config /reliable:yes
        > net start w32time

**FreeIPA ve Active Directory Cross-Realm Trust:**

- Ilk olarak "ipa-adtrust-install" paketini repodan kuralim:

.. code-block:: bash
        
        # yum install ipa-adtrust-install

- IPA Server uzerinde cross-realm islemi icin:

.. code-block:: bash

        # ipa-adtrust-install --netbios-name=PIESSO -a password

**Firewall Konfigurasyonu:**

Windows Server uzerinde firewall uzerindeki kurallar otomatik olarak ekleniyor. Fakat IPA Server uzerinde asagidaki portlarin acik olmasi gerekmektedir. 

.. code-block:: console

        TCP ports: 80, 88, 443, 389, 636, 88, 464, 53, 135, 138, 139, 445, 1024-1300
        UDP ports: 88, 464, 53, 123, 138, 139, 389, 445

Centos 7 ile birlikte gelen firewall manager firewalld spesifik servisleri acmak icin halen yetersiz oldugu icin bunu disabled edip yerine klasik iptables'i aktif edelim: 

.. code-block:: bash
        
        # systemctl disable firewalld
        # systemctl stop firewalld
        # yum install -y iptables-services 
        # systemctl enable iptables

"/etc/sysconfig/iptables" dosyasina gerekli olan portlari acmak icin kurallarimizi girelim:

.. code-block:: console

        \*filter 
        :INPUT ACCEPT [0:0] 
        :FORWARD ACCEPT [0:0] 
        :OUTPUT ACCEPT [0:0] 
        -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT 
        -A INPUT -p icmp -j ACCEPT 
        -A INPUT -i lo -j ACCEPT 
        -A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT 
        -A INPUT -s ad_ip_address -p tcp -m multiport --dports 389,636 -m state --state NEW,ESTABLISHED -j REJECT 
        -A INPUT -p tcp -m multiport --dports 80,88,443,389,636,88,464,53,138,139,445 -m state --state NEW,ESTABLISHED -j ACCEPT 
        -A INPUT -p udp -m multiport --dports 88,464,53,123,138,139,389,445 -m state --state NEW,ESTABLISHED -j ACCEPT 
        -A INPUT -p udp -j REJECT 
        -A INPUT -p tcp -j REJECT 
        -A FORWARD -j REJECT --reject-with icmp-host-prohibited 
        COMMIT

Iptables servisini baslatabiliriz:

.. code-block:: bash

        # systemctl start iptables

**DNS Forward Zone:**

Active Directory ve FreeIPA'yi inbound ve outbound trust olarak isaretlemeden DNS Forward Zone'lari ekleyelim.

- Windows Server 2012 R2 uzerinde:

.. code-block:: powershell

        > dnscmd 127.0.0.1 /ZoneAdd piesso.local /Forwarder 172.16.183.128

- FreeIPA Server uzerinde:

.. code-block:: bash

        # ipa dnsforwardzone-add pencere.local --forwarder=172.16.183.132 --forward-policy=only

- Forwarder DNS zone'larin dogru sekilde eklenip eklenmedigi iki tarafta da kontrol edelim:

*Windows Server 2012 R2 (PowerShell):*

.. code-block:: powershell

        > nslookup
        > set type=srv
        > _ldap._tcp.ad_domain
        > _ldap._tcp.ipa_domain
        > quit

- FreeIPA Server uzerinde:

.. code-block:: bash

        # dig SRV _ldap._tcp.ipa_domain
        # dig SRV _ldap._tcp.ad_domain


**Cross-Realm Trust:**

Freeipa ile Active Directory arasinda "Two-way trust" konfigurasyonu:

.. code-block:: bash

        # ipa trust-add --type=ad pencere.local --admin Administrator --password --two-way=true

"Two-way trust" baglantisinin basarili sekilde kurulup kurulmadigini kontrol edelim:

.. code-block:: bash

        # ipa trust-fetch-domains "pencere.local"
        # ipa trustdomain-find "pencere.local"

