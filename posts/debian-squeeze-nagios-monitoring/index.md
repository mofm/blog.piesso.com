<html><body><strong><img class="alignright" title="nagios" src="http://blog.netways.de/wp-content/uploads/2008/03/nagios_logo.png" alt="" width="230" height="62">Nagios Nedir?</strong> NAGIOS sistem ve ağ denetleme uygulamasıdır.Belirtilen makine üzerinde çalışan servislerin durumunu kontrol eder ve uygulamalarda bir problem olduğunda belirtilen yöntemle kullanıcıya bildirir.Aynı segmentte ya da değil Nagios ile belirtilen makina,servisler kontrol edilebilir.

Nagios ile ne yapılabilir:
<ul>
	<li><em>Network servisleri denetleneme (SMTP, POP3, HTTP, NNTP, PING, vs)</em></li>
	<li><em>Makine kaynakları denetleneme (disk kullanımı vs )</em></li>
	<li><em>Otomatik log döndürme (log rotation)</em></li>
	<li><em>Belirtilen servisler yada makineler üzerinde belirtilen durumlarda kullanıcıya çeşitli</em>
<em> yöntemlerle uyarı verme</em></li>
	<li><em>Mail , SMS , Telefon , ICQ vb yöntemlerle uyarı verebilme</em></li>
	<li><em>Web arayüzünden makinelerin , servislerin ,logların ayrıntılı takibi</em></li>
</ul>
olarak sıralanabilir. [<a href="http://www.google.com.tr/url?sa=t&amp;source=web&amp;cd=1&amp;ved=0CCIQFjAA&amp;url=http%3A%2F%2Fwww.enderunix.org%2Fdocs%2Fnagios.pdf&amp;ei=EIqPTZT4Oo3V4gbB-ZCrCw&amp;usg=AFQjCNF6ZpEBGDdzpDLEhy70b2qE0gET9w" target="_blank">1</a>]

Nagios hakkında kısa bir bilgi verdikten sonra,Debian Squeeze üzerine Nagios kurulumunu ve diğer Debian Squeeze sunucuların nasıl monitor edileceği hakkında kısaca değineceğim.

İlk olarak Nagios'u monitoring yapacağımız makinaya kurulumunu yapalım ve daha sonra nagios client ile  izleyeceğimiz diğer sunuculara geçelim.Kısaca bir makinamız Nagios Server ve diğer izleyeceğimiz sunucu ise Nagios Client olarak anabiliriz.
<h4>Nagios Server Kurulumu :</h4>
Debian Squeeze depolarında nagios paketlerini bulunduğu için ,direk depodan kurulum yapacağım.Kaynak koddan kurulum yapmayacağım.Kaynak kodlardan kurulum için bu <a href="http://www.google.com.tr/url?sa=t&amp;source=web&amp;cd=3&amp;ved=0CCsQFjAC&amp;url=http%3A%2F%2Fwww.syslogs.org%2Fnagios-kurulumu-ve-yapilandirmasi%2F&amp;ei=24uPTaWoNYfM4gbs5pntCw&amp;usg=AFQjCNHAdCSZhOCGXCtsxfrLhCVXqdpn5A" target="_blank">adrese</a> bakabilirsiniz.

Depodan gerekli paketleri kuralım:

<em>Nagios Server</em>
<pre><strong># apt-get install nagios3 nagios-plugins nagios-nrpe-plugin</strong></pre>
Bu kurulum aşamasında SAMBA sizden workgroup adı isteyecektir.Öntanımlı ayarları onaylayarak geçebilirsiniz.Ayrıca Nagiosadmin için sizden parola belirlemenizi isteyecektir.İsteğinize göre parola belirleyip devam edin.

Şimdi Nagios Client olan sunucumuza gerekli kurulumları yapabiliriz.

<em>Nagios Client</em>

<strong># apt-get install nagios-nrpe-server nagios-plugins</strong>

Nagios Client sunucumuzda gerekli paketleri kurduktan sonra yapılandırmalara geçelim.Nagios Client sunucumuzda Nagios Server'ımızın ip adresini verelim.Bunun " <em>/etc/nagios/nrpe.cfg</em> " dosyasında gerekli değişiklikleri yapalım:
<pre><strong># vi /etc/nagios/nrpe.cfg</strong></pre>
Dosyamızı açtıktan "<em>allowed_hosts= </em>" ile başlayan satırı bulun ve ;

<strong>allowed_hosts=127.0.0.1</strong>

yerine Nagios Server'ımızın ip'sini girelim.( Örnek olarak <strong>192.168.1.45</strong> Nagios Server'ımın ip'si)

<strong>allowed_hosts=192.168.1.45</strong>

Şeklinde değiştirin.Yapacağımız diğer bir ayar ise eğer disk kullanımını izlemek istiyorsak gerekli değişikliği yapmalıyız.

Bunun içinde Nagios Client makinamızdaki izleyeceğimiz disk ve partition'ı belirleyip,nagios'a bunu bildirmek.

İzleyeceğiniz disk ve partition'ı yine "<em>/etc/nagios/nrpe.cfg</em>" dosyasında belirtelim.
(disklerimizi ve partitionlarınızı '<strong>df -h</strong>' komutuyla görebilirsiniz.)
Örnek olarak '<strong>sda5</strong>' partition'ı izlemek için gerekli ayarlar:

<strong># vi /etc/nagios/nrpe.cfg</strong>

Dosyamızı açtıktan sonra aşağıdaki satırı bulup gerekli değişiklikleri yapalım.
<pre>command[check_hda1]=/usr/lib/nagios/plugins/check_disk -w 20% -c 10% -p /dev/hda1</pre>
yerine

command[check_sda5]=/usr/lib/nagios/plugins/check_disk -w 20% -c 10% -p /dev/sda5

şeklinde değiştirin.

Nagios Client tarafında gerekli ayarlamaları yaptıktan sonra 'nagios-nrpe' servisini yeniden başlatın.

<strong># /etc/init.d/nagios-nrpe-server restart</strong>

Şimdilik Nagios Client tarafındaki işlemlerimiz bitti.Artık Nagios Server tarafındaki ayarlamalara geçelim.
İlk olarak Nagios Server'a izleyeceğimiz client'ı ve bu client üzerinde izleyeceğimiz servislerin ayarlarını yapalım.
Biraz önce Client ayarlarını yaparken Nagios Server'ımızın ip adresini(<em>192.168.1.45</em>) vermiştik,şimdi de Nagios Server'a
Client'ın ip'sini ve izleyeceğimiz servisleri verelim.(Client makinamın ip'si <strong>192.168.1.91</strong> ve izleyeceğim servisler
<em>HTTP servisi,disk durumu,load avarage,prossesler</em> )

Nagios Server'a bunları belirtmek için her ayrı client'a özel "<em>/etc/nagios3/conf.d/</em> " dizini altında bir konfigurasyon
dosyası oluşturalım.

<strong># touch /etc/nagios3/conf.d/client1_nagios.cfg</strong>

dosyamızı oluşturduktan sonra aşağıdaki ayarları dosyaya yazıp,kaydedelim.
<pre>define host{
        use             generic-host
        host_name       client1
        alias           client1
        address         192.168.1.91
}
define service{
        use                     generic-service
        host_name               client1
        service_description     HTTP-Server
        check_command           check_http
}
</pre>
<pre>define service{
        use                     generic-service
        host_name               client1
        service_description     Current Load
        check_command           check_nrpe_1arg!check_load
}
define service{
        use                     generic-service
        host_name               client1
        service_description     Current Users
        check_command           check_nrpe_1arg!check_users
}
define service{
        use                     generic-service
        host_name               client1
        service_description     Disk Space
        check_command           check_nrpe_1arg!check_sda5
}
define service{
        use                     generic-service
        host_name               client1
        service_description     Total Processes
        check_command           check_nrpe_1arg!check_total_procs
}
</pre>
Yukardaki gibi girildikten sonra Nagios servisini yeniden başlatalım.

<strong># /etc/init.d/nagios3 restart</strong>

Artık bir client için gerekli ayarları yaptık.Şimdi ayarlarımızı ve çalışıp,çalışmadığını test edelim:

<strong># cd /usr/lib/nagios/plugins/</strong>
<strong># ./check_nrpe -H 192.168.1.91 -c check_users</strong>

Eğer düzgün çalışıyorsa aşağıdaki gibi bir sonuç alacaksınız :

<em>USERS OK - 2 users currently logged in |users=2;5;10;0</em>

Nagios kurulumunu burada tamamladık.
Buarada anlatılanlardan daha fazla servis ve client ekleyebilirsiniz,hepsi size kalmış :)</body></html>