<html><body><p>Bu yazıda debian'da xserver güncellemesi sonucu grafik arabiriminin çalışmamasından kaynaklanan sorunun çözümünü anlatacam."Debian sid" kullanıcıları  güncelleme yaptıktan sonra karşılarında sadece kara ekranla başbaşa kalabilirler.Ama üzülmeye hiç gerek yok.Sorunun çözümü çok basit.Yapmanız gerekenleri adımlarla anlatacam.</p>
<p><strong>Yapmanız gereken adımlar:</strong></p>
<p>1. Eğer güncelleme yaptıktan sonra xserver çalışmıyor ve aşağıdaki gibi kodlar veriyor ise;</p>
<pre>(E)Failed to load /usr/lib/xorg/modules/drivers/nvidia_drv.so</pre>
<pre>(E)Failed to load module "nvidia"(loader failed,7)</pre>
<pre>(E)No drivers available</pre>
<pre>Fatal server error:</pre>
<pre>no screen found</pre>
<p>Yukardaki gibi hata alıyorsanız.İlk önce geçici olarak xserver'ımızı çalıştıralım.Bunun içinse root olup aşağıdaki komutu yazalım;<!--more--></p>
<pre>$ nano -w /etc/X11/xorg.conf</pre>
<p>"xorg.conf" dosyası açılmış olacaktır.Bu dosya içinde " Device  "nvidia" " yazan yerdeki "nvidia" yerine "vesa" yazıyoruz.Kaydedip çıkıyoruz.</p>
<p>2. Ardından hemen xserver çalıştırıyoruz:</p>
<pre>$ startx  # bu komutla xserver'ı açıyoruz.</pre>
<p>3. Ekran karşımızda açıldıktan sonra "<a href="http://www.nvidia.com/Download/index.aspx?lang=en-us">Nvidia Driver Download</a>" adresine gidip kendi ekran kartımıza uygun driveri indiriyoruz.Yeni <em>Nvidia</em> sürücümüzü yüklemek için xserver'ı kapatıyoruz(yani çıkış yapıyorsunuz).Ve güzel kara ekranımızda "<em>Nvidia</em>" sürücüsünü indirdiğimiz dizine geçip root olarak yüklüyoruz.Yüklemek için aşağıdak komutu veriyoruz.</p>
<pre>$ sh NVIDIA-Linux-x86_64-173.14.22-pkg2.run --x-prefix=/usr/lib/xorg   #tabiki root olarak veriyoruz.</pre>
<p>ve bu komutu verdikten sonra yönergeleri izleyip kurulumu başarıyla tamamladıktan sonra bilgisayarımızı yeniden başlatıyoruz.</p>
<p>Kolay gelsin.Sorunlarınızı mail ya da yorumla bildirin.</p>
</body></html>