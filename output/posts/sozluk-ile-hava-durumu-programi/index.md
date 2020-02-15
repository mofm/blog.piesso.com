<html><body><blockquote><code>#!/usr/bin/env python
#-*-coding:utf-8-*-</code>
<pre>soru=raw_input("Şehrinizin adını tamamı küçük harf olacak şekilde yazınız: ")</pre>
<pre>cevap={"istanbul":"gök gürültülü ve sağanak yağışlı", "ankara":"açık ve güneşli", "izmir":"bulutlu"}</pre>
<pre>print cevap.get(soru,"Bu şehre ilişkin hava durumu bilgisi bulunmamaktadır.")</pre>
</blockquote></body></html>