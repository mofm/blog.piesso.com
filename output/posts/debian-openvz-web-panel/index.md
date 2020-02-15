<html><body><img class="alignright" title="OpenVZ" src="http://www.admon.org/wp-content/uploads/2010/04/openvz.png" alt="" width="135" height="135">Birkaç adımda <a href="http://www.debian.org" target="_blank">Debian</a> Squeeze üzerine <a href="http://wiki.openvz.org/Main_Page" target="_blank">OpenVZ</a> ve entegre kolay yönetebilir web paneli kurulumu .

<strong>OpenVZ Nedir?</strong>
OpenVZ; Linux tabanlı, işletim sistemi düzeyinde sunucu sanallaştırma yazılımıdır. OpenVZ
aynı fiziksel sunucu üzerinde birden fazla yalıtılmış ve güvenli sanal ortamlar (Virtual
Environments – VEs veya Virtual Private Servers – VPSs diyebiliriz) oluşturur. Her sanal
ortam, fiziksel makine üzerinde sadece kendisi varmış gibi çalışır. Tüm sanal ortamlar
birbirinden bağımsız olarak yeniden başlatılabilir ve her sanal ortamın farklı sistem
kullanıcıları, IP adresleri, belleği, dosyaları, uygulamaları, sistem kütüphaneleri ve
yapılandırmaları vardır.
OpenVZ, SWsoft tarafından desteklenen açık kaynak kodlu, <em>GNU GPL</em> lisanslı bir projedir ve
yine bu firmanın ticari bir ürünü olan <em>VirtuozzoTM</em> temellidir.
OpenVZ altında çalışan bir sanal sistem en fazla <strong>64 GB</strong> belleği (RAM) destekleyebilir. Ayrıca
bir OpenVZ çekirdeği aynı anda en fazla <strong>100</strong> sanal işletim sistemi yönetebilir. [<a href="http://www.enderunix.org/docs/openvz.pdf" target="_blank">1</a>]

<strong>Debian Squeeze OpenVZ Kurulumu</strong>

Debian Squeeze üzerine OpenVZ ve gerekli araçları kurmak için ,

İlk önce depolarımızı güncelleyelim:
<pre><strong># apt-get update</strong></pre>
OpenVZ kernelimizi ve araçları yükleyelim:
<pre><strong># apt-get install linux-image-openvz-amd64 vzctl vzquota vzdump rsync iproute libatml</strong></pre>
Yeni kernelimiz ve araçlarımız yüklendikten sonra kernelimizdeki gerekli değişiklikleri yapalım.Bunun için "<strong>/etc/sysctl.conf</strong>" dosyasında bazı değişiklikler yapıyoruz.Kendi "<em>sysctl.conf</em>" dosyanızda aşağıdaki değişikleri ya da eklemeleri yapın:
<pre>[...]

# On Hardware Node we generally need
# packet forwarding enabled and proxy arp disabled

net.ipv4.conf.default.forwarding=1
net.ipv4.conf.default.proxy_arp=0
net.ipv4.ip_forward=1

# Enables source route verification
net.ipv4.conf.all.rp_filter=1

# Enables the magic-sysrq key
kernel.sysrq=1

# TCP Explict Congestion Notification
#net.ipv4.tcp_ecn=0

# we do not want all our interfaces to send redirects
net.ipv4.conf.default.send_redirects=1
net.ipv4.conf.all.send_redirects=0

[...]
</pre>
Dosyada gerekli değişikleri yaptıysanız , yeni kernelimizle sistemimizi başlatalım:
<pre><strong># reboot</strong></pre>
Sistem açıldıktan sonra kontrollerimizi yapalım :
<pre><strong># uname -r</strong>
2.6.32-5-openvz-amd64</pre>
<pre><strong># ps ax | grep vz</strong>
</pre>
<pre>1801 ?        S      0:00 [vzmond]</pre>
<pre><strong># ifconfig</strong></pre>
<pre>venet0    Link encap:UNSPEC  HWaddr 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00 
 UP BROADCAST POINTOPOINT RUNNING NOARP  MTU:1500  Metric:1
 RX packets:0 errors:0 dropped:0 overruns:0 frame:0
 TX packets:3 errors:0 dropped:0 overruns:0 carrier:0
 collisions:0 txqueuelen:0
 RX bytes:0 (0.0 B)  TX bytes:252 (252.0 B)</pre>
<strong>Yeni SANAL Makina Oluşturalım </strong>

Sanal makina oluşturmadan önce bir tane template indirelim:
<pre><strong># cd /var/lib/vz/template/cache</strong></pre>
<pre><strong># wget http://download.openvz.org/template/precreated/contrib/debian-6.0-amd64-minimal.tar.gz</strong>
<strong># vzctl create 01 --ostemplate debian-6.0-amd64-minimal</strong> (yeni makinamızı oluşturalım.)
<strong># vzctl set 01 --ipadd 10.1.0.100 --save</strong> (sanal makinamıza ip verelim.)
<strong># vzctl set 01 --nameserver 192.168.1.130 --save</strong> ( öntanımlı DNS ekleyelim.)
<strong># vzctl set 01 --hostname piesso.com --save</strong> (hostname'i ayarlayalım.)
<strong># vzctl start 01</strong> (Sanal makinamızı başlatalım.)
<strong># ping 10.1.0.100</strong> ( verdiğimiz ip'yi test edelim.)
<strong># vzctl exec 01 parola</strong> ( parola atayalım.)
<strong># vzctl enter 01</strong> ( Sanal makinaya geçiş yapalım. )</pre>
Daha detaylı bilgi için <a href="http://wiki.openvz.org/Man/vzctl.8" target="_blank">vzctl</a> , <a href="http://wiki.openvz.org/Man/vzlist.8" target="_blank">vzlist</a> , <a href="http://wiki.openvz.org/Man/vz.conf.5" target="_blank">vz.conf </a>man sayfalarına bakabilirsiniz ya da daha kolay yönetilebileceğiniz "OpenVZ Web Panel"i yükleyebilirsiniz.
<h1>OpenVZ Web Panel Kurulumu</h1>
OpenVZ'i daha rahat yönetebilmek ve diğer kullanıcılarında yetkileriyle kendi VPS'lerini yönetebilmesi için "<a href="http://code.google.com/p/ovz-web-panel/" target="_blank">OpenVZ Web Panel</a>"i tek satırda kuralım:
<pre><strong># <tt>wget -O - http://ovz-web-panel.googlecode.com/svn/installer/ai.sh | sh</tt></strong></pre>
Bu komuttan sonra eksik "ruby" paketleri sisteme kurulup paneliniz  burada "<strong>http://adresiniz:3000</strong>" hazır durumdadır.

<img class="alignnone" title="OpenVZ Web Panel" src="http://ovz-web-panel.googlecode.com/svn/wiki/images/promo.png" alt="" width="650" height="500"></body></html>