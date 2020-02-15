<html><body><p>VPN çözümü olarak L2TP/IPSec kullanan Gentoo Linux kullanıcıları için kısaca client yapılandırma adımları:

1. İlk olarak 'portage' ağacımızı güncelleyelim.

<code># emerge --sync</code>
veya
<code># emerge-webrsync</code>

2. Gerekli olan paketleri kuralım."<strong><em>openswan</em></strong> ve <strong><em>xl2tpd</em></strong>"

<code># emerge openswan xl2tpd</code>

<strong>NOT:</strong> VPN bağlantısı(<em>örnek:authentication,encryption,compression gibi</em>) için kernel'de gerekli destekleri vermek gerekmektedir.Aşağıdaki seçenekleri kernel konfigürasyonunuzda aktif edip etmediğinizi kontrol edin.
 
 CONFIG_INET_AH=y
 CONFIG_INET_ESP=y
 CONFIG_INET_IPCOMP=y
 CONFIG_NET_KEY=y
 CONFIG_XFRM_IPCOMP=y
 CONFIG_INET_XFRM_MODE_TRANSPORT=y
 CONFIG_INET_XFRM_MODE_TUNNEL=y



3. Paket kurulumları bittikten sonra VPN bilgilerimize göre konfigürasyonları yapmaya başlayalım.Aşağıda örnek VPN sunucu ve istemci bilgileri verilmiş ve bu bilgilere göre ayarlamalar yapılmıştır.Sizde kendi VPN sunucu ve istemci bilgilerinize göre o kısımları değiştiriniz.


</p><blockquote>
VPN Sunucu Public IP: 195.202.46.45
VPN Sunucu Local IP: 10.1.40.40 ##### Firewall arkasındaki iç IP'si.Tabiki eğer NAT yapılıp,iç IP'si varsa.
Client Local IP: 192.168.2.80  
Interface: wlan0 ##### Kablosuz Arabirimi</blockquote>



<strong>"/etc/ipsec.conf"</strong> dosyasını aşağıdaki gibi düzenleyin.(Kendi IP ve arayüz bilgilerinize göre değiştirmeyi unutmayın!)



<blockquote>config setup
        virtual_private=%v4:10.0.0.0/8,%v4:192.168.0.0/16,%v4:172.16.0.0/12
        nat_traversal=yes
        protostack=netkey
        oe=no
        plutoopts="--interface=wlan0"

conn L2TP-PSK
        authby=secret
        pfs=no
        auto=add
        keyingtries=3
        dpddelay=30
        dpdtimeout=120
        dpdaction=clear
        rekey=yes
        ikelifetime=8h
        keylife=1h
        type=transport
        left=192.168.2.80
        leftnexthop=%defaultroute
        leftprotoport=17/1701
        right=195.202.46.45
        rightid=10.1.40.40
        rightprotoport=17/1701</blockquote>



Burada "<em>rightid=10.1.40.40</em>" şeklinde VPN sunucumuzun Firewall arkasındaki IP bilgilerini "<strong>INVALID_ID</strong>" hatası almamaniz için girmeniz gerekmektedir.Tekrar not düşeyim eğer Firewall arkasında ve NAT'lanmışsa gerek vardır."<em>/etc/ipsec.conf</em>" dosyasını düzenledikten sonra daha önce size verilen IPSEC Pre-Shared keyi "<strong>/etc/ipsec.secrets</strong>" dosyasını oluşturarak aşağıdaki gibi girelim:

<strong>"/etc/ipsec.secrets"</strong>


<blockquote>
192.168.2.80 10.1.40.40 : PSK "vpn_sunucunuzun_secret_keyi"</blockquote>




4. Bu aşamada '<em>portage</em>' ile kurulumunu yaptığımız "<strong>xl2tpd</strong>" paketinin init scripti küçük bir eksikle gelmektedir.Bu eksikliği manuel kendimiz tamamlayalım.

"<strong>/etc/init.d/xl2tpd</strong>" dosyasini açın ve 

<code>start() {
        checkconfig || return 1</code>

satırından sonra aynı girintide aşağıdaki satırları ekleyin.
        
        <code>if !([ -f /var/run/xl2tpd/l2tp-control ]); then
                mkdir -p /var/run/xl2tpd
                touch /var/run/xl2tpd/l2tp-control
        fi</code>

Şu şekilde görünmeli;

<code>start() {
        checkconfig || return 1
##################l2tp-control dosyasi olusturmak icin eklendi.######
        if !([ -f /var/run/xl2tpd/l2tp-control ]); then
                mkdir -p /var/run/xl2tpd
                touch /var/run/xl2tpd/l2tp-control
        fi
#############################################################################
        ebegin "Starting xl2tpd"
        start-stop-daemon --start --quiet --exec /usr/sbin/xl2tpd
        eend $?
}
</code>

ve dosyamızı kaydedip kapatalım.


5. "<strong>/etc/xl2tpd/xl2tpd.conf</strong>" dosyasını aşağıdaki gibi satırları ekleyip kaydedelim.



<blockquote>[lac vpn-connection]
lns = 195.202.46.45
ppp debug = yes
pppoptfile = /etc/ppp/options.l2tpd.client
length bit = yes</blockquote>



6. "<strong>/etc/ppp/options.l2tpd.client</strong>" dosyasını aşağıdaki gibi satırları ekleyip kaydedelim.Dosyanin son iki satırında bulunan '<em>name</em>' ve '<em>password</em>' satırlarına VPN erişimi için kullanacağınız kullanıcı adı ve parolanızı giriniz.



<blockquote>ipcp-accept-local
ipcp-accept-remote
refuse-eap
require-mschap-v2
noccp
noauth
idle 1800
mtu 1410
mru 1410
defaultroute
usepeerdns
debug
lock
connect-delay 5000
name vpnkullaniciadi
password vpnerisimparolasi</blockquote>




7. Servisleri başlatalım.

<code># /etc/init.d/ipsec start

# /etc/init.d/xl2tpd start</code>

8. Gerekli ayarlamalar bitti.VPN bağlantısını aşağıdaki komutları vererek başlatalım;

<code># ipsec auto --up L2TP-PSK

# echo "c vpn-connection" &gt; /var/run/xl2tpd/l2tp-control</code>

9. <em>"ifconfig,ip link"</em> gibi komutlarla '<strong>ppp</strong>' arayüzünün aktif olup olmadığını ve IP alıp almadığını kontrol edin.

10. Buraya kadar sorunsuz ise routing işlemlerine geçelim.Routing işlemlerini birkaç farklı şekilde yapabiliriz.

Sadece belli IP'leri ya da tek IP'yi VPN ağınıza yönlendirmek isteyebilirsiniz.Örnek olarak sadece <strong>10.1.0.0/16</strong> şeklindeki IP bloğunu VPN ağına yönlendirmek isteyebilirsiniz.Bunun için aşağıdaki gibi routing yapabiliriz.
<code>
#  route add -net 10.1.0.0/16 gw 10.1.40.40</code>

Eğer tüm trafiği VPN üzerinden geçirmek istersek(bu aşama biraz karmaşık gelebilir ama değil!) aşağıdaki gibi routing yapabiliriz;

<code># route add 195.202.46.45 gw 192.168.2.1 wlan0</code>

Burada "195.202.46.45" VPN sunucumuzun Public IP'si."192.168.2.1" ise internete bağlı olduğumuz öntanımlı ağ geçidimiz(Kendi ağ geçidinizi öğrenmek için 
<code># route -n |grep "^0\.0\.0\.0" |awk '{print $2}'</code>
komutunu kullanabilirsiniz.)"wlan0" ise internete bağlı olduğumuz arabirimimiz.Yukardaki komutu verdikten sonra mevcut öntanımlı ağ geçidimizi routing tablosundan silelim.
<code>
# route del default gw 192.168.2.1</code>

ve "<strong>ppp</strong>" arayüzünde gördüğümüz VPN sunucunun IP adresini öntanımlı ağ geçidi olarak ayarlayalım.
<code>
# route add default gw 10.1.40.40</code>


Bu adımdan sonra tüm trafiği VPN üzerinden geçirebilirsin.

11.VPN bağlantısını kesmek için;

<code># ipsec auto --down L2TP-PSK
# echo "d vpn-connection" &gt; /var/run/xl2tpd/l2tp-control
# /etc/init.d/ipsec stop
# /etc/init.d/xl2tpd stop
# route del 195.202.46.45 gw 192.168.2.1 wlan0
# route add default gw 192.168.2.1</code></body></html>