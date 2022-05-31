# DHCPv4

## настройка R1

R1(config-if)#int g0/0/1.100

R1(config-subif)#encapsulation dot1Q 100

R1(config-subif)#ip add 192.168.1.1 255.255.255.0

*если я правильно понял инструкцию, ip будет такой*

R1(config-subif)#int g0/0/1.200

R1(config-subif)#enc dot 200

R1(config-subif)#ip add 192.168.1.2 255.255.255.0

% 192.168.1.0 overlaps with GigabitEthernet0/0/1.100 *трейсер подсказал*

R1(config-subif)#ip add 192.168.2.1 255.255.255.0

R1(config-subif)#int g0/0/0

R1(config-if)#ip add 10.0.0.1 255.255.255.0

- и маршрут по умолчанию

