<html><body><p>Eğer engellemediyseniz uzaktaki kişiler sunucunuzun uptime süresini öğrenebilirler.Uptime sürenizi öğrenmek isteyen kişi ,sisteme herhangi bir TCP paketi yollayarak sizin sisteminizden cevap bekler.Sistemimizde "timestamps" engellenmemişse bizim cevap göndereceğimiz TCP paketlerinin başlıklarında "<strong>timestamps</strong>"ler ( zaman imzamız ) bulunmakta.Buradaki "timestamps"leri okuyarak   sistemimizin uptime süresini öğrenebilirler.

Uptime süresini öğrenmek için bir çok uygulama mevcut : nmap,hping  gibi.<a href="http://www.hping.org/" target="_blank">Hping</a> ile hedef sistem üzerinde  istediğimiz porta istediğimiz paketi gönderebildiğimiz için onu kullanarak test yapacağım.Bilgisayarınızda "<strong>hping</strong>" yazılımı yüklü değilse ,ilk olarak kuralım.
</p><pre># emerge -av hping ( Gentoo )</pre>
<pre># apt-get install hping3 (Ubuntu )</pre>
Centos'a yüklemek için "<a href="http://fedoraproject.org/wiki/EPEL" target="_blank">EPEL</a>" deposunu eklemiş olmanız lazım.Eğer bu depoyu eklemediysen <a href="http://linux.piesso.com/epel-ve-rpmforge-depolarini-ekleyin" target="_blank">buradan</a> yardım alabilirsiniz.
<pre># yum install hping3</pre>
Hping yazılımını yükledikten sonra herhangi bir sunucunun uptime süresini öğrenmek bize cevap verecek herhangi bir <strong>TCP</strong> portuna bir istek gönderip,cevap alalım.Şimdi herhangi bir sunucunun uptime süresini öğrenelim:
<pre><strong># hping --tcp-timestamp www.examples.com -p 80 -c 2 -S</strong></pre>
<pre>HPING www.examples.com (eth0 00.00.00.00): S set, 40 headers + 0 data bytes
len=56 ip=00.00.00.00 ttl=55 DF id=0 sport=80 flags=SA seq=0 win=5792 rtt=20.0 ms
 TCP timestamp: tcpts=966942747

len=56 ip=00.00.00.00 ttl=55 DF id=0 sport=80 flags=SA seq=1 win=5792 rtt=19.8 ms
 TCP timestamp: tcpts=966942997
 HZ seems hz=100
 System uptime seems: 111 days, 21 hours, 57 minutes, 9 seconds

--- www.examples.com hping statistic ---
2 packets tramitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 19.8/19.9/20.0 ms</pre>
Yukardaki örnekte de görüldüğü gibi "<em>www.examples.com</em>" sunucusunun 111 gündür vs vs detaylı uptime süresini öğrenebiliyoruz.Uzaktaki sistemin "<strong>uptime</strong>" süresini öğrenmeye değindik,şimdi  "<em>kendi sunucumuzun uptime süresini vermesini istemiyorsak ne yapmalıyız</em>?" ona biraz değinelim.

Eğer sunucumuzun "<strong>timestamps</strong>" gönderip göndermediğini bilmiyorsak ona bakalım:
<pre><strong># /sbin/sysctl -a |grep tcp_timestamps </strong></pre>
<pre>net.ipv4.tcp_timestamps = 1</pre>
Yukardaki komutun çıktısına "<strong>net.ipv4.tcp_timestamps = 1</strong>" değeri alıyorsanız , uptime süre bilginiz öğrenebilinir demektir.Bu bilgiyi dışarıya vermemek için "<strong>1</strong>" değerini "<strong>0</strong>" yapalım.

<strong>I .Yöntem :</strong>
<pre>#  echo 0 &gt; /proc/sys/net/ipv4/tcp_timestamps</pre>
<strong>II.Yöntem :</strong>

Bu yöntemde ise "<em>sysctl.conf</em>" dosyasına "<em>net.ipv4.tcp_timestamps = 0</em>" satırını ekleyelerek yapabiliriz.
<pre><strong># vi /etc/sysctl.conf</strong></pre>
Aşağıdaki satırı ekleyin:
<pre><strong>net.ipv4.tcp_timestamps = 0</strong></pre>
Satırı ekledikten sonra dosyayı kaydedip,kapatın.Ayarların aktif olabilmesi için bilgisayarı <strong>yeniden başlatın</strong> ya da aşağıdaki komutu verin .
<pre><strong># sysctl -p</strong></pre>
Yeni ayarlarımız aktif olduktan sonra uptime bilgimizin gönderilip,gönderilmediğini test edelim.
<pre><strong># hping --tcp-timestamp www.examples.com -p 80 -c 2 -S</strong></pre>
<pre>HPING www.examples.com (eth0 00.00.00.00): S set, 40 headers + 0 data bytes
len=44 ip=00.00.00.00 ttl=64 DF id=0 sport=80 flags=SA seq=0 win=32792 rtt=0.1 ms
 TCP timestamp: tcpts=0

len=44 ip=00.00.00.00 ttl=64 DF id=0 sport=80 flags=SA seq=1 win=32792 rtt=0.1 ms
 TCP timestamp: tcpts=0
</pre>
<pre>--- www.examples.com hping statistic ---</pre>
<pre>2 packets tramitted, 2 packets received, 0% packet loss</pre>
<pre>round-trip min/avg/max = 0.1/0.1/0.1 ms</pre>
Artık sunucumuz dışarıya uptime bilgisi vermiyor.Birde şuna değinmek istiyorum.Eğer "<strong>icmp</strong>" isteklerini engellememişseniz bu yolla da "<strong>timestamp</strong>s" bilginiz öğrenilebilinir."icmp" ile dışarıya "timestamps" göndermek istemiyorsanız özetle <strong>iptables</strong> ile bunu engelleyebilirsiniz.Örnek olarak :
<pre>   ipchains -A input -p icmp --icmp-type timestamp-request -j DROP</pre>
<pre>   ipchains -A output -p icmp --icmp-type timestamp-reply -j DROP</pre></body></html>