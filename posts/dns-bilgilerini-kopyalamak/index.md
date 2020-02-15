<html><body><p>Herhangi bir domain'in dns bilgilerini  ve o domainin subdomain'lerini "<em>AXFR</em>" protokolü ile dns sunucudan çekebiliriz.DNS Sunucu  üzerinde iki tür zone transferi vardır;

* Full Zone Transfer (AXFR)

* Incremental Zone Transfer (IXFR)

<strong>AXFR</strong> , DNS zone' ları arasındaki transferde tüm zone bilgilerinin alınarak güncellemenin gerçekleşmesinde kullanılan ve <span style="text-decoration: underline;"><em><strong><a href="http://sozluk.cozumpark.com/goster.aspx?id=1180&amp;kelime=incremental-zone-transfer-iXFR">incremental zone transfer (IXFR) </a></strong></em></span>protokolüne göre eski bir protokoldür.(<a href="http://sozluk.cozumpark.com/goster.aspx?id=1181&amp;kelime=full-zone-transfer-AXFR" target="_blank">**</a>)

AXFR protokolü hakkında detaylı  bilgi için , <a href="http://cr.yp.to/djbdns/axfr-notes.html" target="_blank">"How the AXFR protocol works"</a> - <em>D.J.Bernstein</em>

Şimdi örnek bir domainin bütün bilgilerini ve sahip olduğu subdomainleri dns sunucusundan çekelim;

İlk olarak bilgilerini almak istediğimiz domain'in yetkili "nameserver" bilgilerini alalım: <a href="http://linux.die.net/man/1/dig" target="_blank">('dig' komutu man sayfası)</a>
</p><pre><strong># dig zargan.com NS</strong></pre>
<pre>; &lt;&lt;&gt;&gt; DiG 9.8.1 &lt;&lt;&gt;&gt; zargan.com NS
;; global options: +cmd
;; Got answer:
;; -&gt;&gt;HEADER&lt;&lt;- opcode: QUERY, status: NOERROR, id: 3226
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;zargan.com.            IN    NS

;; ANSWER SECTION:
zargan.com.        3600    IN    NS    ns2.hayatbilgi.net.
zargan.com.        3600    IN    NS    ns1.hayatbilgi.net.

;; Query time: 542 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Thu Jan 12 23:17:03 2012
;; MSG SIZE  rcvd: 78
</pre>
zargan.com domain adresinin dns sunucuları <em>"ns1.hayatbilgi.net,ns2.hayatbilgi.net"</em> .Şimdi dns sunucularının herhangi birisinden domain bilgilerini çekelim:
<pre><strong># dig @ns1.hayatbilgi.net zargan.com axfr</strong></pre>
<pre>; &lt;&lt;&gt;&gt; DiG 9.8.1 &lt;&lt;&gt;&gt; @ns1.hayatbilgi.net zargan.com axfr
; (1 server found)
;; global options: +cmd
zargan.com.        3600    IN    SOA    ns1.hayatbilgi.net. hostmaster.hayatbilgi.net. 2009042370 900 600 86400 3600
zargan.com.        3600    IN    A    93.94.250.210
zargan.com.        3600    IN    NS    ns2.hayatbilgi.net.
zargan.com.        3600    IN    NS    ns1.hayatbilgi.net.
zargan.com.        3600    IN    MX    5 alt2.aspmx.l.google.com.
zargan.com.        3600    IN    MX    1 aspmx.l.google.com.
zargan.com.        3600    IN    MX    10 aspmx2.googlemail.com.
zargan.com.        3600    IN    MX    15 mail.zargan.com.
zargan.com.        3600    IN    MX    5 alt1.aspmx.l.google.com.
zargan.com.        3600    IN    MX    10 aspmx3.googlemail.com.
zargan.com.        3600    IN    TXT    "v=spf1 include:aspmx.googlemail.com ~all"
ns2.hayatbilgi.net.    3600    IN    A    93.94.249.3
ns1.hayatbilgi.net.    3600    IN    A    93.94.249.2
admin.zargan.com.    3600    IN    A    93.94.250.12
editor.zargan.com.    3600    IN    A    93.94.250.12
mail.zargan.com.    3600    IN    A    93.94.250.210
test.zargan.com.    3600    IN    A    93.94.250.12
www.zargan.com.        3600    IN    A    93.94.250.210
yeni.zargan.com.    3600    IN    A    93.94.250.12
www.yeni.zargan.com.    3600    IN    CNAME    yeni.zargan.com.
zenith.zargan.com.    3600    IN    A    93.94.250.12
zargan.com.        3600    IN    SOA    ns1.hayatbilgi.net. hostmaster.hayatbilgi.net. 2009042370 900 600 86400 3600
;; Query time: 519 msec
;; SERVER: 93.94.249.2#53(93.94.249.2)
;; WHEN: Thu Jan 12 23:20:51 2012
;; XFR size: 22 records (messages 22, bytes 1361)</pre>
Yukardaki çıktıda görüldüğü gibi bu protokol ile domain dns bilgilerini replike edebilirsiniz.</body></html>