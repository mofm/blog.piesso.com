<html><body><p>Debian ve türevlerinde "<em>apache2</em>" default  kurulumda <em>mod_rewrite</em> modülü deaktif olarak geliyor.Apache webserverda bu modülü aktif etmeyi kısaca anlatacağım.

ilk olarak apache webserver kurulu değilse hemen kuralım:
</p><pre>$ aptitude install apache2  (eğer ki apt-get kullanıyorsanız aptitude kullanmanızı tavsiye ederim.)</pre>
Şimdi apache server kurulumu tamamlandı.Hemen mod_rewrite modülünü aktif edelim:
<pre>$ updatedb (bu komutla locate veritabanını yenileyelim.)</pre>
Daha sonra
<pre>$locate mod_rewrite</pre>
bendeki sonuç şöyle : " <em>/usr/lib/apache2/modules</em> " birazdan bu yol bize lazım olacak.

Hemen <em>/etc/apache2/mods-enabled</em> dizinine geçelim ve "<em>rewrite.load</em>" adlı bir dosya oluşturalım.
<pre>$cd /etc/apache2/mods-enabled</pre>
<pre>$touch rewrite.load</pre>
Oluşturduğumuz rewrite.load adlı dosyamızın için aşağıdaki kodları yapıştırıyoruz.
<pre>" <code>LoadModule rewrite_module /usr/lib/apache2/modules/mod_rewrite.so " ==&gt; biraz önce öğrendiğimiz yol burada bizim işimizi görüyor.</code></pre>
Bu adımda da <em>/etc/apache2/sites-enabled</em> klasörüne geçelim ve "<em>000-default</em>" adlı dosyayı editleyelim.
<pre>$ cd /etc/apache2/sites-enabled</pre>
<pre>$ gedit 000-default</pre>
<strong> " Options Indexes FollowSymLinks MultiViews

AllowOverride None

Order allow,deny

allow from all "</strong>

ve bu dizideki " AllowOverride None" yerine "AllowOverride all" yapıyoruz.Yani yeni şekli şöyle olmalıdır:

<strong>" Options Indexes FollowSymLinks MultiViews

AllowOverride all

Order allow,deny

allow from all"</strong>

Son adımda apache serverımızı yeniden başlatıyoruz ve işlemimiz burada bitiyor.
<pre>$/etc/init.d/apache2 restart</pre>
Kolay gelsin.</body></html>