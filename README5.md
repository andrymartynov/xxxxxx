# vlan

![Screenshot (37)](https://user-images.githubusercontent.com/99132039/169118430-897d938e-ad33-4c58-99e0-ab6cdf17096c.png)

## настраиваем транк на коммутаторе SW1

- создаем транк между коммутаторами SW1 и SW2

SW1(config-vlan)#int f0/1

SW1(config-if)#sw mode trunk

- создаем и называем вланы 

SW1(config)#vlan 1000

SW1(config-vlan)#name NATIVE

SW1(config-vlan)#vlan 10

SW1(config-vlan)#name ADM

SW1(config-vlan)#vlan 20

SW1(config-vlan)#name SALES

SW1(config-vlan)#vlan 30

SW1(config-vlan)#name OPERATIONS

SW1(config-vlan)#int f0/1

*также указывем нативный влан*

SW1(config-if)#sw tr native vlan 1000

- задаем IP адрес vlan 10 на SW1

SW1(config)#int vlan 10

SW1(config-if)#ip add 192.168.10.11 255.255.255.0

### аналогично настраиваем транк на SW2 и задаем IP vlan 10 на SW2

## настраиваем транк до маршрутизатора

SW1(config-if)#int f0/6

SW1(config-if)#sw mode tr

SW1(config-if)#sw tr native vlan 1000

## назначаем IP адреса вланам на SW1 согласно таблице адресации

SW1(config)#int vlan 10

SW1(config-if)#

%LINK-5-CHANGED: Interface Vlan10, changed state to up

SW1(config-if)#ip add 192.168.10.11 255.255.255.0

SW1(config-if)#^Z

*аналогично даем IP адреса остальным vlan*

- также указываем шлюз по умолчанию

SW1(config)#ip def

SW1(config)#ip default-gateway 192.168.10.1

### аналогично разбираемся с SW2

## настраиваем роутер

- указываем энкапсуляцию и задаем IP адреса подинтерфейсам

R1(config-subif)#int g0/0/1.30

R1(config-subif)#enc d

R1(config-subif)#enc dot1Q 30

R1(config-subif)#ip add 192.168.30.1 255.255.255.0

R1(config-subif)#int g0/0/1.1000

R1(config-subif)#enc dot1Q 1000 native

*разумеется предварительно включаем интерфейс G0/0/1*

## создаем access порт к PC-1 (и PC-2 аналогично)

SW1(config)#int f0/5

SW1(config-if)#sw mode access

SW1(config-if)#sw ac vlan 20

## разбираемся с PC-1 и PC-2

![Screenshot (33)](https://user-images.githubusercontent.com/99132039/166460547-a891728c-a478-49d6-9fba-b23baf2d3846.png)

![Screenshot (33)](https://user-images.githubusercontent.com/99132039/166460547-a891728c-a478-49d6-9fba-b23baf2d3846.png)

## проверяем работу сети

![Screenshot (35)](https://user-images.githubusercontent.com/99132039/166460805-805a64e7-a192-4ebf-8eef-ac6b5d068b73.png)

![Screenshot (36)](https://user-images.githubusercontent.com/99132039/166460808-6b5d65ae-897f-4ecd-af32-952319552d58.png)
