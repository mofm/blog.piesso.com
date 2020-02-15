<html><body><p>Kıyıda köşede uzun süredir yatan sparc işlemcili <strong>SunFire T2000</strong> makinayı canlandırmaya karar verdim.Sparc portu olan tüm linux dağıtımlarını denememe rağmen "<em>kernel'</em>ini aşağıdaki gibi <em>panic</em>'liyordu".

<span><span><span style="color: black; font-family: arial; font-size: x-small;"><span style="color: black; font-family: arial; font-size: x-small;"><span style="font-family: Arial,Helvetica,sans-serif;">[    0.000000] I7: &lt;paging_init+0xa4c/0xe18&gt;
[    0.000000] Disabling lock debugging due to kernel taint
[    0.000000] Caller[00000000008ab1cc]: paging_init+0xa4c/0xe18
[    0.000000] Caller[00000000008a6db4]: setup_arch+0x394/0x3a4
[    0.000000] Caller[00000000008a4554]: start_kernel+0x74/0x36c
[    0.000000] Caller[0000000000723224]: tlb_fixup_done+0x80/0x88
[    0.000000] Caller[0000000000000000]: (null)
[    0.000000] Instruction DUMP: 92100010  7fee366e  90100011 &lt;d25a0000&gt; 11001ee
f  7ffa2a19  90122270  15001eef  90100011
[    0.000000] Kernel panic - not syncing: Attempted to kill the idle task!
[    0.000000] Call Trace:
[    0.000000]  [000000000045f360] do_exit+0x64/0x6ac
[    0.000000]  [0000000000427c08] die_if_kernel+0x264/0x290
[    0.000000]  [0000000000736f10] unhandled_fault+0x90/0x9c
[    0.000000]  [000000000073748c] do_sparc64_fault+0x570/0x650
[    0.000000]  [0000000000407900] sparc64_realfault_common+0x10/0x20
[    0.000000]  [00000000008a9714] sun4v_mdesc_init+0x1cc/0x2ac
[    0.000000]  [00000000008ab1cc] paging_init+0xa4c/0xe18
[    0.000000]  [00000000008a6db4] setup_arch+0x394/0x3a4
[    0.000000]  [00000000008a4554] start_kernel+0x74/0x36c
[    0.000000]  [0000000000723224] tlb_fixup_done+0x80/0x88
[    0.000000]  [0000000000000000] (null)
[    0.000000] Press Stop-A (L1-A) to return to the boot prom</span></span></span></span></span>

<span><span><span style="color: black; font-family: arial; font-size: x-small;"><span style="color: black; font-family: arial; font-size: x-small;"><span style="font-family: Arial,Helvetica,sans-serif;">Uzun bir uğraştan sonra sadece <strong>2.6.20-r4</strong> kernelli <strong>Gentoo 2007 Universal Live Cd </strong>açıp,sapasağlam bir Gentoo kurulumu yaptım.Fakat bu haliyle makinayı hiçbir güncelleme yapılamayacaktı.Çünkü güncel bir kernelde panik yapıyordu.</span></span></span></span></span>

<span><span><span style="color: black; font-family: arial; font-size: x-small;"><span style="color: black; font-family: arial; font-size: x-small;"><span style="font-family: Arial,Helvetica,sans-serif;">Mail listelerinde bir araştırmadan sonra aynı hata ile karşılaşan bir kişinin firmware güncelleyerek linux kurulumunu başarıyla yaptığını okudum.Hemen firmware güncellemeye geçtik.Tabi sorun burada da bitmiyor ,bir de "sc" ye giriş yapmak için parolayı bilmiyorduk ve birde parola sıfırlamaya giriştik.</span></span></span></span></span>
</p><h5><strong><span style="color: black; font-family: arial; font-size: x-small;"><span style="color: black; font-family: arial; font-size: x-small;"><span style="font-family: Arial,Helvetica,sans-serif;">Parolayı sıfırlamak için;</span></span></span></strong></h5>
<h6><span><span><span style="color: black; font-family: arial; font-size: x-small;"><span style="color: black; font-family: arial; font-size: x-small;"><span style="font-family: Arial,Helvetica,sans-serif;"><strong>1.</strong> İlk olarak güç bağlantısını çıkarın ve 5 sn bekleyin.Daha sonra tekrar bağlayın.
</span></span></span></span></span></h6>
<span><span><span style="color: black; font-family: arial; font-size: x-small;"><span style="color: black; font-family: arial; font-size: x-small;"><span style="font-family: Arial,Helvetica,sans-serif;"><strong>2</strong>.Alom boot etmeye başlayacaktır ve </span></span></span></span></span><em>"Return to Boot Monitor for Handshake ESC keypress detected."</em> yazısını gördüğünüz anda <em>"ESC"</em> tuşuna basın.

<strong>3.</strong> <em>"ESC" </em>tuşuna bastıktan sonra<em> "ALOM boot escape menu"</em> karşınıza gelecektir.
<pre>ALOM  Menu

 e - Erase ALOM NVRAM.
 m - Run POST Menu.
 R - Reset ALOM.
 r - Return to bootmon.
 Your selection:</pre>
<strong>4. </strong>Yukardaki gibi menu karşımıza çıktıktan sonra ilk <em>NVRAM</em>'i silip,daha sonra <em>ALOM</em>'u boot etmesine devam edelim.Bunun için ilk önce <strong>"e" </strong>ve daha sonra<strong> "r"</strong> yi tuşlayalım.

<strong>5.</strong>Bu adımlardan sonra "<strong>sc</strong>" ye doğrudan admin olarak giriş yapabileceksiniz.

<strong>Firmware Güncelleme :</strong>

SunFire T2000'in üstündeki firmware 6.1.10 ve bu firmware ile herhangi port edilmiş bir linux dağıtımını rahatlıkla kuramıyorsunuz.Bunun için firmware güncellemesi gerekli.Fakat dikkat edilecek nokta eğer  Oracle "CIS" numaranızı bilmiyorsanız "OpenSourceLab" ftp'sindeki 6.3.0 sürümünü indirip yükleyin.Aynı depoda 6.7.6 sürümü de mevcut fakat bu firmware geçersiz uyarısı alabilirsiniz."CIS" numaranız varsa zaten böyle bir sıkıntınız da olmayacaktır.

SunFire T2000 'de ya da herhangi Sun Sparc makina da "<strong>sc</strong>" ye düştükten sonra;

# showhost

komutuyla firmware versiyonunuzu öğrenebilirsiniz.Güncellemek için ben ilk olarak firmware'i indirip local'deki bir ftp sunucuya koydum ve flashupdate komutuyla güncelledim.Tabi ftp'ye bağlanmak için "NET MGT" portuna bağlantıyı takmanız lazım.Eğer ağınız otomatik ip almıyorsa;
<pre># setupsc</pre>
komutunu vererek ip atayabilirsiniz.

Firmware'i <a href="http://ftp.osuosl.org/pub/osl/tmp/124750-01/" target="_blank">buradan</a> indirip,bir public ftp'ye attıktan sonra aşağıdaki gibi güncelleyebilirsiniz:
<pre># flashupdate -s [ftp_ip_adresi] -f /pub/Sun_System_Firmware-6_3_0-Sun_Fire_T2000.bin
</pre>
Artık firmware'miz güncelledi."<strong>resetsc" </strong>komutunu verip yeniden başlatın ve <strong>"showhost"</strong> komutuyla güncellenip güncellenmediğini kontrol edin.

 </body></html>