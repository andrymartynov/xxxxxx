- цель: создать сеть и изучить MAC-адреса устройств в ней


- настройка сети

- SW1

Switch>en

Switch#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

Switch(config)#host SW1

SW1(config)#banner motd @

Enter TEXT message.  End with the character '@'.

get da' hell out of here!(unlicensed invasion restricted)@

SW1(config)#enable secret class
	
SW1(config)#int vlan 1

SW1(config-if)#ip add 199.00.10.11 255.01.00.25

SW1(config-if)#exit

SW1(config)#

SW1#

%SYS-5-CONFIG_I: Configured from console by console

SW1#copy run start
Destination filename [startup-config]? 
Building configuration...
[OK]

- SW2 настроен аналогично

- МАС адреса РС

MAC адрес PC0 0006.2A88.C3B8

МАС адрес РС1 0030.A305.1AB6 

- адреса оборудования (SW1 и SW2)

SW1 0010.1137.1501 (bia 0010.1137.1501) 
SW2 000a.4178.da01 (bia 000a.4178.da01)

- MAC address table before and after ping

before

SW2#sh mac

SW2#sh mac add

SW2#sh mac address-table 

Mac Address Table

-------------------------------------------

Vlan    Mac Address       Type        Ports

----    -----------       --------    -----

   1    0010.1137.1501    DYNAMIC     Fa0/1
   
SW2#clear mac add

SW2#clear mac address-table dynamic

SW2#sh mac add

SW2#sh mac address-table 

Mac Address Table

-------------------------------------------

Vlan    Mac Address       Type        Ports

----    -----------       --------    -----

   1    0010.1137.1501    DYNAMIC     Fa0/1

after


