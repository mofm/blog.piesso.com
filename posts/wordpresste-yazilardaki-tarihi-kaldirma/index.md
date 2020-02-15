<html><body><p>Wordpress blogunuzda yazılarınızın üstünde çıkan "kategori,tarih,saat,meta tag,yazar"gibi bilgilerin gözkmesini istemiyorsanız ,aşağıdaki değişikleri hem temanızın index.php,hemde single.php adlı dosyalarında yapın :
</p><pre>1.  " <em>&lt;?php the_date('','&lt;h2&gt;','&lt;/h2&gt;'); ?&gt;</em> " <strong>yukarda çıkan büyük tarihi kaldırmak için  bulup silin.</strong></pre>
<pre>2. "  <em>&lt;?php _e("Filed under:"); ?&gt; &lt;?php the_category(',') ?&gt; &amp;#8212;</em> " <strong>kategoriyi kaldırmak için ,</strong></pre>
<pre>3. "  <em>&lt;?php the_tags(__('Tags: '), ', ', ' &amp;#8212; '); ?&gt;</em> " <strong>meta tagleri kaldırmak için,</strong></pre>
<pre>4. " <em>&lt;?php the_author() ?&gt;</em> " <strong>yazar yazısını kaldırmak için,</strong></pre>
<pre>5. " <em>&lt;?php the_time() ?&gt;</em> " <strong>konunun yazılma saati kaldırmak için dosyalardan bulup silin.</strong></pre></body></html>