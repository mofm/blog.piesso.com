<html><body><p>Apache web sunucunuzun IPv6 bağlantılarını dinlemesi istiyorsanız;

	</p><li> İlk olarak IPv6 desteğini vererek derleyen : ./configure --enable-rule=INET6</li>
	<li> Gentoo Linux kullanıcılarının "ipv6" use flag'ini aktif etmeleri yeterli.</li>

IPv6 desteği ile apache'i kurduktan sonra;

Sadece 'tek IP' IPv6 bağlantısı ve 80 portu  için:

Listen [2001:db8::b00:20ff:fca7:ddea]:80

Tüm IPv6 bağlantılarını ve 80 portunu dinlemesi için :

Listen [::]:80 </body></html>