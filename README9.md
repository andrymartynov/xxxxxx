# security

## настройки роутера

R1(config)#ip dhcp excluded-address 192.168.10.1 192.168.10.9

R1(config)#ip dhcp excluded-address 192.168.10.201 192.168.10.202

- создаем dhcp пул

R1(config)#ip dhcp pool students

R1(dhcp-config)#network 192.168.10.0 255.255.255.0

R1(dhcp-config)#default-router 192.168.10.1

R1(dhcp-config)#domain-name students.com

- loopback

R1(config)# int loopback 0

R1(config-if)#ip add 10.10.1.1 255.255.255.0

- 

R1(config)#int g0/0/1

R1(config-if)#description link to SW1

R1(config-if)#ip dhcp relay information trusted
	
R1(config-if)#ip add 192.168.10.1 255.255.255.0

R1(config-if)#no sh

R1(config-line)#logging synchronous

R1(config-line)#exec-timeout 0 0

- проверяем конфиг

R1#sh ip int br

Interface              IP-Address      OK? Method Status                Protocol 

GigabitEthernet0/0/0   unassigned      YES unset  administratively down down 

GigabitEthernet0/0/1   192.168.10.1    YES manual up                    up 

Loopback0              10.10.1.1       YES manual up                    up 

Vlan1                  unassigned      YES unset  administratively down down

## настраиваем свитчи

- создаем транк и задаем нейтив влан 333 на обоих свитчах

- задаем vlan 10 ip адреса на обоих свитчах

- задаем шлюз по умолчанию 192.168.10.1

- отключаем dtp

Sw1(config-if)#switchport nonegotiate 

Sw1#sh int f0/1 switchport

Negotiation of Trunking: Off

- настройка access портов

Sw1(config)#int f0/5

Sw1(config-if)#sw mode access 

Sw1(config-if)#sw access vlan 10

Sw1(config-if)#int f0/6

Sw1(config-if)#sw mode ac

Sw1(config-if)#sw ac vlan 10

Sw2(config)#int f0/18

Sw2(config-if)#sw mode ac

Sw2(config-if)#sw ac vlan 10

- перемещаем неиспользуемые порты в влан 999 и отключаем их

