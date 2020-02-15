<html><body><p style="text-align: left;"><img class="aligncenter" src="http://img.zamunda.net/bitbucket/Heroes%20of%20Might%20and%20Magic%20III%20The%20Restoration%20of%20Erathia%20Cover.jpg" alt="Heroes Of Might And Magic III" width="228" height="294">
Heroes Of Might And Magic Oyunu Linux kurulu sistemde oynamak istiyorsanız,yapmanız gereken aşağıdaki adımları izlemek ve böylece Linux'da hiç güzel oyun yok diyenleri şaşırtabilirsiniz.
<strong>1.</strong> İlk olarak <a href="http://thepiratebay.org/torrent/3299161/Heroes_Of_Might_And_Magic_3_Linux_ISO" target="_blank">bu adresten </a>torrent dosyasını indirin.(Dosya büyüklüğü=358 MB)
<strong>2.</strong>Bir "Torrent programı" ile (önerim Transmission) bilgisayarınıza 'iso' dosyasını indirin.
<strong>3.</strong>İndirdiğiniz "iso" dosyasını sistemimize bağlayalım.Bunun içinde şu adımları uygulayın;</p>
<p style="text-align: left;">*$ <em>cd /mnt</em></p>
<p style="text-align: left;">*$ <em>sudo mkdir iso</em></p>
<p style="text-align: left;">*$ <em>sudo mount -o loop -t iso9660 </em>HMM3-Linux.iso<em> /mnt/iso/</em></p>
<p style="text-align: left;"><em></em>
<strong>4.</strong>Böylece indirdiğimiz iso dosyasını "/mnt/iso" dizinine bağlamış olduk.Artık oyunu kurabiliriz.Yapmanız gereken tek şey ise;</p>
<p style="text-align: left;">*$ cd /mnt/iso</p>
<p style="text-align: left;">*$<em>sudo sh setup.sh</em>
komutunu verip oyunu sisteminize yüklemek.Kurulum bitince;</p>
<p style="text-align: left;">*$ <em>heroes3 </em>komutu vererek oyuna başlayabilirsiniz.</p>
<p style="text-align: left;">NOT: Eğer sisteminiz "x86_64" ise yapmanız gereken :</p>
<p style="text-align: left;">"setup.sh" dosyasındaki aşağıdaki kısımı değiştirmektir.</p>
<p style="text-align: left;"><strong>Önceki:</strong></p>
<p style="text-align: left;">DetectARCH()
{
status=1
case `uname -m` in
i?86) echo "x86"
status=0;;
*) echo "`uname -m`"
status=0;;
esac
return $status
}</p>
<p style="text-align: left;"><strong>Yeni:</strong></p>
<p style="text-align: left;">DetectARCH()
{
status=1
case `uname -m` in
i?86) echo "x86"
status=0;;
*) echo "x86"
status=0;;
esac
return $status
}</p></body></html>