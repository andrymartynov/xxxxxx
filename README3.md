# Создание ipv6 топологии

- после базовой настройки R1 включаем маршрутизацию и задаем ipv6 настройки

R1(config)#ipv6 unicast-routing

R1(config)#int g0/0/0

R1(config-if)#ipv6 add 2001:db8:acad:a ::1/64

R1(config-if)#ipv6 add fe80::1 link-local 

R1(config-if)#no sh

R1(config)#int g0/0/1
	
R1(config-if)#ipv6 add  2001:db8:acad:1::1/64

R1(config-if)#ipv6 add fe80::1 link-local 

R1(config-if)#no sh

- аналогично настраиваем SW1

- задаем ipv6 адрес и шлюз по умолчанию fe80::1 pc-a и pc-b 

- проверяем сквозное соединение с помощью PC-A

C:\>ping 2001:db8:acad:1::b

Pinging 2001:db8:acad:1::b with 32 bytes of data:

Reply from 2001:DB8:ACAD:1::B: bytes=32 time=2014ms TTL=255

Reply from 2001:DB8:ACAD:1::B: bytes=32 time<1ms TTL=255

Reply from 2001:DB8:ACAD:1::B: bytes=32 time<1ms TTL=255

Reply from 2001:DB8:ACAD:1::B: bytes=32 time<1ms TTL=255

Ping statistics for 2001:DB8:ACAD:1::B:
  
  Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:
  
  Minimum = 0ms, Maximum = 2014ms, Average = 503ms

C:\>ping fe80::1

Pinging fe80::1 with 32 bytes of data:

Reply from FE80::1: bytes=32 time<1ms TTL=255

Reply from FE80::1: bytes=32 time<1ms TTL=255

Reply from FE80::1: bytes=32 time<1ms TTL=255

Reply from FE80::1: bytes=32 time<1ms TTL=255

Ping statistics for FE80::1:

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:
 
 Minimum = 0ms, Maximum = 0ms, Average = 0ms

C:\>tracert 2001:DB8:ACAD:A::3

Tracing route to 2001:DB8:ACAD:A::3 over a maximum of 30 hops: 

  1   0 ms      0 ms      0 ms      2001:DB8:ACAD:1::1
  
  2   1 ms      0 ms      0 ms      2001:DB8:ACAD:A::3

Trace complete.

- аналогичные действия проводим с PC-B

C:\>ping 2001:DB8:ACAD:1::3

Pinging 2001:DB8:ACAD:1::3 with 32 bytes of data:

Reply from 2001:DB8:ACAD:1::3: bytes=32 time<1ms TTL=127

Reply from 2001:DB8:ACAD:1::3: bytes=32 time=3ms TTL=127

Reply from 2001:DB8:ACAD:1::3: bytes=32 time<1ms TTL=127

Reply from 2001:DB8:ACAD:1::3: bytes=32 time<1ms TTL=127

Ping statistics for 2001:DB8:ACAD:1::3:

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:

Minimum = 0ms, Maximum = 3ms, Average = 0ms

C:\>ping fe80::1

Pinging fe80::1 with 32 bytes of data:

Reply from FE80::1: bytes=32 time<1ms TTL=255

Reply from FE80::1: bytes=32 time<1ms TTL=255

Reply from FE80::1: bytes=32 time<1ms TTL=255

Reply from FE80::1: bytes=32 time<1ms TTL=255

Ping statistics for FE80::1:

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:

Minimum = 0ms, Maximum = 0ms, Average = 0ms



