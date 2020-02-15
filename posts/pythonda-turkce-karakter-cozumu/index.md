<html><body><p>Python'da Türkçe karakter sıkıntısı çekenler için çok kısa bir çözüm,lütfen aşağıdaki örneği inceleyin:
</p><pre>
def monte(self):</pre>
<pre>
     soz=self.sozcuk.get()</pre>
<pre>
     soz=<strong>unicode.encode(unicode(soz),"utf8")</strong></pre>
<pre>
     an=self.anlam.get()</pre>
<pre>
     an=<strong>unicode.encode(unicode(an),"utf8")</strong></pre>
yukardaki örnekteki kalın kodlar yapılan text,entry girişlerinde türkçe karakter desteği verecektir.</body></html>