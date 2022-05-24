# DHCPv6


## задаем IPv6 адреса роутерам

R2(config)#ipv6 uni

R2(config)#ipv6 unicast-routing 

R2(config)#int g0/0/0

R2(config-if)#ipv6 add 2001:db8:acad:2::2/64

R2(config-if)#ipv6 add fe80::2 link

R2(config-if)#ipv6 add fe80::2 link-local 

R2(config-if)#no sh

