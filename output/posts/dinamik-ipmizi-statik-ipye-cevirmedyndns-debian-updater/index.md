<html><body><p>Evimizde kuracağınız serverda en büyük sorun ip'nin dinamik olmasıdır(eğer statik ip istememişseniz).Bu yüzden ihtiyacınız olan ilk şey dinamik dns servislerinden birine başvurmak ve böylece sunucumuza,bilgisayarımıza açık olduğu müddetçe uzaktan erişebileceksiniz.Fakat yinede sorun bitmiyor,bu seferde dinamik dns servislerinin ip adresini update sorunu ile karşılaşıyorsunuz.Aşağıda bunun çözümü mevcut:

Bilgisayarınıza bir apache server kurduğunuz,ya da  ssh ile her zaman bağlanmak istiyorsunuz;

ilk olarak dinamik dns servisine üye olalım.Size <strong>dyndns</strong> adlı servisi öneriyorum.Bu servisin sitesi burası <a href="http://www.dyndns.com">tıklayın</a>.

Daha sonra devamlı olarak değişen ip'mizin güncellenmesi için "<strong>ddclient</strong>" kuruyoruz.

bunun için konsoldan;
</p><pre>$ aptitude install ddclient</pre>
diyoruz ve konfigurasyon ekranı geldiğinde dyndns servisinde üye olduğumuz kullanıcı adı ve şifremizi giriyoruz.

Daha sonra <em>checkip.dyndns.com</em> seçeneğine evet deyip,ayrıca bir  <em>ppp0</em> seçeneğine de evet deyip manuel olarak dyndns

servisinden aldığımız host ismini yazıp konfigurasyonu kapatıyoruz.

Güncelleme aralığının <em>300 sn</em> olması normaldir, bu süre aralığını değiştirmezseniz olur,.Artık 300 sn aralığında ip adresiniz dinamik dns servisine

haber verilip güncelleniyor.Bu kadar hadi kolay gelsin.</body></html>