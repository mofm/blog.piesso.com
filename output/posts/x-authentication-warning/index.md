<html><body><p>SquirrelMail webmail ya da diğer mail client programlarından mail gönderdiğiniz zaman mail header'ınızda aşağıdaki gibi uyarı alıyorsanız;

 

</p><blockquote>" X-Authentication-Warning: host.example.com: apache set sender to admin@example.com using -f "</blockquote>


yapmanız gereken "/etc/mail/trusted-users" dosyasına " apache " yi eklemek.

Örnek "trusted-users" dosyası:



<blockquote># trusted-users - users that can send mail as others without a warning
# apache, mailman, majordomo, uucp, are good candidates
apache</blockquote>


</body></html>