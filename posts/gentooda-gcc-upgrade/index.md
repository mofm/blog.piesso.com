<html><body><p>Gentoo'da "GCC" upgrade işlemi dikkatli yapılması ve aynı zamanda kolay yapılabilen bir işlemdir.Aşağıdaki adımları izleyerek sisteminizde "GCC" sürümünü başarıyla yükseltebilirsiniz.

<strong>1.</strong>İlk olarak yeni "GCC" sürümünü sistemimize yüklüyoruz;

$# <em>emerge -uav gcc</em>

<strong>2.</strong>Yeni "GCC" sürümü sisteme yüklendikten sonra önceki sürümü veya sürümleri ile beraber birden çok "gcc" olduğuna göre yeni sürümü aktif derleyici olarak seçmemiz lazım;

$# <em>gcc-config -l </em> (Sisteminizde bulunan GCC sürümlerinin listesini verir.)
$# <em>gcc-config i686-pc-linux-gnu-4.4.3</em> (Yeni GCC sürümü 4.4.3 ise ,CHOST ayarının sonuna GCC sürüm numarasını ekleyip seçiyoruz.)
$# <em>env-update &amp;&amp; source /etc/profile</em>

<strong>3.</strong>{Şartlı Madde} Eğer GCC sürümünü 3.* bir versiyondan 4.* bir versiyona yükseltecekseniz aşağıdaki yapmalısınız;

$# <em>/usr/share/gcc-data/$CHOST//fix_libtool_files.sh 3.4.6</em> (Eski sürümünüz 3.4.6 ise,varsayılan 3.4.6 alınmıştır. )

<strong>4.</strong>"libtool"u yeniden kuruyoruz;

$# <em>emerge --oneshot -av libtool</em>

<strong>5.</strong>Son olarak ise sistemimizin güvenle ve sorunsuz çalışması için yeni yüklenen derleyici ile tüm sistemi yeniden derliyoruz.Bu sisteminize göre uzun zaman alabilir;

$# <em>emerge -eav system</em>
$# <em>emerge -eav world</em>

<strong>NOT:</strong> Eğer sisteminizin yeniden derlenme sürecinde bir hata ile karşılaşırsanız,

$# <em>emerge --resume</em>

komutuyla derlenmeye kaldığı yerden başlatabilirsiniz.Fakat hala aynı paket aynı hatayı veriyor ve derlenmeye devam etmiyorsa, aşağıdaki komutla o paketi atlayıp derlemeye devam ettirebilirsiniz.

$# <em>emerge --resume --skipfirst</em>

Tüm adımlar sorunsuz tamamlanıp,eski "GCC" sürümünü güvenle kaldırmak istiyorsanız;

$# <em>emerge -aC =sys-devel/gcc-3.4*</em> (kaldıracağınız eski sürüm 3.4 ile başlıyorsa,varsayılan olarak bu sürüm alınmıştır.
bu komutla kaldırabilirsiniz.

Ayrıntılı bilgi için <a href="http://www.gentoo.org/doc/en/gcc-upgrading.xml">Gentoo GCC Upgrade Guide</a></p></body></html>