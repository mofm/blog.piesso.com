<html><body><p>Bu program televizyonlardaki alarm sisteminin bilgisayarda olan versiyonudur.Kaç saat ve kaç dakika sonra çalmasını ( bu programda sizi radyo uyandıracak) istiyorsanız giriyorsunuz.Sizin belirttiğiniz süre sonunda bilgisayarınızda tarayıcıda açılacak ve karşınıza AOL radyo çıkacak.Umarım uyanırsınız :)

Programı indirmek için <a href="http://linux.piesso.com/programs/alarm.py">buradan
</a>

$python alarm.py komutu ile programı çalıştırabilirsiniz.

Programın kaynak kodları ise aşağıdaki gibi:

------------------------------------------------------------------------------------------------
</p><pre lang="python">#!/usr/bin/env python
#-*- coding:utf-8 -*-

#"Yazan: Emre ERYILMAZ"
#"Tarih: 28 Aralık 2009"
#"İletişim: emre.eryilmaz@linux.org.tr "
#"web adresi: http://webs.homelinux.com"
#"Bu program televizyonlardaki alarm sisteminin bilgisayarda olan versiyonudur.Kaç saat ve kaç dakika
#sonra çalmasını( bu programda sizi radyo uyandıracak) istiyorsanız giriyorsunuz.Sizin belirttiğiniz
#süre sonunda bilgisayarınızda tarayıcıda açılacak ve karşınıza AOL radyo çıkacak.Umarım uyanırsınız:)"

import time,webbrowser

now=time.strftime("%H:%M:%S")

print "Sistem Saati",": ",now
print "\n\n"

soru=input("Lütfen alarm saatini girin: ")

soru1=input("Lütfen alarm dakikasını girin: ")

ara=(soru*3600)+(soru1*60)

time.sleep(ara)

webbrowser.open("http://player.play.it/player/aolPlayer.html")</pre>
----------------------------------------------------------------------------------------------------------------------</body></html>