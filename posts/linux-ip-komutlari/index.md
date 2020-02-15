<html><body><a href="http://img694.imageshack.us/img694/9539/30112008network1.jpg"><img title="Linux IP komutları" src="http://img694.imageshack.us/img694/9539/30112008network1.jpg" alt="" width="336" height="239"></a>

Linux'de bazı önemli ip komutları;
<pre><strong>Sisteminizdeki ağ arabirimlerini ve özelliklerini göstermek :</strong> $ ifconfig</pre>
<pre><strong>Kullandığınız ağ arabiriminin özelliklerini göstermek :</strong> $ ifconfig eth0</pre>
<pre><strong>Ip atamak :</strong> $ ifconfig eth0 192.168.1.2</pre>
<pre><strong>Ping :</strong> ping -c 3 192.168.1.1</pre>
<pre><strong>Multiple Ip atamak:</strong> $ ifconfig eth0:0 192.168.1.2</pre>
<pre><strong>İkinci bir Ip atamak:</strong> $ ifconfig eth0:1 192.168.1.3</pre>
<pre><strong>Ağ arabirimin devredışı bırakmak:</strong> $ ifconfig eth0 down</pre>
<pre><strong>Ağ arabirimini aktif etmek:</strong> $ ifconfig eth0 up</pre>
<pre><strong>Routing IP tablosunu gösterme:</strong> $ route "veya" route -n</pre>
<pre><strong>Arp cache'i gösterme:</strong> $ arp "veya" arp -n</pre>
<pre><strong>IP/Subnet atamak:</strong> $ ifconfig eth0 192.168.1.2 netmask 255.255.255.0</pre>
<pre><strong>Default gateway atamak:</strong> $ route add default gw 192.168.1.1</pre>
<pre><strong>Ip yolunu gösterme(Traceroute):</strong> $ traceroute webs.homelinux.com</pre>
<pre><strong>Tracepath:</strong> $ tracepath webs.homelinux.com</pre>
<pre><strong>DNS test:</strong> $ host webs.homelinux.com</pre>
<pre><strong>Gelişmiş DNS test:</strong> $ dig webs.homelinux.com</pre>
<pre><strong>Reverse lookup:</strong> host 74.125.43.105</pre>
<pre><strong>Gelişmeiş Reverse lookup:</strong> dig -x 74.125.43.105
</pre>
NOT: Bazı komutlar ve değişiklik yapmak için root yetkisi gerekmektedir.

Daha ayrıntılı bilgi için <a href="http://www.whatismyip.com/faq/linux-ip-commands.asp">buradan</a> .</body></html>