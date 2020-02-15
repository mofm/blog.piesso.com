<html><body><strong><img class="alignright" title="GRUB" src="http://upload.wikimedia.org/wikipedia/commons/1/19/KeePass_icon.png" alt="" width="154" height="154">İpucu:</strong> Sisteminizin güvenliği açısından bilgisayarın açılışında “<strong><strong>GRUB</strong></strong>” a <strong>parola</strong> koyma ihtiyacı duyabilirsin.Eğer “<strong>GRUB</strong>” a <strong>parola</strong> koymak istiyorsanız:

“<strong>/boot/<strong>grub</strong>/<strong>grub</strong>.conf”</strong> dosyasına ” <strong>password</strong> ” satırını ekleyelim.Ama password satırını eklemeden önce ekleyeceğimiz parolayı ‘md5′ kriptolayalım.

<code># <strong>grub</strong></code>

GNU <strong>GRUB</strong> version 0.97  (640K lower / 9216K upper memory)

[ Minimal BASH-like line editing is supported.  For the first word, TAB
lists possible command completions.  Anywhere else TAB lists the possible
completions of a device/filename. ]

<strong>grub</strong>&gt; md5crypt

Password: ******
Encrypted: $1$M1Gou/$U4rKvFwErxqZkpt9MiHYm0

<strong>grub</strong>&gt;

Yukarıda gördüğünüz gibi şifreleyeceğim parolayı yazıp ‘Encrypted’  halini aldım.Buradaki şifreli parolamı (  $1$M1Gou/$U4rKvFwErxqZkpt9MiHYm0 ) kopyalayıp “<strong>/boot/<strong>grub</strong>/<strong>grub</strong>.conf</strong>” dosyasındaki ‘<strong>password</strong>‘ satırına ekleyelim.

<code>password --md5 $1$M1Gou/$U4rKvFwErxqZkpt9MiHYm0</code>

Böylece artık “<strong>GRUB</strong>” ekranında belirlediğiniz <strong>parola</strong> ile giriş yapabileceksiniz.</body></html>