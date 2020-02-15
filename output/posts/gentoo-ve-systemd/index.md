<html><body><p>Systemd büyük bir hızla ,öncelikle güncel linux dağıtımlarında yerini almaya başladı.Systemd linux çekirdeği için geliştirilen ve klasik init sistemlerinin(openrc vs.) yerine geçecek olan daha hızlı ve kararlı bir sistem yönetim daemonu.

<img class="  " alt="systemd pstree çıktısı" src="https://raw.githubusercontent.com/hut/minirc/master/screenshot.png" width="368" height="277"> systemd pstree çıktısı

 
<img class=" " alt="init pstree çıktısı" src="https://cdn-images-1.medium.com/max/582/1*-QPL92V3VJo6BuGRJ6qJ-w.png"     width="357" height="251"> init pstree çıktısı
 
<p>Yukardaki ekran görüntüleri örneklerinde de gördüğünüz gibi systemd 'nin sistem üzerindeki ilk daemon(ve proses) olduğu ve userspace üzerinde çalışacak olan tüm prosesler klasik init sistemlerinde olduğu gibi systemd'nin alt proseslerini oluşturmaktadir.Systemd'nin yapısını biraz daha iyi anlamak için aşağıdaki şema yardımcı olacaktır.
</p>
<img class=" " alt="Systemd Bileşenleri" src="https://upload.wikimedia.org/wikipedia/commons/3/35/Systemd_components.svg" width="432" height="243"> Systemd Bileşenleri

Binary Linux Dağıtımlarında eğer systemd'ye geçilmişse ayrıca birşey yapmanıza gerek yok.Fakat Gentoo Linux dağıtımında şu an stage 3'te öntanımlı gelmediği için kendiniz yardımcı araçlarla geçebilirsiniz.(ki gentoo geliştiricileri bunun için birçok şeyi hazırlamış bulunmakta.)

Kısa adımlarla systemd'ye geçişten bahsedebilirim:

1. İlk olarak çekirdeğimize systemd için gerekli destekleri verelim.Gentoo geliştiricileri bu konuda kullanıcıları rahatlamak için güncel kernel sürümlerinde <em>"kernel konfigürasyon menüsü"</em>ne eklenen <em>"Gentoo Linux"</em> sekmesinin altında bulunan <em>"Support for init systems, system and service managers"</em> alt sekmesinin içinde bulunan <em>"systemd"</em> seçeneğini seçerek kernel için gerekli tüm destekleri kolayca verebilirsiniz.Bu seçenek sizin zorunlu olan destekleri tek tek elle vermek yerine hızlıca yapmanizi sağlayan bir kısayol.

Gerekli destekleri verdikten sonra kernelimizi ve modüllerimizi yeniden derleyin.

 

2. Kullandığınız herhangi grafik arabirimi ya da hangi sistem ise "Gentoo" profilinizi "systemd" profiline değiştirerek gerekli profil değişiklerini tanımlayın.
</p><pre># eselect profile list

Available profile symlink targets:
[1]   default/linux/amd64/13.0
[2]   default/linux/amd64/13.0/selinux
[3]   default/linux/amd64/13.0/desktop
[4]   default/linux/amd64/13.0/desktop/gnome *
[5]   default/linux/amd64/13.0/desktop/gnome/systemd
[6]   default/linux/amd64/13.0/desktop/kde
[7]   default/linux/amd64/13.0/desktop/kde/systemd
[8]   default/linux/amd64/13.0/developer
[9]   default/linux/amd64/13.0/no-multilib
[10]  default/linux/amd64/13.0/x32
[11]  hardened/linux/amd64
[12]  hardened/linux/amd64/selinux
[13]  hardened/linux/amd64/no-multilib
[14]  hardened/linux/amd64/no-multilib/selinux
[15]  hardened/linux/amd64/x32
[16]  hardened/linux/uclibc/amd64</pre>
Beşinci seçenekte olan <i>"default/linux/amd64/13.0/desktop/gnome/systemd"</i> profili ile değiştirelim.
<pre># eselect profile set 5</pre>
 

3. Bu adımda <i>"systemd"</i>yi yükleyelim.
<pre># emerge --ask systemd</pre>
4. Profilimizi değiştirdiğimiz için sistemi güncellemeden önce <i>"sys-apps/dbus"</i> uygulamasının <i>"systemd" <b>USE FLAG</b>'ını deaktif(</i>
<pre>/etc/portage/package.use dosyasınıza "sys-apps/dbus -systemd"</pre>
şeklindeki satırı ekleyin.) edin ve daha sonra sistemi güncelleyin.
<pre># emerge -NuDa world</pre>
Sistemimize bu şekilde gerekli systemd desteğini vererek <b>"systemd"</b> ile açılmasına hazır hale getirdik.

5. Yeniden başlatmadan önce sistemin systemd ile başlaması için ön yükleyicinizin kernel satırına(grub için) aşağıdaki gibi ekleyin:

( /boot/grub/menu.lst )
<pre>kernel /vmlinuz-3.7.10-r1 root=/dev/sda2 init=/usr/lib/systemd/systemd</pre>
Grub 2 için;

( /boot/grub/grub.cfg )
<pre>linux /vmlinuz-3.7.10-r1 root=UUID=21312312-12312312-1231121 init=/usr/lib/systemd/systemd</pre>
UEFI kullanan sistemler için 1.adımda kernel derlemeden önce "kernel konfigürasyon menüsü"nde
"<b>Processor type and features</b>" -&gt; "<b>Built-in kernel command line</b>" içine aşağıdaki gibi ekleyebilirsiniz;
<pre>root=/dev/sda2 init=/usr/lib/systemd/systemd</pre>
6.Sistemi yeniden başlatın.

7.Sistem yeniden başladıktan sonra eski(Openrc vs.) init sistemi üzerinde tanımladığımız hostname,locale ayarları artık systemd üzerinde geçerli olmayacaktır.

Systemd hostname ayarlamak için;
<pre># hostnamectl set-hostname benimpc</pre>
Systemd klavye ayarları için;
<pre># localectl set-keymap trq</pre>
X11 için;
<pre># localectl set-x11-keymap tr</pre>
Sistem locale ayarı için;
<pre># localectl set-locale LANG=en_US.UTF-8</pre>
Türkçe için;
<pre># localectl set-locale LANG=tr_TR.UTF-8</pre>
8.Yukardaki adımda sistem için gerekli tanımlamaları yaptık.Fakat herhangi bir grafik arabirimi kullanıyorsanız,bu açılmayacaktır.Systemd üzerinde de diğer init sistemlerinde olduğu gibi gerekli olan servisleri sistem açılışına ekleyebilir,servisleri çalıştırabilir,durumunu öğrenebilir ve bir servisi durdurabiliriz.

Systemd üzerinde sistem açılışında aktif olan servis ya da  hizmetleri ve bunların durumlarını görmek için;
<pre># systemctl</pre>
Aktif ve deaktif tüm servislerin durumunu görmek için;
<pre># systemctl list-unit-files</pre>
Herhangi bir servisi sistem açılışına eklemek için;
<pre># systemd enable vixie-cron.service</pre>
Herhangi bir servisi çalıştırmak için;
<pre># systemctl start syslog-ng.service</pre>
<b>NOT:</b> systemd herhangi bir syslog yazılımına ihtiyaç duymamaktadır.Systemd üzerinde journal log bilgilerini tutmaktadır.

Herhangi bir servisin durumunu görmek için;
<pre># systemctl status NetworkManager.service</pre>
Herhangi bir servisi durdurmak için;
<pre># systemctl stop upower.service</pre>
Herhangi bir servisi yeniden başlatmak için;
<pre># systemctl restart dhcpcd.service</pre>
<b>NOT:</b> Gerekli olan servisleri sistem açılışında aktif etmeyi ihmal etmeyin.Grafik arabirimini sistem açılışında başlaması için örnek olarak "xdm"i sistem açılışında aktif etmek için;
<pre># systemctl enable xdm.service</pre>
Burada dikkat edilecek nokta openrc'den systemd'ye geçişte <i>"/etc/conf.d/xdm"</i> içerisinde yapmış olduğumuz herhangi bir <i>"display manager"</i> ayarımız geçersiz olacaktır.Geçerli olan <i>"display manager"</i>i xdm'nin açılışta çalıştırması istiyorsanız;

<i>"/usr/lib/systemd/system/xdm.service"</i> dosyası içindeki ,
<pre>[Service]
ExecStart=/usr/bin/xdm -nodaemon</pre>
--&gt; satırını;

(GDM için)
<pre>[Service]
ExecStart=/usr/bin/gdm</pre>
---&gt; şeklinde değiştirin.Bu şekilde sistem açılışında <b>"gdm"</b>yi aktifleştirebiliyoruz.

9. Değinebileceğim diğer bir nokta ise açılışta otomatik yüklenmesi istediğiniz modüller ve network ayarları.

Sistem açılışında otomatik yüklenmesi istediğiniz modül ya da  modülleri <b>"/etc/modules-load.d"</b> dizini içerisine isterseniz ayrı ayrı,istediğiniz sekilde isimlendirdiğiniz dosyaların içerisine ilk satıra ve ya tek bir dosya içerisinde her modül tek satırda olacak şekilde yazabilirsiniz.Örnek:

( /etc/modules-load.d/modullerim.conf )
<pre>bridge

tun</pre>
<pre>şeklinde ekleyebilirsiniz.

Network Ayarları kısmında ise ,kablolu ve otomatik ip alan bir networkte bulunuyorsanız, açılışta dhcpcd servisini aktif etmeniz yeterli.</pre>
<pre># systemctl enable dhcpcd.service</pre>
Eğer network-manager kullanıyorsanız , sistem açılışında aktif etmek için;
<pre># systemctl enable NetworkManager.service</pre>
Ya da farklı bir network modelinde çalışıp kendiniz oluşturmak için kolayca systemd servis dosyası yazabiliriz."/etc/systemd/system" dizini içerisine kendi istediğimiz modelde bir script yazarak açılışta aktif edebiliriz.Örnek olarak;

( /etc/systemd/system/mynetwork.service )
<pre>[Unit]
Description=network ayarlarim
After=network.target

[Service]
Type=oneshot
RemainAfterExit=yes

EnvironmentFile=/etc/conf.d/bridge.conf

ExecStart=/bin/ifconfig eth0 up
ExecStart=/bin/ifconfig eth1 up
ExecStart=/usr/bin/tunctl -b -u rico -t tap0
ExecStart=/bin/ifconfig tap0 up promisc
ExecStart=/sbin/brctl addbr br0
ExecStart=/sbin/brctl addif br0 eth0
ExecStart=/sbin/brctl addif br0 eth1
ExecStart=/sbin/brctl addif br0 tap0
ExecStart=/sbin/dhcpcd br0

ExecStop=/usr/bin/killall dhcpcd
ExecStop=/bin/ifconfig eth0 down
ExecStop=/bin/ifconfig eth1 down
ExecStop=/bin/ifconfig tap0 down
ExecStop=/sbin/brctl delif br0 tap0
ExecStop=/usr/bin/tunctl -d tap0
ExecStop=/sbin/brctl delif br0 eth0
ExecStop=/sbin/brctl delif br0 eth1
ExecStop=/bin/ifconfig br0 down
ExexStop=/sbin/brctl delbr br0

[Install]
WantedBy=multi-user.target</pre>
Systemd ile iyi keyifler :)</body></html>
