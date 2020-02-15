<html><body><p>"embdemid GNU/Linux" mobil internet araçları(Compal JAX 10,Aigo P8860,Aigo P8888) için emdebian tabanlı oluşturduğum bir embedded linux projesi."embdemid linux" usb flash belleklere kurulabilir.Compal ve Aigo MID'ler üzerinde kablolu ve kablosuz interneti mükemmel çalışan bir embedded dağıtım.Yakında bluetooth'u da tanıması üzerine çalışmalarım sürmekte. Eğer sizde bir MID'e sahipseniz mutlaka denemenizi tavsiye ediyorum."embdemid linux" MID için konfigure edildi fakat ufak birkaç değişiklikle tüm x86 platformlarında çalıştırabilirsiniz."embdemid linux"u sourceforge "<a href="http://sourceforge.net/projects/embdemid/" target="_blank">http://sourceforge.net/projects/embdemid/</a>" adresinden inderebilirsiniz.
</p><h3>Embdemid Linux'u USB Flash Belleğe Kurmak :</h3>
<strong>1-</strong> İlk olarak yukardaki adresten embdemid-0.0.1.tar.bz2(56 MB)   adlı dosyayı indirin ve açın;

$ <em>tar xjvf  embdemid-0.0.1.tar.bz2</em>

<strong>2-</strong> USB Flash belleğimizi yüklemeye hazır hale getirelim.(Minimum 180 MB alan gereklidir.)

# <em>su</em>

#<em> fdisk -l</em>

# <em>umount /dev/sda1 </em> (Eğer usb flask disk sisteme bağlıysa ayıralım.)

Ben örnek olarak "/dev/sda" aygıtını baz alarak anlatacağım.Sizin sisteminizde "/dev/sdX" şeklinde farklı olabilir,ona göre bu bölümleri değiştirmelisiniz.

# <em>fdisk /dev/sda</em>

&gt; d   (Bu komutla önceki bölümleri silelim.Eğer birden fazla bölüm varsa " d " ile hepsini silin.)

&gt;p  (Bu komutla flash diskte tüm bölümlerin silindiğine emin olun.)

&gt; n ,  p  ,  1 , enter , enter  (Bu komutları sırasıyla arda arda yapın.Unutmayın fdisk programının içindeyiz!)

&gt; p  (Bölümümüzün oluştuğuna emin olalım.)

&gt;w

<strong>3-</strong> Yukardaki adımları uyguladıysanız flash diskinizdeki bölümün hazır olması lazım ve bu bölümü ext2 ile şekillendirelim.

# <em>mkfs.ext2 /dev/sda1</em>

#<em> tune2fs -i 0 /dev/sda1</em>

<strong>4-</strong>USB Flash diskimizi sisteme bağlayalım.

# <em>mkdir /mnt/flash</em>

# <em>mount -t ext2 /dev/sda1 /mnt/flash</em>

<strong>5-</strong> İndirdiğimiz "embdemid-0.0.1" in içindekiler flash diske kopyalalım.

# <em>cp -r /nereye-indirdiyseniz-oranın-yolu/embdemid-0.0.1/* /mnt/flash</em>

<strong>6- </strong>Artık son olarak flash diske grub yükleyerek bitirelim.

# <em>echo '(hd0) /dev/sda' &gt; /mnt/flash/boot/grub/device.map</em> (Eğer sisteminizde Usb Flash disk  sizinde "/dev/sda" da  ise bu adımı yapmanıza gerek yok.

# <em>grub-install --root-directory=/mnt/flash /dev/sda</em>

<em>Öntanımlı olarak sistemde iki kullanıcı mevcut.Bu kullanıcılar ile sisteme giriş yapabilirsiniz.</em>

<strong><em>1- root</em></strong>

<strong><em>parola= embedded</em></strong>

<strong><em>2- linux</em></strong>

<em><strong>parola= 123456</strong>
</em>

Tüm adımlar bu kadar sisteminiz hazır, flash diski MID'e takarak test edebilirsiniz ,bol eğlenceler.

<strong><strong> </strong><strong> </strong></strong><strong><strong>
</strong></strong></body></html>