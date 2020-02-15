<html><body><h2>Python ile basit MySQL uygulaması,MySQL veritabanı ve tablo oluşturma</h2>
Python programlama diline yeni başlayanlar için(benim gibi) mysql veritabanı ve tablo oluşturma,ardından da bu veritabanını(tabloyu) yazdığım küçük python programımızda nasıl veri ekliyeceğimizi yada veritabanına nasıl sorgu gönderip veri çekeceğimizi anlatacağım.

İlk olarak Python ile MySQL veritabanını kullanabilmemiz için "<strong>mysqldb</strong>" kütüphanesine ihtiyacımız olacak.Debian ve türevi kullanıcıları için;

<em>$aptitude install python-mysqldb</em> #komutu ile sistemimize bu kütüphaneyi indirip kuruyoruz.

Şimdi gelelim programımızda kullanacağımız MySQL veritabanını ve tablomuzu oluşturmaya;

<em>$mysql -u root -p</em> #konsola komutu verip ve ardından şifremizi girdikten sonra mysql veritabanına erişelim.

Mysql'e giriş yaptıktan sonra yeni veritabanını oluşturalım;

<strong>mysql&gt;</strong><em>create database ornek;</em> (sizin verebiliceğiniz herhangi veritabanı adı)

<em>Query OK</em> ,cümlesi ile başlayan cevabı aldığımızda işlemimiz olumlu sonuçlanmış ve veritabanımız oluşturulmuştur.Hemen bu veritabanına geçip tablo oluşturalım.Burada tablo oluştururken sütun ve karakter sayısı sizin ihtiyacınıza kalmış.Aşağıdaki örneği inceleyelim;

<strong>mysql&gt;</strong><em>use ornek ;</em># yeni oluşturduğumuz veritabanına geçiş yapalım.

<strong>mysql&gt;</strong><em>create table kutuphane (kitap varchar(50), yazar varchar(50), yayin varchar(50), yil varchar(10));</em>

Böylece veritabanımızda "kitap,yazar,yayin,yil" sütunları olan kutuphane adlı bir tablo oluşturduk.Şimdi tablo örnek bir veri girelim;

<strong>mysql&gt;</strong><em>insert into kutuphane values ("Python Linux","Great TUX","Linux Yayinlari","2009");</em>

<em>Query OK</em>,ile başlayan mesajı aldıysanız  veritabanına ilk  veri girişimiz başarıyla tamamlanmış demektir.Eklediğimiz verileri tabloda görmek için;

<strong>mysql&gt;</strong><em>select * from kutuphane;</em> #yazarak görebilirsiniz.

Böylece MySQL'de veritabanımızı,tablomuzu ve ilk örnek verimizi girmiş olduk.Sıra geldi yazacağımız Python  ile bu veritabanına veri ekleyeceğimiz küçük bir program yazmaya.Aşağıda örnek kodları mevcut dikkatle inceleyin.
<pre lang="python">#!/usr/bin/env python
#-*- coding:utf-8 -*-

import MySQLdb

def ekle():
 x=raw_input("Lütfen ekleyeceğiniz kitabın adını girin: ")
 y=raw_input("Eklediğiniz kitabın yazarını girin: "
 z=raw_input("Yayınevi : ")
 v=raw_input("Basım Yılı: ")
 db=MySQLdb.connect(host="localhost",user="root",passwd="123456",db="ornek")
 cursor=db.cursor()
 s="""insert into kutuphane (kitap,yazar,yayin,yil) values (%s,%s,%s,%s)"""
 cursor.executemany(s,[(x,y,z,v)])

ekle()</pre>
Bu kodları herhangi bir metin düzenliyici ile yazıp "ornek.py" olarak kaydedin.Konsoldan dosyanın bulunduğu dizine girip;

<em>$python ornek.py</em> #yazarak veritabanınıza veri ekleyin.(Kodlarda yanlışlık olabilir eğer varsa yorumlarda belirtin lütfen)

Kolay gelsin.</body></html>