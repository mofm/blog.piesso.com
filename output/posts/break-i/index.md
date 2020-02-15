<html><body><blockquote><code>#!/usr/bin/env python
#-*- coding: utf-8 -*-</code>
<pre>kullanici_adi = "kullanici"
parola = "parola"</pre>
<pre>while True:
soru1=raw_input("Kullanıcı adı: ")
soru2=raw_input("Parola: ")</pre>
<pre>if soru1 == kullanici_adi and soru2 == parola :
print "Kullanıcı adı ve parolanız onaylandı.Programa hoşgeldiniz!"
break
else:
print "Kullanıcı adınız veya parolanızdan en az birisi onaylanmadı."
print "Lütfen tekrar deneyiniz!"</pre>
</blockquote></body></html>