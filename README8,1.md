# DHCPv4

## настройка R1

R1(config-if)#int g0/0/1.100

R1(config-subif)#encapsulation dot1Q 100

R1(config-subif)#ip add 192.168.1.1 255.255.255.192

*если я правильно понял инструкцию, ip будет такой*

R1(config-subif)#int g0/0/1.200

R1(config-subif)#enc dot 200

R1(config-subif)#ip add 192.168.2.1 255.255.255.224

% 192.168.1.0 overlaps with GigabitEthernet0/0/1.100 *трейсер подсказал*

R1(config-subif)#ip add 192.168.2.1 255.255.255.0

R1(config-subif)#int g0/0/0

R1(config-if)#ip add 10.0.0.1 255.255.255.0

- и маршрут по умолчанию

R1(config)#ip route 0.0.0.0 0.0.0.0 10.0.0.2

R2(config)#ip route 0.0.0.0 0.0.0.0 10.0.0.1

R1#ping 10.0.0.2

Type escape sequence to abort.

Sending 5, 100-byte ICMP Echos to 10.0.0.2, timeout is 2 seconds:

.!!!!

Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms

## настраиваем свитчи



## и наконец DHCP

R1(config)#ip dh p R1

R1(dhcp-config)#default-router 192.168.1.1

R1(dhcp-config)#network 192.168.1.0 255.255.255.192

R1(dhcp-config)#dns-server R1-net1
	
R1(dhcp-config)#domain-name CCNA-LAB.com

R1(dhcp-config)#exit

R1(config)#ip dhcp ex 192.168.1.1 192.168.1.5

R1(config)#ip dhcp ex 192.168.2.1 192.168.2.5

R1(config)#ip dh pool R1_2

R1(dhcp-config)#default-router 192.168.2.1

R1(dhcp-config)#net 192.168.2.0 255.255.255.224

R1(dhcp-config)#domain-name CCNA-LAB1.com

R1(config)#ip dhcp pool R2_client_LAN

R1(dhcp-config)#default-router 10.0.0.1 *(в остальных пулах наверно тоже надо было этот адрес дать...)*

R1(dhcp-config)#net 192.168.3.0 255.255.255.128

R1(dhcp-config)#domain-name CCNA-LAB.com

R1(config)#ip dhcp ex 192.168.3.1 192.168.3.5 

- и еще один момент

R2(config-if)#ip helper-address 10.0.0.1

## тестируем



R1#sh ip dhcp binding 

IP address       Client-ID/              Lease expiration        Type

Hardware address

192.168.1.6      0002.178D.BB9A           --                     Automatic

192.168.3.6      0005.5EC1.9322           --                     Automatic

