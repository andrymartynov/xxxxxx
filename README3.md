# Создание ipv6 топологии

- после базовой настройки R1 включаем маршрутизацию и задаем ipv6 настройки

R1(config)#ipv6 unicast-routing

R1(config)#int g0/0/0

R1(config-if)#ipv6 add 2001:db8:acad:a::1/64

R1(config-if)#ipv6 add fe80::1 link-local 

R1(config-if)#no sh

R1(config)#int g0/0/1
	
R1(config-if)#ipv6 add  2001:db8:acad:1::1/64

R1(config-if)#ipv6 add fe80::1 link-local 

R1(config-if)#no sh

- аналогично настраиваем SW1

- задаем ipv6 настройки pc-a и pc-b

