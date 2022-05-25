# DHCPv6


## задаем IPv6 адреса роутерам и проводим базовую настройку

R1(config)#int g0/0/0

R1(config-if)#ipv6 add 2001:db8:acad:2::1/64

R1(config-if)#ipv6 add fe80::1 l

R1(config-if)#no sh

R1(config)#ipv6 route 0:0:0:0::0/64 2001:db8:acad:2::2

R1(config)#ipv6 unicast-routing

- провереям связь между роутерами

- проверяем работу SLAAC с помощью PC1

## настраиваем DHCPv6 на R1

### без состояния

R1(config)#ipv6 dhcp pool R1-STATELESS
	
R1(config-dhcpv6)#dns-server 2001:db8:acad::254

R1(config-dhcpv6)#domain-name stateless.com

R1(config)#int g0/0/1

R1(config-if)#ipv6 nd other-config-flag 

R1(config-if)#ipv6 dhcp server R1-STATELESS

- вводим команду ipconfig /all на PC1 и наблюдаем появление DNS суффикса

### с сохоанением состояния

R1(config)#ipv6 dhcp pool R2-STATEFUL

R1(config-dhcpv6)#address prefix 2001:db8:acad:3:aaa::/80

R1(config-dhcpv6)#dns-server 2001:db8:acad::254

R1(config-dhcpv6)#domain-name stateful.com

R1(config-dhcpv6)#int g0/0/0

R1(config-if)#ipv6 dhcp server R2-STATEFUL

- настраиваем ретрансляцию

*тут возникла проблема*

R2(config-if)#ipv6 dhcp relay destination 2001:db8:acad:2::1/64 g0/0/0

% Invalid input detected at '^' marker.

*трейсер говорит что команды не существует, судя по форумам у него в принципе проблемы с этой командой*
