<html><body><p>Sistem üzerinde tam denetim sağlamak özellikle güvenlik açısından çok önemlidir.Çünkü herhangi bir saldırı sadece dışardan değil , içerden de gelebilir ve ya kullanıcı sistem üzerinde zararlı bir program çalıştırabilir.İşte bu nokta da kullanıcıları ve süreçleri  kontrol altında tutmak gerekir.

GNU/Linux üzerinde "<a href="http://www.gnu.org/software/acct/" target="_blank"><strong>acct</strong></a>" (<em>GNU Accounting Utilities</em> ) adlı araçla kullanıcı ve süreçleri izleyebiliriz.İlk olarak eğer sistem üzerinde "<strong>acct</strong>" kurulu değil ise kurulumunu yapalım.
</p><pre># yum install psacct ( CentOS için )</pre>
Diğer bazı dağıtımlarda "<strong>psacct</strong>" yerine "<strong>acct</strong>" yazarak kurabilirsiniz.Örneğin ;
<pre># emerge acct   (Gentoo için)</pre>
<pre># yum install acct ( Suse için )</pre>
Kurulum yaptıktan sonra "<strong>/var</strong>" dizini altında "<em>account</em>" adlı bir klasör ve bu klasörün içinde "<em>pacct</em>" adlı dosya oluşturması gerekir.Eğer bu klasör ve dosyayı oluşturmamışsa elle oluşturalım.
<pre># mkdir /var/account</pre>
<pre># touch /var/account/pacct</pre>
<pre># chmod 660 /var/account/pacct</pre>
Süreç kayıtlarını aktif hale getirelim.
<pre># accton /var/account/pacct</pre>
"<strong>acct</strong>" uygulamasını başlangıça ekleyelim ve çalıştıralım.( <em>CentOS</em> )
<pre># chkconfig psacct on</pre>
<pre># service psacct start</pre>
Artık "<strong>acct</strong>" uygulaması ile gelen bazı yararlı komutları inceleyelim."<strong>ac</strong>" komutu ile başlayalım."<strong>ac</strong>" komutu kullanıcının sistem üzerinde ne kadar süredir bağlı kaldığını gösterir.
<pre> # ac
 total      537.71
</pre>
Yukarda görüldüğü gibi "<strong>ac</strong>" komutu hiç bir parametre almadan sadece komutu veren kullanıcının ne kadar süre sistemde olduğunu gösteriyor.Eğer sistem üzerinde tüm kullanıcıların ne kadar süre sistem üzerinde olduklarını görmek için ise "<strong>-p</strong>"(people)  parametresi kullanıyoruz.
<pre># ac -p
 ares                           537.95</pre>
<pre> zeus                           100.00
 total      637.95</pre>
* İkinci yararlı komutumuz ise "<strong>lastcomm</strong>" . "<strong>lastcomm</strong>" komutu ile hangi komutu kim,ne zaman,nerede verildiği hakkında bilgi verir.
<pre># lastcomm</pre>
<pre>grep                   root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
sed                    root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
sed                    root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
grep                   root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
sed                    root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
sed                    root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
grep                   root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
sh                F    root     pts/0      0.00 secs Fri Jan 21 06:56
sed                    root     pts/0      0.00 secs Fri Jan 21 06:56
</pre>
"<strong>lastcomm</strong>" komutu parametresiz sistem üzerinde verilen tüm komutları listeler.Eğer belli bir kullanıcının verdiği komutları görmek istersek "<strong>lastcomm</strong>" komutundan sonra "<strong>kullanıcı adı</strong>"nı yazıyoruz.
<pre># lastcomm ares</pre>
<pre>bash                   ares pts/1      0.02 secs Fri Jan 21 03:46</pre>
<pre>clear                  ares pts/1      0.00 secs Fri Jan 21 04:43</pre>
<pre>bash              F    ares pts/1      0.00 secs Fri Jan 21 04:43</pre>
<pre>bash              F    ares pts/1      0.00 secs Fri Jan 21 04:43</pre>
<pre>bash                   ares pts/0      0.04 secs Thu Jan 20 19:39</pre>
<pre>clear                  ares pts/0      0.00 secs Fri Jan 21 04:43</pre>
<pre>ssh                    ares pts/1      0.03 secs Fri Jan 21 03:46</pre>
<pre>firefox              X ares __       1860.00 secs Thu Jan 20 16:24</pre>
<pre>plugin-containe        ares __       454.73 secs Thu Jan 20 16:24</pre>
<pre>task1                X ares __         0.35 secs Fri Jan 21 04:35</pre>
<pre>gnome-panel       F    ares __         0.00 secs Fri Jan 21 04:35</pre>
<pre>xauth            S     ares pts/0      0.00 secs Fri Jan 21 04:31</pre>
<pre>whoami                 ares pts/0      0.00 secs Fri Jan 21 04:31</pre>
<pre>uname                  ares pts/0      0.00 secs Fri Jan 21 04:31</pre>
<pre>uname                  ares pts/0      0.00 secs Fri Jan 21 04:31</pre>
* Diğer bir komut ise "<strong>sa</strong>" . "<strong>sa</strong>" komutu ile kayıt altına komutları ve bu komutların kaç defa çalıştırıldığını gösterir.
<pre># sa</pre>
<pre>8014       0.16re       0.00cp         0avio      4475k   mv</pre>
<pre> 5495       0.01re       0.00cp         0avio      2052k   dirname</pre>
<pre> 5484       0.78re       0.00cp         0avio      5707k   libtoolize*</pre>
<pre> 4377       0.18re       0.00cp         0avio      2071k   stty</pre>
<pre> 3621       0.02re       0.00cp         0avio      3445k   touch</pre>
<pre> 3258       0.09re       0.00cp         0avio      2326k   tr</pre>
<pre> 3214       0.14re       0.00cp         0avio      2319k   mkdir</pre>
<pre> 3055       0.01re       0.00cp         0avio      3365k   true</pre>
<pre> 2711       7.00re       0.00cp         0avio      2251k   collect2</pre>
<pre> 2687       0.13re       0.00cp         0avio      2658k   head</pre>
<pre> 2557       0.01re       0.00cp         0avio      2034k   expr</pre>
<pre> 2118       0.28re       0.00cp         0avio      2752k   sort</pre>
<pre> 1868       0.00re       0.00cp         0avio      2183k   uname</pre>
<pre> 1860       0.08re       0.00cp         0avio      5617k   autoconf-2.65*</pre>
<pre> 1610       0.09re       0.00cp         0avio     17421k   python2.6*</pre>
<pre> 1466       0.02re       0.00cp         0avio      1894k   ln</pre>
<pre> 1320       0.00re       0.00cp         0avio      3721k   chgrp</pre>
<pre> 1225       0.00re       0.00cp         0avio      5547k   shtool*</pre>
"acct" ile gelen diğer bazı komutlar ise ;

<strong>last =</strong>Sisteme en son giriş yapan kullanıcılar listeler.

<strong>dump-acct =</strong> Kayıt dosyasını okunabilir  şekilde ekrana yazdırır.

"<strong>acct</strong>" ve komutları hakkında daha fazla bilgi için man sayfalarına ve <a href="http://www.gnu.org/software/acct/manual/html_chapter/accounting.html" target="_blank">şuraya</a> bakabilirsiniz.</body></html>