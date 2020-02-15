<html><body><strong><img class="alignright" title="CentOS logo" src="http://www.rainbowcomputech.com/published/publicdata/WASTORE/attachments/SC/products_pictures/Centos_Logo6u_thm.gif" alt="" width="100" height="100">CentOS</strong> resmi depoları kısıtlı ve aradığımız bazı paket ve ya uygulamaları bu depolarda bulamayabiliriz.Fakat EPEL ve RPMforge depoları ile neredeyse ihtiyacımız olan birçok paket ve uygulamaları kapsar nitelikte.Sizde EPEL ve RPMforge depolarından herhangi birini ya da ikisini de  ekleyerek deponuzu genişletebilirsin.

<strong>"RPMforge " deposunu ekleyelim:</strong>

* İlk olarak kendi sürüm ve mimarimize uygun paketi indirelim:

<strong>CentOS 6 :</strong>

<em>i686 </em>:  <a href="http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm" target="_blank">http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm</a>

<em>x86_64</em> : <a href="http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm" target="_blank">http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm</a>

<strong>CentOS 5 :</strong>

<em>i686</em> : <a href="http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.i386.rpm" target="_blank">http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.i386.rpm</a>

<em>x86_64</em> : <a href="http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm" target="_blank">http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm</a>

* Kendimizi uygun olan paketi indirdikten sonra deponun anahtarlarını içe aktaralım .

<code>#   rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt</code>

* Anahtar listesini aktardığımıza göre indirdiğimiz "<strong>rpm</strong>"  paketini kontrol edelim.

<code># rpm -K rpmforge-release-0.5.2-2.el*.rf.*.rpm</code> (kendi mimarinize ve sürümünüze uygun indirdiğiniz paket)

* Doğruluğu teyit edildiğine göre artık paketi yükleyip,depomuzu ekleyelim.

<code># rpm -i rpmforge-release-0.5.2-2.el*.rf.*.rpm</code>

<strong>EPEL deposunu ekleyelim:</strong>

* EPEL deposu içinde ilk olarak kendi mimarimize ve sürmümüze uygun olan paketi indirelim;

<strong>CentOS 6</strong> (Beta aşamasında ) :

<em>i386</em> : <a href="http://download.fedora.redhat.com/pub/epel/beta/6/i386/epel-release-6-5.noarch.rpm" target="_blank">http://download.fedora.redhat.com/pub/epel/beta/6/i386/epel-release-6-5.noarch.rpm</a>

<em>x86_64</em> : <a href="http://download.fedora.redhat.com/pub/epel/beta/6/x86_64/epel-release-6-5.noarch.rpm" target="_blank">http://download.fedora.redhat.com/pub/epel/beta/6/x86_64/epel-release-6-5.noarch.rpm</a>

<strong>CentOS 5</strong> :

<em>i386</em> : <a href="http://download.fedora.redhat.com/pub/epel/5/i386/epel-release-5-4.noarch.rpm" target="_blank">http://download.fedora.redhat.com/pub/epel/5/i386/epel-release-5-4.noarch.rpm</a>

<em>x86_64</em> : <a href="http://download.fedora.redhat.com/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm" target="_blank">http://download.fedora.redhat.com/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm</a>

* Kendi mimarimize ve sürümümüze uygun paketi indirdikten sonra depomuzu kuralım.

<code># rpm -i epel-release-*-*.noarch.rpm</code>

<code>
* Ya da hiçbir paket indirmeden doğrudan paketi kurup,depoyu ekleyebiliriz.</code>

# rpm -ivh <a href="http://download.fedora.redhat.com/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm" target="_blank">http://download.fedora.redhat.com/pub/epel/*/*/epel-release-*-*.noarch.rpm</a>
Depolarımızı sisteme ekledik fakat bu depolarda sistemde yüklü olan taban ya da diğer paketlerin,uygulamaların farklı sürümleri mevcut olabilir.Sistem kararlılığını riske atmamak için bu depoların önceliğini değiştirelim ya da sadece ihtiyacımız olduğu zaman kullanalım.

<strong>1.İhtiyaç halinde depolar:</strong>

* Eklediğimiz depoları ihtiyaç halinde ,istediğimiz zaman kullanmak için öntanımlı olarak "geçersiz" bırakalım.Depoları geçersiz bırakmak için depo konfigurasyon dosyalarındaki "<strong>enabled=1</strong>" ifadesini "<strong>enabled=0</strong>" olarak değiştirelim.

<code># vi /etc/yum.repos.d/rpm.forge.repo</code>

<code># vi /etc/yum.repos.d/epel.repo</code>

Yukardaki dosyaları bir editör ile açtıktan sonra depoları "enabled=1" yaparak geçersiz kılalım.Ya da diğer bir yolla :

<code># sed -i “s/enabled=1/enabled=0/” /etc/yum.repos.d/epel.repo</code>

<code># sed -i “s/enabled=1/enabled=0/” /etc/yum.repos.d/rpm.forge.repo</code>

Şeklinde yaparak da değeri değiştirebilirsiniz.Depoların geçersiz olup olmadığını kontrol edelim.

<code># yum repolist all</code>

Bu komutla eklediğimiz depoların karşısında geçersiz olduğunu gösteren kırmızı ile "<em>disabled</em>" yazısını göreceksiniz.Artık depolara ihtiyacımız olduğunda  "<strong>yum</strong>" komutundan sonra "<em>--enablerepo=epel</em>" ya da "<em>--enablerepo=rpmforge</em>" şeklinde yazarak kullanabiliriz.Örnek :

<code># yum --enablerepo=epel install mod_security</code>

<strong>2.Depoların önceliğini değiştirelim:</strong>

* Yukarda dediğim gibi eklediğimiz bu depoların herhangi bir kararsızlığa mahal vermemesi için depolar için öncelik ayarı yapabiliriz.Depolara öncelik ayarı yapmak için "<strong>yum-priorities</strong>" paketini kuralım.

<code># yum install yum-priorities</code>

* Paketini kurduktan sonra ekli olan tüm depoları geçerli yapabiliriz.Depoları geçerli hale getirmek için "enable=0" değerini "enable=1" yapın.Artık depolara öncelik verelim.Depolara öncelik atamak için "<strong>priority=DEĞER</strong>" şeklinde bir öncelik tanımlayabiliriz.Mesela CentOS'un kendi depolarına "priority=1" değerini atalım.Diğer EPEL ve RPMforge depolarına "priority=2" değerini atayalım.Depolara değer atamak için "priority" değerlerini depo konfigurasyon dosyalarına her depo alt satırına ekleyelim.Örnek:

<code># vi /etc/yum.repos.d/epel.repo</code>

[epel]
name=Extra Packages for Enterprise Linux 5 - $basearch
#baseurl=http://download.fedoraproject.org/pub/epel/5/$basearch
mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=epel-5&amp;arch=$basearch
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL
<strong>priority=2</strong></body></html>