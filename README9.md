# security

![Screenshot (50)](https://user-images.githubusercontent.com/99132039/171043162-50ee47af-eb5d-4ce9-84dc-f1ed23f5814f.png)

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

999  parking-lot                      active    

Fa0/2, Fa0/3, Fa0/4, Fa0/7

Fa0/8, Fa0/9, Fa0/10, Fa0/11

Fa0/12, Fa0/13, Fa0/14, Fa0/15

Fa0/16, Fa0/17, Fa0/18, Fa0/19

Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                
Fa0/24, Gig0/1, Gig0/2

## настройка безопасности access портов

- настраиваем port-security sw1

Sw1#sh port-security int f0/6

Port Security              : Enabled

Port Status                : Secure-up

Violation Mode             : Restrict

Aging Time                 : 60 mins

Aging Type                 : Inactive

SecureStatic Address Aging : Disabled

Maximum MAC Addresses      : 3

- sw2

Sw2#sh port-security int f0/18

Port Security              : Disabled

Port Status                : Secure-down

Violation Mode             : Protect

Aging Time                 : 60 mins

Aging Type                 : Absolute

SecureStatic Address Aging : Disabled

Maximum MAC Addresses      : 2

## dhcp snooping

Sw2(config)#ip dhcp snooping

Sw2(config)#int f0/1

Sw2(config-if)#ip dhcp snooping trust

Sw2(config-if)#int f0/18

Sw2(config-if)#ip dhcp snooping limit rate 5

Sw2(config)#ip dhcp snooping vlan 10

## bpdu guard и portfast

Sw2(config-if)#spanning-tree portfast 

Sw2(config-if)#spanning-tree bpduguard enable

## проверяем связь

![Screenshot (49)](https://user-images.githubusercontent.com/99132039/171043172-057f245d-518d-4379-8094-251d47865b39.png)
