<html><body><img class="alignright" title="OpenSolaris" src="http://4.bp.blogspot.com/_b7TOyTq06Us/SvxiLBRV6eI/AAAAAAAAAZ4/epfS5wbNuFc/s200/opensolaris.jpg" alt="" width="200" height="200">OpenSolaris Nvidia Ekran kartınızı tanımıyorsa yapmanız gereken adımlar:

1. " <a href="http://www.nvidia.com/object/unix.html" target="_blank">http://www.nvidia.com/object/unix.html</a> " adresinden Solaris için sürümlerine bakabilirsiniz ve kartınızın desteklenip desteklenmediğini kontrol edin.

2.Eğer destekliyorsa "Nvidia Driver"ını bilgisayarınıza indirin.Örnek : 173.14.27

3.Uçbiriminizi açın ve root olun.

#<em> pkg uninstall NVDAgraphics</em>

yukardaki komut ile sistemde bulunan nvidia sürücüsünü kaldırın.

4."Nvidia Driver"ını  indirdiğinize gelip,

# <em>sh ./Nvidia.173.14.XX </em>

komutunu yazarak driverı yükleyin.Sisteminizi yeniden başlatın.

Kolay gelsin :)</body></html>