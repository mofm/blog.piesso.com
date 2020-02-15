<html><body><p>Güvenlik politikası olarak belirsizliği seviyorsanız sunucularınızın üstünde çalışan uygulamaların kimliklerini dışa vermemelerini istiyorsunuzdur.Daha önceki bir yazıda kısaca <a href="http://linux.piesso.com/sunucu-kimligi-maskeleme" target="_blank">Apache Web Sunucusunun kimliğini gizleme</a>den bahsetmiştim, bu yazıda da DNS sunucumuzun versiyonunu maskelemeden bahsedeceğim.

Sunucumuzu maskelemeden önce dışarıya karşı ne gibi bilgiler veriyor bakalım :
</p><pre><strong>$ dig @ns1.mydomain.com -c CH -t txt version.bind</strong></pre>
<pre>
; &lt;&lt;&gt;&gt; DiG 9.7.2-P2 &lt;&lt;&gt;&gt; @ns1.mydomain.com -c CH -t txt version.bind</pre>
<pre>; (1 server found)</pre>
<pre>;; global options: +cmd</pre>
<pre>;; Got answer:</pre>
<pre>;; -&gt;&gt;HEADER&lt;&lt;- opcode: QUERY, status: NOERROR, id: 64071</pre>
<pre>;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 0</pre>
<pre>;; WARNING: recursion requested but not available</pre>
<pre>
;; QUESTION SECTION:</pre>
<pre>;version.bind.            CH    TXT</pre>
<pre>
;; ANSWER SECTION:</pre>
<pre>version.bind.        0    CH    TXT    <strong>"9.2.4"</strong></pre>
<pre>
;; AUTHORITY SECTION:</pre>
<pre>version.bind.        0    CH    NS    version.bind.</pre>
<pre>
;; Query time: 84 msec</pre>
<pre>;; SERVER: 00.00.00.00#53(00.00.00.00)</pre>
<pre>;; WHEN: Thu Jan 27 20:58:38 2011</pre>
<pre>;; MSG SIZE  rcvd: 62</pre>
Yukarda görüldüğü gibi <strong>Bind DNS</strong> sunucusu öntanımlı olarak dışarıya  kendi ve versiyonu ile ilgili bilgileri vermektedir.Bind DNS sunucumuzun versiyonu "9.2.4" müş.Kimliğimizi dışarıya vermemek ya da yanıltmak için "named.conf" dosyamızın içindeki "options" kısmına "version" satırını ekleyerek kimliğimizi dışarıya karşı maskeleyelim."version" satırı için istediğimiz bir isim ekleyebiliriz.
<pre><strong># vi /var/named/chroot/etc/named.conf</strong></pre>
options {
directory "/var/named";
dump-file "/var/named/data/cache_dump.db";
statistics-file "/var/named/data/named_stats.txt";
recursion no ;
allow-transfer { none; };
dnssec-enable yes;
<strong>version "DNS Server" ;</strong>

Sunucumuzu yeniden başlatalım :
<pre><strong># /sbin/service named restart</strong>
</pre>
Yukarda görüldüğü gibi "<em>options</em>" kısmına " <em>version "DNS Server" ; </em>" satırını ekledik.DNS sunucumuzun versiyonunu tekrar sorgulattığımızda artık bize "<strong>DNS Server</strong>" adını göstermesi lazım.
<pre> <strong>$ dig @ns1.mydomain.com -c CH -t txt version.bind
</strong>
; &lt;&lt;&gt;&gt; DiG 9.7.2-P2 &lt;&lt;&gt;&gt; @ns1.mydomain.com -c CH -t txt version.bind
; (1 server found)
;; global options: +cmd
;; Got answer:
;; -&gt;&gt;HEADER&lt;&lt;- opcode: QUERY, status: NOERROR, id: 29215
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;version.bind.            CH    TXT

;; ANSWER SECTION:
version.bind.        0    CH    TXT    "DNS Server"

;; AUTHORITY SECTION:
version.bind.        0    CH    NS    version.bind.

;; Query time: 110 msec
;; SERVER: 00.00.00.00#53(00.00.00.00)
;; WHEN: Thu Jan 27 21:11:16 2011
;; MSG SIZE  rcvd: 60
</pre>
Artık DNS sunucumuz versiyon bilgisi vermiyor.Onun yerine yazmış olduğumuz "<strong>DNS Server</strong>" yazısını ekrana yazıyor.Sadece bunu yaparak DNS sunucumuzu güvende mi tutuyoruz?Elbetteki hayır! Şu an sadece sunucumuzun versiyonunu maskelemiş olduk.Yoksa  maskeleyemedik mi ???

Aslında tam olarak da maskeleyemedik."<a href="http://code.google.com/p/fpdns/" target="_blank"><strong>Finger print DNS</strong></a> " yazılımı ile kolayca sunucumuzun kimliğini ifşa edebilirler.Kimse etmeden ilk biz deneyelim."<strong>fpdns</strong>" yazılımı neredeyse her dağıtımın deposunda mevcut.Hemen bu yazılımı kuralım:
<pre><strong># yum install fpdns</strong></pre>
"fpdns" yazılımını kurduktan sonra sunucumuzu sorgulatalım.
<pre><strong>$  fpdns ns1.mydomain.com</strong></pre>
<pre>fingerprint (ns1.mydomain.com, 00.00.00.00): BIND 9.2.3rc1 -- 9.4.0a0</pre>
Yukarda görüldüğü gibi demek ki çok da iyi saklayamamışız :)</body></html>