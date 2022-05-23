# MAC адресация

- топология

![Screenshot (38)](https://user-images.githubusercontent.com/99132039/169853542-d80fba4a-93cb-4cf6-9317-8eeeb4d89262.png)

## базовая настройка устройств 

- SW1

Switch>en

Switch#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

Switch(config)#host Sw1

Sw1(config)#int vlan 1

Sw1(config-if)#ip add 192.168.1.11 255.255.255.0

Sw1(config-if)#no sh

__аналогично настраивается SW2__

- задаем ip адреса PC1 и PC2

## узнаем MAC адреса сетевых устройств

- PC1 и PC2

C:\>ipconfig /all

_узнаем MAC адрес_

Physical Address................: 00E0.A340.26C6

- SW1 и SW2

Sw1#sh int f0/1

  Hardware is Lance, address is 0009.7c63.4901 (bia 0009.7c63.4901)

## изучаем таблицу MAC адресов SW2

- до эхо запросов

Sw2#sh mac address-table 

Mac Address Table

-------------------------------------------

Vlan    Mac Address       Type        Ports

----    -----------       --------    -----

   1    0009.7c63.4901    DYNAMIC     Fa0/1 
   
- после эхо запросов

Sw2#sh mac address-table 

Mac Address Table

-------------------------------------------

Vlan    Mac Address       Type        Ports

----    -----------       --------    -----

   1    0002.1637.0600    DYNAMIC     Fa0/18
  
   1    0009.7c63.4901    DYNAMIC     Fa0/1
 
   1    00e0.a340.26c6    DYNAMIC     Fa0/1

*были отправлены эхо запросы с PC1 и PC2*

## очищаем таблицу мак адресов и снова смотрим ее

Sw2#clear mac address-table dynamic

Sw2#sh mac address-table 

Mac Address Table

-------------------------------------------

Vlan    Mac Address       Type        Ports

----    -----------       --------    -----

   1    0009.7c63.4901    DYNAMIC     Fa0/1
   
   *вновь видим только мак адрес самого Sw2*
   
   ## вводим команду arp -a на PC2 до и после эхо заппросов устройствам сети
   
   - до эхо запросов
   
   C:\>arp -a
 
 Internet Address      Physical Address      Type
 
 192.168.1.12          000c.cfe7.b5c0        dynamic
 
 - после 
 
 C:\>arp -a
  
  Internet Address      Physical Address      Type
  
  192.168.1.1           00e0.a340.26c6        dynamic
  
  192.168.1.11          0001.425b.e5e3        dynamic
  
  192.168.1.12          000c.cfe7.b5c0        dynamic

в arp кэше появились записи об устройствах, которым были отправлены эхо запросы

