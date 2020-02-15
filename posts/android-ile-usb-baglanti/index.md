<html><body><p>Dün gece herhangi şekilde internet erişimim olmadığı için telefonumdaki interneti bilgisayara paylaştırmam gerekti.Fakat Android yüklü telefonu USB ile bağlayınca ,internete bağlanmadığını , çekirdeğin tanımadığını farkettim.Tabiki kerneli derlerken böyle birşey yapacağım aklıma gelmemişti ve USB Network Drivers'lara hiç dokunmamıştım .Kerneli yeniden derlemek başa düştü ve sizde derlerken böyle bir şeye ihtiyaç duyacaksanız aşağıdaki gibi çekirdeğinize desteği vermeyi unutmayın :)

# make menuconfig
</p><pre>Device Drivers ---&gt;
  [*] Network device support ---&gt;
    USB Network Adapters ---&gt;
      [*] Multi-purpose USB Networking Framework
        &lt;*&gt; CDC Ethernet support
        &lt;*&gt; CDC EEM support
        &lt;*&gt; Simple USB Network Links (CDC Ethernet subset)
          [*] Embedded ARM Linux links
  [*] USB Support ---&gt;
    &lt;*&gt; USB Modem (CDC ACM) support
    &lt;*&gt; USB Wireless Device Management support</pre>
 </body></html>