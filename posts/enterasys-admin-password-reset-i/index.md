<html><body><p>Enterasys kenar switchlerde üç tane öntanımlı kullanıcı bulunuyor : <strong>admin,rw,ro</strong> .Sistem üzerindeki en yetkili kullanıcı "admin"  adlı kullanıcıdır ve şöyle bir sıralama mevcuttur; admin &gt; rw &gt; ro ."ro" kullanıcısı switch üzerinde sadece okuma yapabilir.Hiçbir değişikliğe yetkisi yoktur.

Enterasys kenar switch üzerindeki "<em>admin</em>" kullanıcısının parolası unutulduysa I.metod<em> (bu metodla parolayı resetleyebilmeniz için "rw" kullanıcısı ile bağlanabilmeniz gereklidir.)</em> ile parola resetleme adımlarına geçelim ;
</p><h5><strong>1. Adım :</strong></h5>
Kenar Switch'e "rw" kullanıcısı ile telnet ya da ssh yoluyla bağlanalım.

 
<h5><strong>2.Adım:</strong></h5>
Switch üzerinde çalışan konfigurasyonun yedeğini alalım.( daha önce bu <a href="http://linux.piesso.com/enterasys-yedek-almak" target="_blank">yazıda </a>detaylı bahsetmiştim. )

# <strong>show config outfile configs/28102011</strong>

 
<h5><strong>3.Adım:</strong></h5>
Yedeğini aldığımız konfigurasyon dosyasını TFTP sunucumuza upload edelim.( daha önce bu <a href="../enterasys-yedek-almak" target="_blank">yazıda </a>detaylı bahsetmiştim. )

# <strong>copy configs/28102011 tftp://192.168.1.12/28102011 </strong><em>(kendi TFTP sunucu adresinizi yazın.)</em><strong> </strong>

 
<h5><strong>4.Adım:</strong></h5>
TFTP <strong>su</strong>nucusuna upload ettiğimiz yedeği herhangi bir editörle açalım ve aşağıdaki gibi olan "admin" kullanıcısına parola atanan konfigurasyon satırını dosyadan silelim,

set system login admin super-user enable password :4f543cb3af317e6d7d5aea1534345625d1435d80698760262972042a9c736e0c4e2d8b30d50a5c2661:

 
<h5>5.Adım:</h5>
Yukardaki satırı sildikten sonra dosyayı kaydedelim ve bu dosyayı switch'e yeni dosya ismiyle tekrar yükleyelim,

# <strong>copy tftp://<em>192.168.1.12</em>/<em>28102011</em> configs/<em>passconf</em></strong>

 
<h5><strong>6.Adım:</strong></h5>
Yeniden yüklediğimiz konfigurasyon dosyasının yüklenip yüklenmediğini kontrol edelim ve switch'i bu dosyadan yeniden konfigure edelim.

<em><strong># dir</strong></em>

<em><strong># configure configs/passconf</strong></em>
<h5>7.Adım :</h5>
"admin" kullanıcısının parolası bu şekilde sıfırlanmış oldu.Switch yeni açılınca kullanıcı adına "admin" yazıp ,parola kısmını "enter"layıp geçin.

<strong>
</strong></body></html>