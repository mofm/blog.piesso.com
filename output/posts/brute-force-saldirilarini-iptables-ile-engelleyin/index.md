<html><body><strong>Brute Force saldırısı</strong><em>(Brute Force Attack)</em> diğer bir deyişler <strong>Anahtar Arama Saldırısı</strong> <em>( exhaustive key search)</em> hedefin özel alanlara sızmak için deneme- yanılma yolu o servise  ulaştıracak giriş bilgilerini tespit edip sisteme sızma  saldırılarıdır.Ayrıntılı bilgi için bakınız <a href="http://en.wikipedia.org/wiki/Brute-force_attack" target="_blank">***</a>

Sunucular internet dünyasına açıldığı takdirde bu tip saldırılardan  nasibini alması kaçınılmazdır.Örnek bir “brute force” saldırısı:
<pre>May 05 01:23:23 zeus sshd[12355]: Illegal user office from 2**.1**.**.***
May 05 01:23:33 zeus sshd[12755]: Failed password for illegal user office from 2**.1**.**.*** port 53033 ssh2
May 05 01:24:10 zeus sshd[12857]: Illegal user samba from 213.191.74.219
May 05 01:24:16 zeus sshd[12357]: Failed password for illegal user samba from 2**.1**.**.*** port 53712 ssh2
May 05 01:24:19 zeus sshd[12659]: Illegal user tomcat from 2**.1**.**.***
May 05 01:24:25 zeus sshd[12459]: Failed password for illegal user tomcat from 2**.1**.**.*** port 54393 ssh2
May 05 01:24:34 zeus sshd[12361]: Illegal user webadmin from 2**.1**.**.***
Jul 28 01:24:43 zeus sshd[12361]: Failed password for illegal user webadmin from 2**.1**.**.*** port 55099 ssh2

Yukarda gördüğünüz gibi saldırgan rastgele kullanıcı adı ve parolalarla <strong>“ssh”</strong> servisine sızmaya çalışıyor.
Bu ve bu gibi brute saldırıları <em>iptables</em>‘e kural ekleyerek engellemeye çalışalım.
( <em>Daha  önceki bir yazıda ssh güvenliği ilgili not yazmıştım<a href="http://linux.piesso.com/sunucu-guvenligissh-ile-root-girisini-kapatin" target="_blank">**</a>O yazıya göz atabilirsiniz.</em>)
<br>


<pre>iptables -A INPUT -i eth0 -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
iptables -A INPUT -i eth0 -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 5 --rttl --name SSH -j DROP


Yukardaki iptables kurallarındaki “<strong>eth0</strong>” arayüzünü,”<strong>22</strong>”  portunu kendi sisteminizdeki göre düzenleyiniz.

Bu kuralda ssh  servisimizi 1 dakika içerisinde 5 defa giriş izni vermiş olduk.Eğer  5′ten fazla giriş olduğu takdirde

 iptables “ssh” ulaşımını  engelleyecek.Bu kuralın normal ssh ile bağlanan kullanıcılar için bir  zararı olmayacak 

fakat durmadan atak yapacak olan saldırganı  engelleyecektir.
 

<h3>SSHatter ile kendinize saldırın!</h3>

Şimdi koyduğumuz kuralı test edelim.Bu kuralı test etmek için kendi kendimize saldıralım.

”SSH” servislerine “<em>brute force attack</em>” yapmak için kullanılan <strong>“SSHatter”</strong>ı kullanarak koyduğumuz kuralı test edelim.

<strong>SSHatter</strong>‘ı “<em>freshmeat</em>” sitesinden edinebilirsiniz.<strong>SSHatter</strong>‘ı <a href="http://freshmeat.net/projects/sshatter/?branch_id=70781&amp;release_id=263196" target="_blank">indirin</a> .

SSHatter’i indirdikten sonra uygun bir yere açalım.
 
<code>$ tar zxvf  SSHatter-1.0.tar.gz</code>
 
SSHatter’ın  iki tane bağımlılığı bulunuyor.Bunlar <em>ForkManager</em> ve <em>Net-SSH-Perl</em> bunları paket yöneticisi ile indirebiliriz.
 
<code># emerge -av Parallel-ForkManager</code> ( Debian kullanıcıları #apt-get install libparallel-forkmanager-perl )
 
<code># emerge -av  net-ssh-perl</code>
 
Artık saldırıya hazırız.SSHatter dizinine geçelim.
 
<code>$ cd SSHatter-1.0/src/</code>
 
$ ls
 
Saldıraya başlamadan önce deneme yapacağı birkaç username belirleyelim.Bunun için “<em>users</em>” adlı bir dosya oluşturup 

içine ekleyelim.Her satıra bir kullanıcı adı yazın.
 
<code>$nano users</code>
 
elma
 
armut
 
erik
 
….. gibi örnek kullanıcı adları yazıp kaydedin.Şimdi hedefi  belirleyelim.Bunun için ise “targets” adlı 

bir dosya oluşturup içine  hedefi yazalım.
 
<code>$ echo 127.0.0.1 &gt; targets</code>
 
Zaten “src” dizininde “passwords” adlı bir dosyada örnek parolalar  bulunmakta,kendiniz ekleme de yapabilirsiniz.

Artık “brute force” atak  yapmaya hazırız fakat kendi kendimizi de banlamamak için “cron” a 5  dakika sonra 

“iptables” kurallarını sıfırlamasını söyleyelim.
<br>
<pre>*/5 * * * * /sbin/iptables -F
</pre>
Yukardaki satırı “cron”a eklemeyi unutmayın.Şimdi atağı başlatabiliriz.Örnek atak komutu:

<code>$ perl SSHatter.pl -x 1 -t targets -u users -p passwords</code>

Atak başladı ve 5 deneme girişinden sonra iptables tarafından  banlanması gerekir ve 5 dakika sonra bu kural iptal

olacak ve tekrar  erişime açılacak.

Bu eklediğimiz iptables kuralının her açılışta aktif  olmasını istiyorsanız basit script yazarak sistem açılışına

ekleyebilirsiniz.Eğer daha kolay yollar arıyorsanız<strong> fail2ban</strong> gibi yazılımlara bakabilirsiniz.

<a href="http://www.syslogs.org/centos-uzerinde-fail2ban-ile-brute-force-onlemi/" target="_blank">Bu sitede</a> fail2ban hakkında güzel bir yazı mevcut.</pre>
</pre></body></html>