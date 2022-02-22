# SW and R basic settings



- задача: произвести базовую настройку коммутатора и маршрутизатора, создать пароли, задать IP адрес, установить и проверить соединение коммутатора и маршрутизатора и его состояние
## SW settings
- переход в привелегированный режим

Switch>en
- режим глобальной настройки

Switch#conf t

Enter configuration commands, one per line.  End with CNTL/Z.
- имя устройства
Switch(config)#host SW1
- баннер
SW1(config)#banner motd @

Enter TEXT message.  End with the character '@'.

Achtung! @
- создание паролей
 
SW1(config)#enable sec class

SW1(config)#line console 0

SW1(config-line)#logging sync

SW1(config-line)#password class

SW1(config-line)#login

SW1(config-line)#

SW1#
%SYS-5-CONFIG_I: Configured from console by console

SW1#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

SW1(config)#line vty

% Incomplete command.

SW1(config)#line vty ?

<0-15>  First Line number
- настройка виртуальных линий
SW1(config)#line vty line vty 0 4
                     ^
% Invalid input detected at '^' marker.
 
SW1(config)#line vty 0 4
- пароль
SW1(config-line)#password class

SW1(config-line)#login

SW1(config-line)#transport input all

SW1(config-line)#

SW1#
%SYS-5-CONFIG_I: Configured from console by console

SW1#conf int

^
% Invalid input detected at '^' marker.
 - настройка ip
 
SW1#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

SW1(config)#conf int
             ^
% Invalid input detected at '^' marker.
	
SW1(config)#conf int ?

% Unrecognized command

SW1(config)#int vlan 1

SW1(config-if)#ip add ?

A.B.C.D  IP address
  dhcp     IP Address negotiated via DHCP

SW1(config-if)#ip add ip add 10.0.0.10 255.0.1.0
                      ^
% Invalid input detected at '^' marker.
	
SW1(config-if)#ip add 10.0.0.10 255.0.1.0

Bad mask 0xFF000100 for address 10.0.0.10

SW1(config-if)#no sh

SW1(config-if)#

%LINK-5-CHANGED: Interface Vlan1, changed state to up

SW1(config-if)#

SW1#

%SYS-5-CONFIG_I: Configured from console by console

SW1#copy run start

Destination filename [startup-config]? 

Building configuration...

[OK]

SW1#exit

### Router settings
 - ip 
 
Router>en

Router#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

Router(config)#int g0/0/0

Router(config-if)#ip add 10.0.0.1

% Incomplete command.

Router(config-if)#ip add 10.0.0.1 ?

A.B.C.D  IP subnet mask

Router(config-if)#ip add 10.0.0.1 255.0.0.0

Router(config-if)#no sh


Router(config-if)#

%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up

Router(config-if)#end

Router#

%SYS-5-CONFIG_I: Configured from console by console
- hostname
 
Router#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

Router(config)#host R1


R1#exit
