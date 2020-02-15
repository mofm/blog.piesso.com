<html><body><p>Yumurta zamanlayıcısı lezzetli ve tam kıvamında yumurtalar hazırlaması için yazılmıştır.Yapmanız gereken ilk önce yumurta suyunu kaynatıp daha sonra "<em>Yumurta Zamanlayıcı</em>"sını çalıştırmak.Seçtiğiniz yumurta kıvamına göre size altını kapatmanız gerektiği uyarısını bilgisayarınız "<em>beep</em>" sesi ile verecektir.

Yumurta pişirmenin incelikleri hakkında bilgi almak için <a href="http://www.nizip.com/showthread.php?t=12074">buradan</a>

Programı indirmek için ise <a href="http://linux.piesso.com/programs/yumurta.py">buradan</a>

$ <em>python yumurta.py</em> komutu ile programı çalıştırabilirsiniz.

<strong>Programın kaynak kodları:</strong>

-------------------------------------------------------------------------------------------------------
</p><pre lang="python">#!/usr/bin/env python
#-*- coding:utf-8 -*-

#"Yazan: Emre ERYILMAZ"
#"Tarih: 28 Aralık 2009"
#"İletişim: emre.eryilmaz@linux.org.tr "
#"web adresi: http://webs.homelinux.com"
#"Bu program size tam kıvamında yumurtalar hazırlaması için hazırlanmıştır."

import time

class yumurta(object):
 def __init__(self):
 self.ekran()

 def rafadan(self):
 time.sleep(180)
 print "\a\a\a\a","Rafadan yumurtanız Hazır,Afiyet olsun."
 def kayisi(self):
 time.sleep(300)
 print "\a\a\a\a","Mis gibi Kayısı yumurtanız Hazır,Afiyet olsun."
 def kati(self):
 time.sleep(720)
 print "\a\a\a\a","Katı yumurtanız Hazır,Afiyet olsun."
 def ekran(self):
 now=time.strftime("%H:%M:%S")
 print "Sistem Saati",": ",now
 print "\nYumurta Zamanlayıcısı\nProgram Önerisi:Lütfen ilk önce suyu kaynatın, daha sonra yumurtayı ilave edip programı başlatın ve seçiminizi yapın.\n\n"

 print "(1) Rafadan Yumurta"
 print "(2) Kayısı Yumurta"
 print "(3) Katı Yumurta\n\n"
 soru=input("Lütfen yumurta seçimini yapın: ")
 if soru==1:
 self.rafadan()
 elif soru==2:
 self.kayisi()
 elif soru==3:
 self.kati()
 else:
 print "Lütfen seçim yapın"

yumurta()</pre>
-----------------------------------------------------------------------------------------------------</body></html>