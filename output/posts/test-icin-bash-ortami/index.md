<html><body><p>Test için kısıtlı bir BASH ortamı ihtiyacınız ve chrooting 'e kolay giriş yapmak için chroot ortamında bash kabuğu oluşturalım.Bunun için ilk olarak gerekli olan dizinleri oluşturun;
</p><pre># mkdir /chroot</pre>
<pre># mkdir /chroot/bash</pre>
<pre># mkdir /chroot/bash/lib64</pre>
<pre># mkdir /chroot/bash/bin</pre>
Gerekli olan dizinleri oluşturduktan sonra bash kabuğunun ihtiyacı olan kütüphaneleri dizine (lib64) kopyalamamız lazım.Bash'in ihtiyacı olan kütüphaneleri bulalım.ldd(list dynamic dependencies) komutu ile bu kütüphaneleri listeleyelim:
<pre># ldd /bin/bash</pre>
<pre>linux-vdso.so.1 =&gt;  (0x00007fffe2511000)
 libncurses.so.5 =&gt; /lib64/libncurses.so.5 (0x00007f137fe71000)
 libdl.so.2 =&gt; /lib64/libdl.so.2 (0x00007f137fc6d000)
 libc.so.6 =&gt; /lib64/libc.so.6 (0x00007f137f902000)
 /lib64/ld-linux-x86-64.so.2 (0x00007f13800c4000)</pre>
Yukardaki çıktıda görüldüğü gibi gerekli olan kütüphaneler:

* libncurses.so.5

* libdl.so.2

* libc.so.6

* ld-linux-x86-64.so.2

Yukardaki kütüphaneleri oluşturduğunuz dizine(lib64 - sisteminize göre bu dizin "lib" olabilir.) taşıyın:
<pre># cp /lib64/libncurses.so.5 /chroot/bash/lib64
</pre>
<pre># cp /lib64/libdl.so.2 /chroot/bash/lib64</pre>
<pre># cp /lib64/libc.so.6 /chroot/bash/lib64</pre>
<pre># cp /lib64/ld-linux-x86-64.so.2 /chroot/bash/lib64</pre>
Bu işlemi yaptıktan sonra "<em>bash</em>" komutunu oluşturduğumuz "<strong>bin</strong>" dizinine kopyalayalım.
<pre># cp /bin/bash /chroot/bash/bin</pre>
Şimdi ihtiyacımız olan komutları chroot bash kabuğunuza kopyalayın.Mesela "<em>ls</em>" komutundan başlayalım.
<pre># ldd /bin/ls</pre>
<pre>linux-vdso.so.1 =&gt;  (0x00007fff161ff000)
 librt.so.1 =&gt; /lib64/librt.so.1 (0x00007fa1effe5000)
 libacl.so.1 =&gt; /lib64/libacl.so.1 (0x00007fa1efddc000)
 libc.so.6 =&gt; /lib64/libc.so.6 (0x00007fa1efa71000)
 libpthread.so.0 =&gt; /lib64/libpthread.so.0 (0x00007fa1ef854000)
 /lib64/ld-linux-x86-64.so.2 (0x00007fa1f01ee000)
 libattr.so.1 =&gt; /lib64/libattr.so.1 (0x00007fa1ef64f000)
</pre>
"ls" komutu için gerekli olan kütüphaneler yukardaki gibi.Hemen bunları chroot bash kabuğu ortamındaki "lib64" dizinine kopyalayın.
<pre># cp /lib64/librt.so.1 /chroot/bash/lib64</pre>
<pre># cp /lib64/libacl.so.1 /chroot/bash/lib64</pre>
<pre># cp /lib64/libpthread.so.0 /chroot/bash/lib64</pre>
<pre># cp /lib64/libattr.so.1 /chroot/bash/lib64</pre>
<strong>libc.so.6</strong> ve <strong>ld-linux-x86-64.so.2</strong> kütüphanelerini daha önce kopyaladığımız için bunlara gerek yok.Bu kütüphaneleri kopyaladıktan sonra "<em>ls</em>" komutunu oluşturduğumuz "<strong>bin</strong>" dizinine kopyalabiliriz.
<pre># cp /bin/ls /chroot/bash/bin
</pre>
Dizinimizdeki(lib64) kütüphaneler ile test edeceğimiz bash kabuğu için yeterli komutları çalıştırabiliriz.İhitiyacım olan <em> cp,cat,touch,mkdir,rm,mv</em> komutlarını kopyalayalım.
<pre># cp /bin/cp /chroot/bash/bin</pre>
<pre># cp /bin/mv /chroot/bash/bin</pre>
<pre># cp /bin/cat /chroot/bash/bin</pre>
<pre># cp /bin/rm /chroot/bash/bin</pre>
<pre># cp /bin/mkdir /chroot/bash/bin</pre>
<pre># cp /bin/touch /chroot/bash/bin
</pre>
Kabuğumuz için ihtiyacımız olan komutlarını koyduktan sonra artık kısıtlı bash kabuğumuza giriş yapabiliriz.
<pre># chroot /chroot/bash /bin/bash</pre>
Hiçbir hata almadıysanız kabuk ortamına girdiniz,şimdi koyduğunuz komutları test edebilirsiniz.</body></html>