<html><body><p>İlk önce eğer ağınızda veya evinizde "Opendns" kullanmıyorsanız hemen geçmenizi öneririm.OpenDns'e geçmek için dns adreslerinizi şöyle girmelisiniz:
</p><h4>208.67.222.222
208.67.220.220</h4>
Ev kullanıcılarının OpenDns'i daha sağlıklı kullanmaları için "ADSL modem"den DNS ayarlarından içindeki mevcut Telekom dnslerini silip Opendns serverın adresleri ile değiştirin.Böylece garanti bir şekilde her zaman dns adresinizi değiştirmek zorunda kalmayacaksınız.

Evinizde dinamik ip kullanıyorsanız ve OpenDns'in tüm nimetlerinden(istatistik,loglar,ve en önemlisi filtre gibi) faydalanmak istiyorsanız,değişen ip'mizi belli aralıklarla Opendns'e bildirmemiz gerekiyor.Opendns'in windows ve mac kullanıcıları için böyle bir "updater" programı hazırlamış ancak linux kullanıcıları için zaten var olan özelliklerinden olacaktır ki böyle bir şeye gerek duyulmamış.Şimdi gelelim Opendns'e ip'mizi belli aralıklarla göndermemize;

ilk olarak "ddclient" kuruyoruz.

$aptitude install ddclient (debian ve türevleri için)

Kurulumu tamamlandığında,hemen konfigurasyon dosyasını açıp editliyoruz.

$gedit /etc/ddclient.conf

Buraya aşağıdaki gibi kendi bilgilerinizi yazarak kaydediyoruz.
<pre>##
## OpenDNS.com account-configuration
##
use=web, web=whatismyip.org
server=updates.opendns.com
protocol=dyndns2
login=user_name #Opendns'e kaydolduğunuz kullanıcı adınız
password='123456' #Kullanıcı şifreniz
newset  #Opendns'te oluşturduğunuz ağ adınız</pre>
ve ddclient'ın kaç saniye bir ip'mizi güncellemesini istiyorsak aşağıdaki komutu giriyoruz.

<code>/usr/sbin/ddclient -daemon 300 -syslog #Buradaki 300 rakamı saniye sayısıdır.İstediğiniz saniye aralığı ile değiştirebilirsiniz.</code>

Artık rahatça internette gezinebilirsiniz.</body></html>