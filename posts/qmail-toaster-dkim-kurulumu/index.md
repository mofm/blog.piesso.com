<html><body><a href="http://www.qmailtoaster.com/" target="_blank"><img class="alignright" title="qmail" src="http://techyguru.com/images/kl-qmail-w.gif" alt="" width="200" height="163">QMail-Toaster</a> Mail sunucunuz üzerinde mailleri <a href="http://www.dkim.org/" target="_blank">DKIM</a>(<em>DomainKeys Identified Mail</em>) ile imzalamaya kısaca değineceğim.DKIM ile imzalamak mail sunucunuzdan çıkan her mailin gerçekten sizin sunucunuzdan çıktığını kanıtlamak için kullanılır.Özellikle bazı büyük mail sağlayıcıları yahoo,gmail bunu kullanmaktadır.

Qmail-Toaster üzerine <strong>DKIM</strong>'i kurmaya başalamadan önce eğer Centos(<em>ya da RHEL,FEDORA</em>) üzerine "rpmforge" deposunu eklemediyseniz hemen ekleyelim."RpmForge" ek deposunu eklemek için kendi dağıtım ve sürümünüze uygun rpmforge "rpm" paketini "<a href="http://dag.wieers.com/rpm/packages/rpmforge-release/" target="_blank">http://dag.wieers.com/rpm/packages/rpmforge-release/</a>" adresinden indirelim ve indirdiğimiz paketi kuralım.
<pre>$ wget <a href="http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm" target="_blank">http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm</a> (Centos 5 64 bit için)</pre>
<pre># rpm -i rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm</pre>
"RpmForge"  paketini kurduktan sonra paket depolarını güncelleyin.
<pre># yum update</pre>
Böylece depomuza "rpmforge" ek deposunu ekledik.Şimdi "DKIM" kurulumuna geçebiliriz.İlk QMail-Toaster'ın DKIM scriptlerini sisteme indirelim.

$ wget <a href="http://qmailtoaster.com/dkim.tgz" target="_blank">http://qmailtoaster.com/dkim.tgz</a>
<pre>$ tar zxvf dkim.tgz</pre>
<pre>$ cd  dkim</pre>
"dkim" paketini sisteme indirip,açtıktan sonra kurulum adımlarına devam edelim.Eksik perl paketlerini sisteme kuralım;(bazı paketler Centos dağıtım depolarında bulunmadığı için "rpmforge" ek depolarını kurmuştuk.Özellikle "perl-Mail-DKIM" paketi ve bağımlılıkları dağıtım deposunda bulunmuyor.)
<pre># yum install perl-XML-Simple perl-Mail-DKIM perl-XML-Parser</pre>
Eksik paketlerimizde kurulduysa bu adımda başarı ile tamamlandı.Artık "DKIM"i "QMail"e adapte edelim.Bunun için ise control dosyalarının olduğu bölüme "dkim" adlı bir dizin oluşturup içine "dkim" imzamızı oluşturalım.Aşağıdaki adımları sırayla takip edin;
<pre># mkdir /var/qmail/control/dkim</pre>
<pre># cp signconf.xml /var/qmail/control/dkim/</pre>
<pre># chown -R qmailr:qmail /var/qmail/control/dkim/</pre>
<pre># dknewkey /var/qmail/control/dkim/global.key &gt; /var/qmail/control/dkim/public.txt</pre>
<pre># perl -pi -e 's/global.key/dkim1/' /var/qmail/control/dkim/public.txt</pre>
<pre># qmailctl stop</pre>
Bu adımlardan sonra imzamızı oluşturduk ve en sonunda "qmail"i durdurduk,şimdi eski "qmail-remote" dosyasını "dkim" paketi ile gelen "qmail-remote" dosyası değiştirip izinleri ayarlayalım.
<pre># mv /var/qmail/bin/qmail-remote /var/qmail/bin/qmail-remote.orig</pre>
<pre># mv qmail-remote /var/qmail/bin</pre>
<pre># chmod 777 /var/qmail/bin/qmail-remote</pre>
<pre># chown root:qmail /var/qmail/bin/qmail-remote</pre>
<pre># qmailctl start</pre>
Buraya kadar hiçbir hata ile karşılaşmadıysanız "DKIM" başarı ile kuruldu ve artık geriye sadece dns'imize oluşan TXT kaydını eklemek kaldı.
<pre>$ cat /var/qmail/control/dkim/public.txt</pre>
Yukardaki komuttan sonra çıkan <strong>TXT </strong>kaydını DNS Zone dosyanızda yayınlayın.Tüm adımlar bu kadar.Artık mailleriniz "DKIM" ile imzalanacak.

<a href="http://wiki.qmailtoaster.com/index.php/How_to_Setup_DKIM_with_Qmail_Toaster" target="_blank">How to setup DKIM with qmail-toaster</a></body></html>