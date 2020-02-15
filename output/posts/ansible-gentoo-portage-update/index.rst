.. title: Ansible Gentoo-Portage Update
.. slug: ansible-gentoo-portage-update
.. date: 2018-01-14 02:13:06 UTC+03:00
.. tags: ansible, gentoo, portage
.. category: 
.. link: 
.. description: 
.. type: text

Ansible Portage module [1]_ ile Gentoo Linux sisteminizi guncelleyebilir ve upgrade edebilirsiniz. Asagidaki ornekte 
Ilk once buildfarm adini verdigimiz sunucu uzerinde compile edilip diger gentoo sunucularimiza binary paketleri
elde edip guncellemelerini yapmaktadir.


Yukarda bahsettigim sekilde bir buildfarm sunucusu yani paketlerin compile edilecegi sunucuda binary paketleri uretip 
diger sunuculara bu binary paketleri sunmak icin portage uzerinde "buildpkg" ozelligini aktif etmek gerekmektedir.

``/etc/portage/make.conf``:

.. code-block:: bash

   FEATURES="buildpkg"


Diger Gentoo sunucularin buildfarm uzerindeki paketleri alabilmesi icin yayinlamasi gerekli. Bunun birden fazla sekilde
kendinize cozum saglayabilirsiniz. FTP, FTPS, NFS, SSH, HTTP, HTTPS gibi. Biz kucuk bir web sunucusu kurup paketleri bu sekilde yayinlayalim.


.. code-block:: bash

   # emerge -av www-servers/lighttpd


lighttpd web sunucusunu kurduktan sonra olusturulan paketlerin buradan yayinlanmasini konfigure edelim."/etc/lighttpd/lighttpd.conf"
dosyasinin sonuna asagidaki iki satiri ekleyin.


``/etc/lighttpd/lighttpd.conf``:

.. code-block:: bash

   server.modules += ( "mod_alias" )
   alias.url = ( "/packages" => "/usr/portage/packages/" )


Artik web sunucumuzu baslatabiliriz.


.. code-block:: bash

   # rc-update add lighttpd default
   # /etc/init.d/lighttpd start


Buildfarm sunucumuz ile ayarlarimiz bu kadar. Artik diger sunucularimizi buildfarm sunucusu uzerinden binary paketleri
almasi icin konfigure edebiliriz.


``/etc/portage/make.conf``:


.. code-block:: bash

   FEATURES="getbinpkg"
   PORTAGE_BINHOST="http://buildfarm.hostname/packages"

Artik ansible ile sistemizi ilk once buildfarm ile derlenip binary paketler ile diger sunucularinizi guncelleyebilirsiniz.


.. gist:: 843654e91765dee16e64814bd3ba76af


.. [1] http://docs.ansible.com/ansible/latest/portage_module.html
