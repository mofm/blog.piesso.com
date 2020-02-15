<html><body><p>Debian'nın son kararlı sürümü 6.0 Squeeze çıkmasına üzerine birçok kişi de yükseltme hevesinde.Tabi önemli olanda yükseltme işini güvenli ve kayıpsız olarak sapasağlam yapabilmek.

Sürümümüzü yükseltmeye geçmeden önce olabilecek herhangi bir arızaya karşın önemli olan tüm dosya ve dizinleri yedekleyin.Bu yedeklerin içine önemli kofigurasyon dosyalarınıza da eklemeyi unutmayın.

İlk olarak mevcut olan Lenny'i güncelleyelim ve daha sonra Squeeze sürümüne yükseltelim.

# vi /etc/apt/sources.list

Debian depo kaynak adreslerinin olduğunu "sources.list" dosyasını kontrol edelim ve içindeki depo adreslerinin aşağıdaki gibi olup olmadığını gözden geçirin:
</p><pre>deb http://ftp.tr.debian.org/debian/ lenny main contrib non-free
deb-src http://ftp.tr.debian.org/debian/ lenny main contrib non-free
deb http://security.debian.org/ lenny/updates main
deb-src http://security.debian.org/ lenny/updates main
deb http://volatile.debian.org/debian-volatile lenny/volatile main
deb-src http://volatile.debian.org/debian-volatile lenny/volatile main 

Kaynak adreslerini kontroldan sonra Lenny'i güncelleyelim.

# apt-get update
# apt-get upgrade
# apt-get dist-upgrade

Lenny'i güncelleme adımları tamamlandıktan sonra herhangi bir soruna karşın yükseltilmeyecek ya da
tam yüklenmemiş paketlerin olup olmadığını kontrol edelim.

# dpkg --audit
# dpkg --get-selections | grep hold

</pre></body></html>