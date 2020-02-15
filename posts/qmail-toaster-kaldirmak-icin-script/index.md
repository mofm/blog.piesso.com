<html><body><a href="http://www.qmailtoaster.com/" target="_blank"><strong>Qmail-Toaster</strong></a> kurulumu için hazırlanmış olan scriptler işimizi kolaylaştırıyordu.Kaldırmak içinde yine bir script işimizi kolaylaşıtırıyor.Qmail-Toaster mail listesinde  bunun için hazırlanmış bir script ile karşılaştım .İhtiyacımız olduğunda kullanabiliriz.

<strong>NOT: </strong>Script içinde "<strong>MYSQLPW</strong>" için vpopmail veritabanının parolasını girip,düzenlenmeyi unutmayın!

Scripti dosya halinde indirmek için <a href="http://linux.piesso.com/programs/remove_toaster.sh" target="_blank">tıklayın</a> .
<pre>#!/bin/sh
# CentOS 5
# Remove Qmail-Toaster
# Removes all the qmailtoaster rpms except zlib.  Deletes all the needed users.
#Deletes the Database. Deletes ALL the files and directories left behind. THIS
#WILL WIPE THE SLATE CLEAN.  YOU WERE WARNED. No Guarantee it will work for you.
# Modify as you see fit. Pass improvements back to below email.
#
#
#
# Set mysql password
MYSQLPW=your pasword here
#
# Remove rpms in order of deps.
echo
echo "Removing *ALL* Toaster RPMs in order of deps, except zlib"
rpm -e simscan-toaster
rpm -e clamav-toaster
rpm -e spamassassin-toaster
rpm -e squirrelmail-toaster
rpm -e vqadmin-toaster
rpm -e isoqlog-toaster
rpm -e maildrop-toaster-devel
rpm -e maildrop-toaster
rpm -e qmailmrtg-toaster
rpm -e qmailadmin-toaster
rpm -e ezmlm-cgi-toaster
rpm -e ezmlm-toaster
rpm -e control-panel-toaster
rpm -e autorespond-toaster
rpm -e courier-imap-toaster
rpm -e qmail-pop3d-toaster
rpm -e qmail-toaster
rpm -e vpopmail-toaster
rpm -e ucspi-tcp-toaster
rpm -e daemontools-toaster
rpm -e send-emails-toaster
#
#Drop vpopmail database.
#
echo
echo "Dropping vpopmail database"
mysqladmin -f -uroot -p$MYSQLPW drop vpopmail
#
#Delete directories and files.
#
echo
echo "Removing all directories and files associated with Qmail-Toaster"
rm -f /etc/freshclam.conf.rpmsave
rm -f /etc/tcprules.d/tcp.smtp.rpmsave
rm -Rf /etc/ezmlm
rm -Rf /etc/isoqlog
rm -Rf /etc/log.d/scripts/services/vpopmail
rm -Rf /etc/log.d/scripts/services/courier
rm -Rf /etc/log.d/scripts/services/clamav
rm -Rf /etc/log.d/scripts/services/qmail
rm -f /usr/src/redhat/RPMS/i386/*toaster*.rpm
rm -f /usr/src/redhat/RPMS/noarch/*toaster*.rpm
rm -Rf /usr/share/toaster
rm -Rf /usr/share/clamav
rm -Rf /usr/src/qtms-install
rm -Rf /usr/src/qtms
rm -Rf /usr/share/doc/isoqlog
rm -Rf /usr/share/courier
rm -Rf /var/qmail
rm -Rf /var/log/clamav
rm -Rf /var/log/qmail
rm -Rf /home/vpopmail
echo
echo "All done."
#
#
exit
</pre></body></html>