<html><body><p>Bilgisayarımıza kurmak istediğimiz herhangi bir dağıtımın ".iso" uzantılı cd ya da dvd kalıbı indirdiniz.Fakat bunun için cd ya da dvd harcama niyetinde değil de,"usb flash belleğim var ben bununla kurulum yapmak istiyorum" diyorsanız aşağıdaki adımları izleyin.

<strong>1-</strong> İlk olarak sistem üzerindeki flash diskimizi görelim.

# <em>fdisk -l</em>

bu komutun çıktısına göre sisteminize bağlı "/dev/sdX" şeklinde bir usb flash belleğin bağlı olduğunu göreceksiniz.Ben ön tanımlı olarak "/dev/sda" olarak alacam.

<strong>2-</strong>Flash belleğimiz "/dev/sda" noktasına bağlı.Bu bölüm sisteme bağlı ise kaldıralım ve flash bellekte bulunan bölümleri silip,boot sektör oluşturalım.

#<em>umount /dev/sda1</em>

# <em>dd  if=/dev/zero of=/dev/sda count=1024</em>

<strong>3-</strong>Flash bellekte yeni bir bölüm oluşturalım.Fdisk yazılımını kullanmasını az buçuk aşina olmanız lazım.

#<em> fdisk /dev/sda </em>(Bu komuttan sonra sırayla aşağıdaki adımları uygulayın!)

<em>&gt;p</em>

<em>&gt;n  , p , 1 , enter enter</em>

<em>&gt;p</em>

<em>&gt;a ,1</em>

<em>&gt;p</em>

<em>&gt;w</em>

<strong>4-</strong> Yukardaki adımdan sonra flash bellek üzerinde "/dev/sda1" bölümünü oluşturduk ve bu bölümü şimdi ext2 ile şekillendirelim.

#<em>mkfs.ext2 /dev/sda1</em>

#<em>tune2fs -i 0 /dev/sda1</em>

5-Bu adımda flash belleğimize "mbr" yükleyecez fakat daha önceden sisteminizde "syslinux" adlı yazılımın bulunması lazım.Eğer yoksa paket yöneticisi yardımıyla hemen indirin.(Örnek: " apt-get install syslinux" "emerge syslinux" )

# <em>cat /usr/share/syslinux/mbr.bin &gt; /dev/sda</em>

6-İndirdiğimiz iso kalıbını ve flash belleğimizi sisteme bağlayalım.(Not:Ben indirdiğimiz iso kalıbına örnek olarak "debian-5.0.iso" adını verdim.Siz indirdiğiniz iso kalıbının adı ve bilgisayarınızdaki yolu neyse onu yazacaksınız.

# <em>mkdir /mnt/flash</em>

# <em>mkdir /mnt/iso</em>

# <em>mount -t ext2 /dev/sda1 /mnt/flash</em>

$<em>mount -t iso9660 -o loop,user /home/user/downloads/debian-5.0.iso /mnt/iso</em>

<strong>7-</strong> iso kalıbının içindekileri usb flash belleğimize kopyalım.

#<em>cd /mnt/flash</em>

#<em>cp -r /mnt/iso/* /mnt/flash</em>

<strong>8-</strong>İso kalıbının usb flash bellekten yüklenebilmesi için birkaç düzeltme ve bootloader yükleyelim.

# <em>mv isolinux extlinux</em>

#<em>mv extlinux/isolinux.cfg extlinux/extlinux.conf</em>

#<em>rm extlinux/isolinux.bin</em>

# <em>cd ..</em>

# <em>extlinux -i /mnt/flash/extlinux</em>

<strong>9-</strong>Bu adıma kadar hata almadan gelebilmişseniz herşey doğru ve artık usb flash bellekten kuruluma hazırdır.Bunun içinde ilk önce flash belleğimizi sistemden ayırıp,daha sonra kendiniz biostan usb 'den boot seçeneğini aktif ederek kuruluma başlayabilirsiniz.

# <em>umount /mnt/flash</em>

Kolay gelsin :)</p></body></html>