<html><body><p>Bu kodlamada da döngü de bir oluşmuş olabilir.
</p><blockquote><code>#!/usr/bin/env python
#-*- coding:utf-8 -*-</code>
<pre>print  "      Ölçü Birimleri Çevirme Programı'na Hoşgeldiniz!!!"
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
<pre>while True:</pre>
<pre>print anamenu1
print anamenu2
print anamenu3
print anamenu4
print anamenu5</pre>
<pre>soru=raw_input("Lütfen işlem yapacağınız genbiin kodunu girin: ")
while soru!="/u":
if soru=="a":
print "Uzunluk Ölçü Birimleri"
print secenek1,secenek2
print secenek3,secenek4
print secenek5,secenek6
print secenek7,secenek8</pre>
<pre>if soru=="b":
print "Alan Ölçü Birimleri"
print secenek9,secenek10
print secenek11,"",secenek12
print secenek13,"",secenek14
print secenek15,"",secenek16
print secenek17</pre>
<pre>if soru=="c":
print "Ağırlık Ölçü Birimleri"
print secenek18,"",secenek19
print secenek20,"",secenek21
print secenek22,"",secenek23
print secenek24</pre>
<pre>if soru=="d":
print "Hacim Ölçüleri"
print secenek25,secenek26
print secenek27,secenek28
print secenek29,secenek30
if soru=="e":
print "Tartılar"
print secenek31,secenek32
print secenek33,secenek34
print secenek35,secenek36
print secenek37,secenek38
print secenek39</pre>
<pre>print soru
aciklama="Lütfen sayısal değeri girin: "
sorux=input(aciklama)</pre>
<pre>if soru=="a1":
sorux
i=sorux*0.3937
print sorux,"cm"," :", i," inch"
break
if soru=="a2":
sorux
y=sorux*1.0936
print sorux,"m"," :",y," yarda"
break
if soru=="a3":
sorux
mil=sorux*0.6214
print sorux,"km"," :",mil," mil"
break
if soru=="a4":
sorux
s=sorux*2.5400
print sorux,"İnç"," :",s," cm"
break
if soru=="a5":
sorux
f=sorux*0.3048
print sorux,"foot"," :",f," cm"
break
if soru=="a6":
sorux
me=sorux*0.9144
print sorux,"yarda"," :",me," m"
break
if soru=="a7":
sorux
met=sorux*1609
print sorux,"karamili"," :",met," m"
break
if soru=="a8":
sorux
metr=sorux*1852
print sorux," denizmili"," :",metr," m"
break
if soru=="b1":
sorux
si=sorux*0.1550
print sorux," cm2"," :",si," inç kare"
break
if soru=="b2":
sorux
my=sorux*1.1960
print sorux," m2"," :",my," yarda kare"
break
if soru=="b3":
sorux
haa=sorux*2.4711
print sorux," ha"," :",haa," acre"
break
if soru=="b4":
sorux
kmk=sorux*0.3861
print sorux," km2"," :",kmk," mil kare"
break
if soru=="b5":
sorux
icm=sorux*6.4516
print sorux," inç kare"," :",icm," cm2"
break
if soru=="b6":
sorux
acm=sorux*929
print sorux," ayak kare"," :",acm," cm2"
break
if soru=="b7":
sorux
yam=sorux*0.8361
print sorux," yarda kare"," :",yam," m2"
break
if soru=="b8":
sorux
acrem=sorux*4046.86
print sorux," acre"," :",acrem," m2"
break
if soru=="b9":
sorux
mih=sorux*259
print sorux," mil kare"," :",mih," hektar"
break
if soru=="c1":
sorux
gou=sorux*0.0353
print sorux," gr"," :",gou," ounce"
break
if soru=="c2":
sorux
kgp=sorux*2.2046
print sorux," kg"," :",kgp," pound"
break
if soru=="c3":
sorux
tkt=sorux*1.1023
print sorux," ton"," :",tkt," küçük ton"
break
if soru=="c4":
sorux
ongr=sorux*28.350
print sorux," onunce"," :",ongr," gr"
break
if soru=="c5":
sorux
pkg=sorux*0.4536
print sorux," pound"," :",pkg," kg"
break
if soru=="c6":
sorux
ktt=sorux*0.9072
print sorux," küçük ton"," :",ktt," ton"
break
if soru=="c7":
sorux
btt=sorux*1.0161
print sorux," büyük ton"," :",btt," ton"
break
if soru=="d1":
sorux
sink=sorux*0.061
print sorux," cm3"," :",sink," inç küp"
break
if soru=="d2":
sorux
deak=sorux*0.0353
print sorux," dm3"," :",deak," ayak küp"
break
if soru=="d3":
sorux
myk=sorux*1.3079
print sorux," m3"," :",myk," yarda küp"
break
if soru=="d4":
sorux
incm=sorux*16.390
print sorux," inç küp"," :",incm," cm3"
break
if soru=="d5":
sorux
aydk=sorux*28.320
print sorux," ayak küp"," :",aydk," dm3"
break
if soru=="d6":
sorux
yamk=sorux*0.7646
print sorux," yarda küp"," :",yamk," m3"
break
if soru=="e1":
sorux
liga=sorux*0.2642
print sorux," litre"," :",liga," galon ABD"
break
if soru=="e2":
sorux
hekbu=sorux*2.83178
print sorux," hektolitre"," :",hekbu," bushel ABD"
break
if soru=="e3":
sorux
pikl=sorux*0.5506
print sorux," pint-kuru ABD"," :",pikl," litre"
break
if soru=="e4":
sorux
piyl=sorux*0.4732
print sorux," pint-yat ABD"," :",piyl," litre"
break
if soru=="e5":
sorux
pntl=sorux*0.5683
print sorux," pint İngiliz"," :",pntl," litre"
break
if soru=="e6":
sorux
bshl=sorux*35.238
print sorux," bushel ABD"," :",bshl," litre"
break
if soru=="e7":
sorux
bshll=sorux*36.369
print sorux," bushel İngiliz"," :",bshll," litre"
break
if soru=="e8":
sorux
gall=sorux*3.7853
print sorux," galon ABD"," :",gall," litre"
break
if soru=="e9":
sorux
gal=sorux*4.5461
print sorux," galon İngiliz"," :",gal," litre"
break</pre>
</blockquote></body></html>