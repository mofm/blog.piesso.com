<html><body><img src="http://upload.wikimedia.org/wikipedia/en/2/24/Soldier_of_Fortune_Coverart.png" alt="Soldier Of Fortune">

Raven Software tarafından yapılan ve Activision tarafından dağıtılan "first-person-shooter" oyunu.(Ayrıntılı bilgi için <a href="http://en.wikipedia.org/wiki/Soldier_of_Fortune_%28video_game%29" target="_blank">buradan</a>).Bu oyununuzu Linux kurulu sisteminizde oynamak istiyorsanız,aşağıdaki adımları takip edin:
<strong>1.</strong> İlk olarak <a href="http://thepiratebay.org/torrent/3299227/Soldier_Of_Fortune_For_Linux_FULL_ISO" target="_blank">bu adresten </a>torrent dosyasını indirin.(Dosya büyüklüğü=613 MB)
<strong>2.</strong>Bir "Torrent programı" ile (önerim Transmission) bilgisayarınıza 'iso' dosyasını indirin.
<strong>3.</strong>İndirdiğiniz "iso" dosyasını sistemimize bağlayalım.Bunun içinde şu adımları uygulayın;

*$ <em>cd /mnt</em>

*$ <em>sudo mkdir iso</em>

*$ <em>sudo mount -o loop -t iso9660 </em>Soldier.Of.Fortune-Linux<em>.iso /mnt/iso/</em>

<em></em>
<strong>4.</strong>Böylece indirdiğimiz iso dosyasını "/mnt/iso" dizinine bağlamış olduk.Artık oyunu kurabiliriz.Yapmanız gereken tek şey ise;

*$cd /mnt/iso

*$<em>sudo sh setup.sh</em>
komutunu verip oyunu sisteminize yüklemek.Kurulum bitince;

*$ <em>sof </em>komutunu vererek oyuna başlayabilirsiniz.Oyun ilk açıldığı ekranda sizden CD Key isteyecektir.CD Key'inizde burada= BEN2-BAC7-BUZ6-JAD3-9742

NOT: Eğer sisteminiz "x86_64" ise yapmanız gereken :

"setup.sh" dosyasındaki aşağıdaki kısımı değiştirmektir.

<strong>Önceki:</strong>

DetectARCH()
{
status=1
case `uname -m` in
i?86) echo "x86"
status=0;;
*) echo "`uname -m`"
status=0;;
esac
return $status
}

<strong>Yeni:</strong>

DetectARCH()
{
status=1
case `uname -m` in
i?86) echo "x86"
status=0;;
*) echo "x86"
status=0;;
esac
return $status
}</body></html>