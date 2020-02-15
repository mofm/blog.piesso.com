<html><body><p>Tek komutla ADSL Modeminizi resetlemek için küçük bir script.İlk önce bir metin editörü açın :

</p><blockquote><tt>
$ nano modem-restart
</tt></blockquote>

ve aşağıdaki scripti yapıştırın,kullanıcı adı ve parola alanı ve ip adresi yerine kendi modem adresinizi,kullanıcı adı ve parolanızı girin.Daha sonra "modem-restart" adlı dosyayı kaydedin.Kaydettiğimiz dosyayı "/usr/bin/ " dizini altına kopyalın ve çalıştırma izni verin.

<blockquote><tt>

$ sudo cp modem-restart /usr/bin/
$ sudo chmod +x /usr/bin/modem-restart

</tt></blockquote>

Artık uçbirimden tek komutla modeminizi yeniden başlatabilirsiniz :)

SCRIPT:::::::::::

<blockquote><tt>
#!/bin/bash
host=192.168.1.1 (kendi ip adresiniz)
port=23
login=kullanici_adiniz
passwd=parolaniz
cmd=reboot

(echo open ${host} ${port}
sleep 3
echo ${login}
sleep 3
echo ${passwd}
sleep 3
echo ${cmd}
sleep 10
echo exit) | telnet

  </tt></blockquote></body></html>