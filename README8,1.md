# DHCPv4

![Screenshot (59)](https://user-images.githubusercontent.com/99132039/171287113-dce4d625-012e-4ebc-b5aa-63e70002b653.png)

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

![Screenshot (53)](https://user-images.githubusercontent.com/99132039/171287130-a6723b0c-8b51-469d-8e20-72ffb8910775.png)

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

![Screenshot (54)](https://user-images.githubusercontent.com/99132039/171287134-ddc510c4-41fb-445d-ab82-1bf4aafc9630.png)

![Screenshot (55)](https://user-images.githubusercontent.com/99132039/171287102-6afdaf55-78d3-4eee-9cf6-01dfeb730a6b.png)

![Screenshot (56)](https://user-images.githubusercontent.com/99132039/171287108-cd1b0eb1-d839-4cfd-8198-c31012c907ce.png)

![Screenshot (57)](https://user-images.githubusercontent.com/99132039/171287109-6e711ae3-6988-44c6-8c8a-e80c65cae7f5.png)

![Screenshot (58)](https://user-images.githubusercontent.com/99132039/171287110-07f90bdc-3b96-4fc7-9281-11b40635f7b1.png)

R1#sh ip dhcp binding 

IP address       Client-ID/              Lease expiration        Type

Hardware address

192.168.1.6      0002.178D.BB9A           --                     Automatic

192.168.3.6      0005.5EC1.9322           --                     Automatic
