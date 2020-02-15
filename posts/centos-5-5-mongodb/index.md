<html><body><strong><img class="alignright" title="Mongodb" src="http://www.gonosql.com/wp-content/uploads/2010/03/mongodb-logo.png" alt="" width="210" height="70">Centos</strong> ve diğer <strong>RedHat</strong> tabanlı dağıtımlar üstünde <a href="http://www.mongodb.org/" target="_blank">MongoDB</a> ihtiyacı duyuyorsanız, resmi depolarda olmadığı için güvenilir ve sürekli güncellenen bir depoya ihtiyacınız olabilir.MongoDB geliştiricileri bu noktada ihtiyacınız olan depoyu oluşturmuşlar.Depoyu ekleyip,sisteme hemen kurulum yapabilirsiniz.

MongoDB geliştiricilerinin oluşturduğu depoda <strong>2</strong> farklı platform(<em>x86</em> , <em>x86_64</em>)  için <strong>3</strong> sürümü(<em> stable , unstable, snapshot</em>) bulunuyor.İstediğiniz sürümü depodan yükleyebilirsiniz.

İlk olarak depomuzu ekleyelim:
<pre>#  touch /etc/yum.repos.d/10gen-mongodb.repo</pre>
Oluşturduğumuz "<em>10gen-mongodb.repo</em>" dosyasına depo bilgilerini aşağıdaki gibi platformunuza göre ekleyin.

# vi /etc/yum.repos.d/10gen-mongodb.repo

 

<strong>X86_64 için :</strong>
<div>[10gen]
name=10gen Repository
baseurl=http://downloads-distro.mongodb.org/repo/redhat/os/x86_64
gpgcheck=0 

<strong>X86 için :</strong>
<div>
<div>

[10gen]
name=10gen Repository
baseurl=http://downloads-distro.mongodb.org/repo/redhat/os/i686
gpgcheck=0

 

Depomuzu ekledikten sonra MongoDB Server ve Client paketlerini yükleyebiliriz:

<em><strong>MongoDB Server ve Client Stable Sürüm :</strong></em>

# yum install mongo-10gen mongo-10gen-server

</div>
<div><em><strong>MongoDB Server ve Client Unstable Sürüm :</strong></em></div>
<div><em><strong>
</strong></em></div>
</div>
<div># yum install mongo-10gen-unstable mongo-10gen-unstable-server</div>
</div>
<div>MongoDB için ayar yapmak için konfigurasyon dosyasından gerekli değişiklikleri yapabiliriz."<em>/etc/mongodb.conf</em> " dosyasında istediğiniz değişiklikleri yapabilirsiniz.</div>
<div>"<em> /etc/mongodb.conf</em> " için :</div>
<div><strong>logpath =</strong> ' Bu kısıma mongodb için log tutulacak dosyanın yolunu yazın.'</div>
<div><strong>port =</strong> ' Burada mongodb 'nin kullanacağı portu belirtin.'</div>
<div><strong>dbpath = </strong>' mongodb için kullanacağı dizin yolunu belirtin.'</div>
<div>Bu dosyada gerekli değişiklikleri yaparken dikkat etmeniz gereken öntanımlı ayarların en uygun ayarlar olduğunu göz önünde bulundurun.</div>
<div>Yukarda mongodb için "<em>dbpath</em>" belirtiyseniz herhangi bir sorun yaşanmaması için izinlerini vermeyi unutmayın.Bunun içinde :</div>
<pre># chown -R mongod.mongod 'dbpath_icin_yazdiginiz_yol'</pre>
<div>Dikkat edilmesi diğer bir nokta ise yine "<em> mongodb.conf</em> " dosyasında belirtmiş olduğunuz portun firewall tarafından izin verilip,verilmediğini kontrol edin.</div>
<div>Artık MongoDB'yi başlatalım ve açılışa ekleyelim :</div>
<pre># /etc/init.d/mongod start
</pre>
<pre># chkconfig --levels 235 mongod on
</pre>
<div>Ve son olarak Mongo'nun çalışıp çalışmadığını test edin :</div>
<pre># mongo 
</pre></body></html>