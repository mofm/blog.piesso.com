<html><body><p>Basit bir konsoldan çalıştırabileceğiniz "google içinde arama" programı.Programı konsoldan çalıştırdıktan sonra arayacağınız metayı girip enterladığınızda sonucu o an açık olan tarayıcıda yeni bir tabda ya da default tarayıcınızda açan basit python ile yazılmış program.

Programı indirmek için <a href="http://linux.piesso.com/programs/google.py">buradan</a>

İndirdikten sonra çalıştırmak için,konsoldan programın bulunduğu dizine geçip,

$ python google.py  komutunu vermeniz yeterli.

Programın kaynak kodları ise aşağıdaki gibi:

----------------------------------------------------------------------------------
</p><pre lang="python">
#!/usr/bin/env python
#-*- coding:utf-8 -*-
#"Yazan: Emre ERYILMAZ"
#"Tarih: 28 Aralık 2009"
#"İletişim: emre.eryilmaz@linux.org.tr "
#"web adresi: http://webs.homelinux.com"
#"Google'dan girdiğiniz metayı bulup tarayıcınızda açan basit bir konsol programı"
import webbrowser
while True:
    print "Çıkış için 'q' tuşuna basın."
    meta = raw_input("Ara :  ")
    if meta=="q":
        break
    else:
        pass
    google = 'http://www.google.com/search?hl=tr&amp;q='
    adress = ''
    meta = '+'.join((meta.split(' ')))
    print meta
    webbrowser.open(google+meta)
</pre>
--------------------------------------------------------------------</body></html>