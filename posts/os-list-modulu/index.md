<html><body><blockquote><code>#!usr/bin/env python
#-*- coding:utf-8 -*-</code>
<pre>import os</pre>
<pre>a=os.listdir("/home/semrelin")
c=0</pre>
<pre>for dosyalar in a :
if c&lt;len(a):
c=c+1
print c,".", dosyalar</pre>
</blockquote></body></html>