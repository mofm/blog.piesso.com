<html><body><p>Bu kodlamada büyük yanlışlıklar var olabilir.
</p><blockquote><code>#!/usr/bin/env python
#-*- coding:utf-8 -*-</code>
<pre>print  "      Ölçü Birimleri Çevirme Programı'na Hoşgeldiniz!!!"
anamenu1=" (a) Uzunluk Ölçü Birimleri"
anamenu2=" (b) Alan Ölçü Birimleri"
anamenu3=" (c) Ağırlık Ölçü Birimleri"
anamenu4=" (d) Hacim Ölçüleri"
anamenu5=" (e) Tartılar"
secenek1=" (a1) santimetre'cm' &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; inç"
secenek2=" (a2) metre'm' &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; yarda"
secenek3=" (a3) kilometre'km' &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; mil"
secenek4=" (a4) inç &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; Santimetre'cm'"
secenek5=" (a5) ayak'foot' &gt;&gt;&gt;&gt; santimetre'cm'"
secenek6=" (a6) yarda &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; metre'm'"
secenek7=" (a7) karamili &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; metre'm'"
secenek8=" (a8) denizmili &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; metre'm'"
secenek9=" (b1) santimetrekare'cm2'&gt;&gt;&gt; inçkare"
secenek10=" (b2) metrekare(m2) &gt;&gt;&gt;&gt; yarda kare"
secenek11=" (b3) hektar'ha' &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; acre"
secenek12=" (b4) kilometrekare &gt;&gt;&gt;&gt;&gt;&gt; mil kare"
secenek13=" (b5) inç kare &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; 'cm2'"
secenek14=" (b6) ayak kare &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; 'cm2'"
secenek15=" (b7) yarda kare &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; 'm2'"
secenek16=" (b8) acre &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; 'm2'"
secenek17=" (b9) mil kare &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; hektar"
secenek18=" (c1) gram'gr' &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; ounce"
secenek19=" (c2) kilogram'kg' &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; pound"
secenek20=" (c3) ton &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; küçük ton"
secenek21=" (c4) onunce'oz' &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; gram 'gr'"
secenek22=" (c5) pound'Ib' &gt;&gt;&gt;&gt;&gt; kilogram 'kg'"
secenek23=" (c6) küçük ton &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; ton"
secenek24=" (c7) büyük ton &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; ton"
secenek25=" (d1) santimetre küp'cm3'&gt;&gt;&gt;inç küp"
secenek26=" (d2) desimetre küp'dm3'&gt;&gt;&gt;ayak küp"
secenek27=" (d3) metre küp'm3'&gt;&gt;&gt;&gt;&gt;&gt;&gt;yarda küp"
secenek28=" (d4) inç küp&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'cm3'"
secenek29=" (d5) ayak küp&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'dm3'"
secenek30=" (d6) yarda küp&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'m3'"
secenek31=" (e1) litre'lt'&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'galon'ABD"
secenek32=" (e2) hektolitre'hl'&gt;&gt;&gt;&gt;'bushel'ABD"
secenek33=" (e3) 'pint-kuru'ABD&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'litre'"
secenek34=" (e4) 'pint-yat'ABD&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'litre'"
secenek35=" (e5) 'pint'İngiliz&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'litre'"
secenek36=" (e6) 'bushel'ABD&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'litre'"
secenek37=" (e7) 'bushel'İngiliz&gt;&gt;&gt;&gt;&gt;&gt;&gt;'litre'"
secenek38=" (e8) 'galon'ABD&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'litre'"
secenek39=" (e9) 'galon'İngiliz&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;'litre'"</pre>
<pre>print anamenu1
print anamenu2
print anamenu3
print anamenu4
print anamenu5</pre>
<pre>soru0=raw_input("Lütfen işlem yapacağınız genel birimin kodunu girin: ")</pre>
<pre>if soru0=="a":
print "Uzunluk Ölçü Birimleri"
print secenek1,secenek2
print secenek3,secenek4
print secenek5,secenek6
print secenek7,secenek8
if soru0=="b":
print "Alan Ölçü Birimleri"
print secenek9,secenek10
print secenek11,"",secenek12
print secenek13,"",secenek14
print secenek15,"",secenek16
print secenek17
if soru0=="c":
print "Ağırlık Ölçü Birimleri"
print secenek18,"",secenek19
print secenek20,"",secenek21
print secenek22,"",secenek23
print secenek24
if soru0=="d":
print "Hacim Ölçüleri"
print secenek25,secenek26
print secenek27,secenek28
print secenek29,secenek30
if soru0=="e":
print "Tartılar"
print secenek31,secenek32
print secenek33,secenek34
print secenek35,secenek36
print secenek37,secenek38
print secenek39</pre>
<pre>while True:
aciklama="Lütfen sayısal değeri girin: "
soru=raw_input("Lütfen çeviri yapacağınız birimin numarasını girin: ")</pre>
<pre>if soru=="a1":
soru1=input(aciklama)
i=soru1*0.3937
print soru1,"cm"," :", i," inch"</pre>
<pre>if soru=="a2":
soru2=input(aciklama)
y=soru2*1.0936
print soru2,"m"," :",y," yarda"</pre>
<pre>if soru=="a3":
soru3=input(aciklama)
mil=soru3*0.6214
print soru3,"km"," :",mil," mil"
if soru=="a4":
soru4=input(aciklama)
s=soru4*2.5400
print soru4,"İnç"," :",s," cm"
if soru=="a5":
soru5=input(aciklama)
f=soru5*0.3048
print soru5,"foot"," :",f," cm"
if soru=="a6":
soru6=input(aciklama)
me=soru6*0.9144
print soru6,"yarda"," :",me," m"
if soru=="a7":
soru7=input(aciklama)
met=soru7*1609
print soru7,"karamili"," :",met," m"
if soru=="a8":
soru8=input(aciklama)
metr=soru8*1852
print soru8," denizmili"," :",metr," m"
if soru=="b1":
soru9=input(aciklama)
si=soru9*0.1550
print soru9," cm2"," :",si," inç kare"
if soru=="b2":
soru10=input(aciklama)
my=soru10*1.1960
print soru10," m2"," :",my," yarda kare"
if soru=="b3":
soru11=input(aciklama)
haa=soru11*2.4711
print soru11," ha"," :",haa," acre"
if soru=="b4":
soru12=input(aciklama)
kmk=soru12*0.3861
print soru12," km2"," :",kmk," mil kare"
if soru=="b5":
soru13=input(aciklama)
icm=soru13*6.4516
print soru13," inç kare"," :",icm," cm2"
if soru=="b6":
soru14=input(aciklama)
acm=soru14*929
print soru14," ayak kare"," :",acm," cm2"
if soru=="b7":
soru15=input(aciklama)
yam=soru15*0.8361
print soru15," yarda kare"," :",yam," m2"
if soru=="b8":
soru16=input(aciklama)
acrem=soru16*4046.86
print soru16," acre"," :",acrem," m2"
if soru=="b9":
soru17=input(aciklama)
mih=soru17*259
print soru17," mil kare"," :",mih," hektar"
if soru=="c1":
soru18=input(aciklama)
gou=soru18*0.0353
print soru18," gr"," :",gou," ounce"
if soru=="c2":
soru19=input(aciklama)
kgp=soru19*2.2046
print soru19," kg"," :",kgp," pound"
if soru=="c3":
soru20=input(aciklama)
tkt=soru20*1.1023
print soru20," ton"," :",tkt," küçük ton"
if soru=="c4":
soru21=input(aciklama)
ongr=soru21*28.350
print soru21," onunce"," :",ongr," gr"
if soru=="c5":
soru22=input(aciklama)
pkg=soru22*0.4536
print soru22," pound"," :",pkg," kg"
if soru=="c6":
soru23=input(aciklama)
ktt=soru23*0.9072
print soru23," küçük ton"," :",ktt," ton"
if soru=="c7":
soru24=input(aciklama)
btt=soru24*1.0161
print soru24," büyük ton"," :",btt," ton"
if soru=="d1":
soru25=input(aciklama)
sink=soru25*0.061
print soru25," cm3"," :",sink," inç küp"
if soru=="d2":
soru26=input(aciklama)
deak=soru26*0.0353
print soru26," dm3"," :",deak," ayak küp"
if soru=="d3":
soru27=input(aciklama)
myk=soru27*1.3079
print soru27," m3"," :",myk," yarda küp"
if soru=="d4":
soru28=input(aciklama)
incm=soru28*16.390
print soru28," inç küp"," :",incm," cm3"
if soru=="d5":
soru29=input(aciklama)
aydk=soru29*28.320
print soru29," ayak küp"," :",aydk," dm3"
if soru=="d6":
soru30=input(aciklama)
yamk=soru30*0.7646
print soru30," yarda küp"," :",yamk," m3"
if soru=="e1":
soru31=input(aciklama)
liga=soru31*0.2642
print soru31," litre"," :",liga," galon ABD"
if soru=="e2":
soru32=input(aciklama)
hekbu=soru32*2.83178
print soru32," hektolitre"," :",hekbu," bushel ABD"
if soru=="e3":
soru33=input(aciklama)
pikl=soru33*0.5506
print soru33," pint-kuru ABD"," :",pikl," litre"
if soru=="e4":
soru34=input(aciklama)
piyl=soru34*0.4732
print soru34," pint-yat ABD"," :",piyl," litre"
if soru=="e5":
soru35=input(aciklama)
pntl=soru35*0.5683
print soru35," pint İngiliz"," :",pntl," litre"
if soru=="e6":
soru36=input(aciklama)
bshl=soru36*35.238
print soru36," bushel ABD"," :",bshl," litre"
if soru=="e7":
soru37=input(aciklama)
bshll=soru37*36.369
print soru37," bushel İngiliz"," :",bshll," litre"
if soru=="e8":
soru38=input(aciklama)
gall=soru38*3.7853
print soru38," galon ABD"," :",gall," litre"
if soru=="e9":
soru39=input(aciklama)
gal=soru39*4.5461
print soru39," galon İngiliz"," :",gal," litre"</pre>
</blockquote></body></html>