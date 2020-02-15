<html><body><p>Özgür,başarılı ve neredeyse en kolay konfigure edilebilen  MTA yazılımı olan "Postfix"i spamlardan korumak için bir kaç yol.
"/etc/postfix/main.cf" dosyamızı bir metin editörü ile açıp birkaç konfigurasyon ekleyelim:
</p><blockquote># vi /etc/postfix/main.cf</blockquote>
ve aşağıdaki kodları bu dosyaya ekleyelim.

<em>
disable_vrfy_command = yes
smtpd_delay_reject = yes
smtpd_helo_required = yes
smtpd_helo_restrictions = permit_mynetworks,
reject_non_fqdn_hostname,
reject_invalid_hostname,
permit</em>

<em>smtpd_recipient_restrictions =
permit_sasl_authenticated,
reject_invalid_hostname,
reject_non_fqdn_hostname,
reject_non_fqdn_sender,
reject_non_fqdn_recipient,
reject_unknown_sender_domain,
reject_unknown_recipient_domain,
permit_mynetworks,
reject_rbl_client list.dsbl.org,
reject_rbl_client sbl.spamhaus.org,
reject_rbl_client cbl.abuseat.org,
reject_rbl_client dul.dnsbl.sorbs.net,
permit</em>

<em> </em></body></html>