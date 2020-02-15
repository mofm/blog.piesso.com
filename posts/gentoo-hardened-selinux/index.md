<html><body><p>Geçtiğimiz günlerde Gentoo depolarına kullancılar tarafından test edilmesi için Gentoo Hardened/SELinux sanal makina kalıbı eklendi.Denemek isteyenler için herhangi bir Gentoo yansısından "<strong>experimental/amd64/qemu-selinux/</strong>" yolunu izleyerek indirip,test edebilirler.Sıkıştırılmış hali yaklaşık 158 MB olan kalıp açılınca 1.6 GB gibi yer kaplayacaktır.
Dikkatlerden kaçmamasi için geliştiricilerin depoya koyduğu nota bakmada fayda var.

<code>SELinux node
============

The SELinux node VM image is a qemu/kvm-compatible image that runs a base Gentoo
Linux installation, using the Gentoo Hardened toolchain and kernel (including
grSecurity and PaX) and with SELinux enabled in enforcing mode.

To run it successfully on your system, please run it with the "-cpu kvm64" qemu
option to enable the KVM 64-bit processor.

The image provides three accounts by default: root (with password "rootpass"),
user (with password "userpass") and oper (with password "operpass"). These
accounts map to the SELinux users/roles of root (sysadm_r), user_u (user_r) and
staff_u (staff_r).

Once booted, you can find more information about the SELinux node using
"man selinuxnode".

For more information or feedback, please contact Sven Vermeulen through
swift@gentoo.org

Extracting
----------

The image is compressed using xz. You can decompress it using "xz -d <filename>".
Expect the extracted image to be around 1.4 GiB.</filename></code>


Ayrıca kalıbı boot etmeden önce virtio driver'larını yüklemeniz gerekmekte( Paravirtualized VM ).</p></body></html>