<html><body><p>Network'ünüz yalın IPv6'yı desteklemiyorsa ya da "İnternet Sağlayıcı"nız yalın IPv6 kullanmazı önermiyorsa,ama siz IPv6 ağına dahil olmak istiyorsanız dünyanın çeşitli bölgelerinde ücretsiz hizmet sunan "<em>IPv6 tunnel brokers</em>" mevcut.Tünelleme ile IPv4 bağlantınız üzerinden IPv6 ağına bağlanabileceksiniz.

"IPv6 Tunnel Brokers" listesi için <a href="http://en.wikipedia.org/wiki/List_of_IPv6_tunnel_brokers" target="_blank">buradan</a>.

Gentoo Linux üzerinde "IPv6" ağına birkaç dakika içinde dahil olabilirsiniz.İlk olarak içinde "ping" ve "ping6" komutlarını bulunduran "<strong>iputils</strong>" paketi kurulu değilse kurulumunu yapalım.


</p><blockquote># emerge net-misc/iputils</blockquote>

Ücretsiz tunnel brokers'lardan biri olan "<strong>Freenet6</strong>" ile IPv6 ağına bağlanmak için "<em>Freenet6 client</em>" uygulamasını kuralım.


<blockquote># emerge net-misc/gogoc</blockquote>

İsteğe bağlı olarak bu <a href="http://gogonet.gogo6.com/page/freenet6-ipv6-services" target="_blank">adresten</a> kendinize ait bir hesap açabilir ya da anonim olarak bağlanabilirsiniz.Eğer hesap oluşturduysanız,aşağıdaki gerekli yerleri "client" konfigurasyon dosyasına ekleyelim/değiştirelim.


<blockquote># vi /etc/gogoc/gogoc.conf</blockquote>

<code>userid=kullanici_adiniz (açmış olduğunuz freenet6 hesabı kullanıcı adı)
passwd=parolaniz
server=authenticated.freenet6.net (anonim server adresini comment'leyin.) 
auth_method=any (en güvenli seçenek)
dns_server=8.8.8.8:8.8.4.4 (herhangi IPv6 desteği olan DNS sunucuları)</code>

Gerekli konfigurasyonu yaptıktan sonra "freenet6 client" servisini çalıştıralım.


<blockquote># /etc/init.d/gogoc start </blockquote>

Her zaman IPv6 bağlantısı yapmak istiyorsanız bu servisi açılışa ekleyebilirsiniz.


<blockquote># rc-update add gogoc default</blockquote>

 
</body></html>