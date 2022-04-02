# SSH

- выполняем базовую настройку свитча и роутера

- настраиваем ssh и виртуальные линии на свитче

SW1(config)#no ip domain-lo

SW1(config)#no ip domain-lookup 

SW1(config)#ip domain-n

SW1(config)#ip domain-name SW1

SW1(config)#username admin sec adm1n

SW1(config)#crypto key generate rsa 


SW1(config)#line vty 0 4

SW1(config-line)#login local

SW1(config-line)#tran

SW1(config-line)#transport in

SW1(config-line)#transport input ssh

- аналогично настраиваем роутер

R1(config)#no ip domain-lookup 

R1(config)#ip domain-n

R1(config)#ip domain-name R1

R1(config)#username admin sec adm1n

R1(config)#ip ssh version 2

Please create RSA keys (of at least 768 bits size) to enable SSH v2.

R1(config)#crypto key gen

R1(config)#crypto key generate rsa


R1(config)#line vty 0 4

R1(config-line)#login local

R1(config-line)#tr

R1(config-line)#transport in

R1(config-line)#transport input ssh

- проверяем связь в сети

![Screenshot (26)](https://user-images.githubusercontent.com/99132039/161400438-7ba52296-292d-42a1-a9aa-6a4725accfba.png)

- пробуем подключиться к R1 по ssh

