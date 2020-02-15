<html><body><p>Eğer halen uzaktaki sunucunuza ssh ile root olarak bağlanıyorsanız hemen kapatın! Sunucuza root ile bağlanıyorsanız büyük risk altındasınız demektir.Çünkü ssh ile root girişine izin vermek büyük bir güvenlik açığıdır.Bu açığı şu şekilde açıklayabiliriz;Sunucunuza brute force bir saldırı olduğunu ve bu saldırıda saldırgan sizin kullanıcı adınızı ve parolanızı  tahmin etmeye çalışacaktır.Her linux ya da unix sunucuda bir root kullanıcısı var olduğuna göre,bu root kullanıcısı açık bir hedeftir.Çünkü saldırgan hem kullanıcı adı ve parolayı bulmaya çalışacağına,artık kullanıcı adı için uğraşmasına hiç gerek yoktur.Geriye sadece parolayı tahmin etmek kalıyor.Bahsettiğimiz bu açığı hemen kapatalım ve sunucumuza daha güvenli bir şekilde bağlanalım.

İlk olarak yapmamız gereken ssh'ın ön tanımlı <strong>"22"</strong> portunu değiştirmek.Çünkü bu portu kullandığınızda saldırganın bu adımı hiç düşünmeden atlamasına olanak tanıyorsunuz.Bunu değiştirmek için kullandığınız bir editör ile "<em> /etc/ssh/sshd_config</em>" dosyasını açın;
</p><blockquote># nano /etc/ssh/sshd_config</blockquote>
ve bu dosyada <strong>"Port 22 " </strong>yazan satırın başında diyez(#)  varsa kaldırın ve "<em>22</em>" nci porttan farklı bir port girin.Örnek olarak: <strong>"Port 2222"</strong> gibi.

Daha sonra aynı dosyada <em>"# Authentication:"</em> bölümünde <em>"#PermitRootLogin yes"</em> yazan satırı bulun ve başındaki diyezi kaldırıp yes yerine no yazın.Bu satırla ssh ile bağlanırken root girişini kapatmış oluyoruz.Örnek satır: <strong> " PermitRootLogin no "</strong>

Artık bu dosyayı kaydedip kapatın ve kendinize <em>"useradd"</em> ya da <em>"adduser"</em> komutuyla ssh uzaktan bağlantı sağlayacak bir kullanıcı oluşturun,parolanızı belirleyin ve ssh'ı yeniden başlatın.
<blockquote># /etc/init.d/sshd restart</blockquote>
Bu adımlarla sunucumuzun ssh portunu değiştirip,root girişini kapattık.Artık sunucuya root olarak giriş yapamazsınız.Bu kadar güvenli hayır değil.Bundan daha güvenli bağlanmak için "ssh key" kullanmanız önerilir.

Sunucuya <strong>"ssh key "</strong> ile bağlanmak için sunucuya bağlantı yapacağımız bilgisayarda bir anahtar oluşturmak lazım.Anahtar oluşturmak için:
<blockquote>$ssh-keygen -b 1024 -t dsa</blockquote>
Bu komutla bir anahtar oluşturup,isterseniz parola belirleyebilirsiniz.Bu komuttan sonra <em>".ssh" </em>dizininizde bir private bir de public anahtarınız oluşacaktır.Sunucuya bu key ile bağlanmak istiyorsak bir şekilde <strong>"id_dsa.pub"</strong> adlı dosyayı sunucuya ulaştırmamız lazım.Bunun için <em>ftp,scp</em> vs. yollar kullanılabilir.

Eğer <strong>"id_dsa.pub"</strong> dosyasını sunucuya ulaştırdıysanız bu anahtara bağlanmak için sunucuda yetki verelim:
<blockquote>$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
$ cat ~/id_dsa.pub &gt;&gt; ~/.ssh/authorized_keys
$ rm ~/id_dsa.pub
$ chmod 600 ~/.ssh/authorized_keys</blockquote>
Bu adımlardan sonra sunucumuza bu anahtarla bağlanabiliriz.

NOT:

<strong>*</strong> Eğer ssh bağlantısını sadece belirli kullanıcılara vermek istiyorsanız,<em> "/etc/ssh/sshd_config"</em> dosyasına "AllowUsers" yazdıktan  bu kullanıcıları ekleyin.<strong>Örnek:</strong>



<blockquote>AllowUsers ahmet mehmet mustafa kemal</blockquote>



<strong>*</strong> Eğer belirli kullanıcılarına ssh bağlantısını kapatmak isterseniz, <em>"/etc/ssh/sshd_config"</em> dosyasına "DenyUsers" yazdıktan sonra bu kullanıcıları ekleyin.<strong>Örnek:</strong>



<blockquote>DenyUsers cuma sercan hamit can</blockquote>

</body></html>