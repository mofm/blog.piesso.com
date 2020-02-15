<html><body><p>Elime içimde bayağı bir uzun satır ve sütun olan bir excel dosyası geçti ve bunu hemen mysql'e aktarmam gerekti.Bunun için kendim için kısa bir çözüm oluşturdum.

Bu esnada yaptığım işlemleri adım adım kısa özet bir şekilde geçeyim :

<strong>1.</strong> İlk olarak elimizdeki excel dosyasını dışarıya "<em>csv</em>" şeklinde export edelim.

<strong>2.</strong> Bu siteden( <a href="http://csv2sql.com/" target="_blank">http://csv2sql.com/</a> ) "<strong>csv</strong>"yi <strong>sql</strong>'e çevirelim.

<strong>3.</strong> Site üretilen sql satırlarını bir dosyaya kaydedelim.Örnek: <em>data.sql</em>

<strong>4.</strong>Bu dataları atacağımız bir veritabanı oluşturalım.
</p><pre>$ mysql -u root -p</pre>
mysql&gt; create database perso ;

<strong>5.</strong> Dataları import edeceğimiz tabloyu oluşturalım.

mysql&gt; CREATE TABLE aka ( id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), unvan VARCHAR(255), adi VARCHAR(255), soyadi VARCHAR(255), sicil VARCHAR(255), birim VARCHAR(255) );

<strong>6.</strong> Son olarak oluşturduğumuz "<strong>data.sql</strong>" dosyasını veritabanına import edelim.
<pre>$ mysql -u root -p perso &lt; data.sql</pre></body></html>