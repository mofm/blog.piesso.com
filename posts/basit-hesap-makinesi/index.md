<html><body><blockquote><code>#!/usr/bin/env python
#-*- coding:utf-8 -*-</code>
<pre>from __future__ import division</pre>
<pre>while True:</pre>
<pre>secenek1="    (1) toplama"
secenek2="    (2) çıkarma"
secenek3="    (3) çarpma"
secenek4="    (4) bölme"
secenek5="    (5) üs alma"</pre>
<pre>print secenek1
print secenek2
print secenek3
print secenek4
print secenek5</pre>
<pre>soru=raw_input("  Lütfen yapmak istediğiniz işlemin numarasını girin: ")</pre>
<pre>if soru=="1":
sayi1=input("  Lütfen toplama işlemi için ilk sayıyı girin: ")
print sayi1
sayi2=input("  Lütfen toplama işlemi için ikinci sayıyı girin: ")
print sayi1, "+", sayi2, ":", sayi1 + sayi2</pre>
<pre>if soru=="2":
sayi3=input("  Lütfen çıkarma işlemi için ilk sayıyı girin: ")
print sayi3
sayi4=input("  Lütfen çıkarma işlemi için ikinci sayıyı girin: ")
print sayi3, "-", sayi4, ":", sayi3 - sayi4</pre>
<pre>if soru=="3":
sayi5=input("  Lütfen çarpma işlemi için ilk sayıyı girin: ")
print sayi5
sayi6=input("  Lütfen çarpma işlemi için ikinci sayıyı girin: ")
print sayi5, "*", sayi6, ":", sayi5 * sayi6</pre>
<pre>if soru=="4":
sayi7=input("  Lütfen bölme işlemi için ilk sayıyı girin: ")
print sayi7
sayi8=input("  Lütfen bölme işlemi için ikinci sayıyı girin: ")
print sayi7, "/", sayi8, ":", sayi7 / sayi8</pre>
<pre>if soru=="5":
sayi9=input("  Lütfen üs alacağınız sayıyı girin: ")
print sayi9
sayi10=input("  Lütfen alacağınız üssü girin: ")
print sayi9, "**" , sayi10, ":", sayi9 ** sayi10</pre>
</blockquote></body></html>