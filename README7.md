# STP



## базовая настройка свитчей (на примере SW1)

Switch(config)#host SW1

SW1(config)#int vlan 1

SW1(config-if)#ip add 192.168.1.1 255.255.255.0

SW1(config-if)#no sh

- проверка связи устройств в сети

SW1#ping 192.168.1.3

Type escape sequence to abort.

Sending 5, 100-byte ICMP Echos to 192.168.1.3, timeout is 2 seconds:

..!!!

Success rate is 60 percent (3/5), round-trip min/avg/max = 0/0/0 ms

SW1#ping 192.168.1.2

Type escape sequence to abort.

Sending 5, 100-byte ICMP Echos to 192.168.1.2, timeout is 2 seconds:

..!!!

Success rate is 60 percent (3/5), round-trip min/avg/max = 0/0/0 ms

SW2#ping 192.168.1.3

Type escape sequence to abort.

Sending 5, 100-byte ICMP Echos to 192.168.1.3, timeout is 2 seconds:

..!!!

Success rate is 60 percent (3/5), round-trip min/avg/max = 0/0/0 ms

## определение корневого моста


- выключаем все порты

- создаем транки 

- включаем f0/2 и f0/4 на всех коммутаторах

- наблюдаем данные STP

SW1#sh spanning-tree 

VLAN0001

Spanning tree enabled protocol ieee

Root ID    Priority    32769
  
  Address     0005.5E1A.D7A7
 
 Cost        19

Port        4(FastEthernet0/4)

Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
 
 Address     0090.2114.E7D2

Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
  
  Aging Time  20
  
  *корневой порт этого коммутатора - f0/4, назначенный порт - f0/2*
  
  - аналогично изучаем STP на других свитчах

*корневым мостом является SW3*

## наблюдение за процессом выбора портов протоколом STP, исходя из их стоимости

- изменяем стоимость рабочего порта на свитче с заблокированным портом

- видим изменение топологии STP, теперь заблокированный порт имеет SW1

- отменяем изменения стоимости порта

## наблюдение за процессом выбора портов протоколом STP, исходя из их приоритета 

- включаем порты f0/1, f0/3 на всез свитчах

- изучаем данные STP на некорневых мостах

*STP изменил корневой порт на порт с меньшим значением, так как стоимость портов не отличалась*

