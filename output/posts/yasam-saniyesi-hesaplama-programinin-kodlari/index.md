<html><body><blockquote><code>#!/usr/bin/env python
# -*- coding: utf-8 -*-</code>
<pre>print "     Yaşam Saniyesi Hesaplama Programına Hoşgeldiniz!"</pre>
<pre>dakika=60                                        # Dakika saniyesi
saat=dakika*60                                   # Saatin saniyesi
gun=saat*24                                      # Gunun saniyesi
ay=30*gun                                        # Ayin saniyesi
yil=365*gun                                      # Yilin saniyesi
y=input("  Lütfen doğum yılınızı giriniz: ")       # Kisinin kendi dogum yili
a=input("  Lütfen doğdunuz ayı rakamla başında sıfır olmadan giriniz: ")#     //    //    //  ayi
g=input("  Doğdunuz günü rakamla giriniz: ")       #    //    //    //   gunu
o=input("  Şu anki yılı giriniz: ")                # Icinde bulundugumuz yil
k=input("  Şu anki ayı giriniz: ")                 #  //        //       ay
p=input("  Şu anki günü giriniz: ")                #  //        //       gun
t=o-y                                            # Matematikesel Yil hesaplamasi
c=k-a                                            #  //          Ay       //
m=p-g                                            #  //          Gun      //
T=t*yil+c*ay+m*gun                               # Toplam Yaşam Saniyesi
soluk=T/17                                       # Ortalama soluk alıp verme
uyku=(8*saat)*(t*365+c*30+1*m)                   # Ortalama uykuda gecen sure
kalp=70*(T/60)                                   # Ortalama dakikada kalp atışı</pre>
<pre>print  T, "saniyedir yaşamakta",soluk," defa ortalama soluk alıp vermekte",uyku," saniye ömrünüzü uykuda geçirmekte",
kalp," defa kalbiniz atış yapmıştır."</pre>
</blockquote></body></html>