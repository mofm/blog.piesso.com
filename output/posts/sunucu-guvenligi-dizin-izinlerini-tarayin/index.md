<html><body><p>Sisteminizde herkes ve grup tarafından yazılabilir dizinler güvenlik açısından büyük bir risk oluşturur.Bu riski ortadan kaldırmak için sistemimizdeki tüm dizinlerin izinlerini tarayın.

<strong>*</strong> Sisteminizde herkes ve grup tarafından yazılabilir dizinleri tarayın:



</p><blockquote>$ find / -type d \( -perm -g+w -o -perm -o+w \) -exec ls -lad {} \;
</blockquote>


<strong>* </strong>Sisteminizde izinleri ayarlanmamış dizinleri tarayın:



<blockquote>$ find / -type d \( -perm -g+w -o -perm -o+w \) \ -not -perm -a+t -exec ls -lad {} \;</blockquote>

</body></html>