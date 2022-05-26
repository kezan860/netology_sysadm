# Домашнее задание к занятию "3.7. Компьютерные сети, лекция 2"

1. Проверьте список доступных сетевых интерфейсов на вашем компьютере. Какие команды есть для этого в Linux и в Windows?

***Ответ:***

На Linux:
```
# ip a |awk '/state UP/{print $2}'
eth0:
```

```
# ifconfig
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:82ff:fe48:dcc2  prefixlen 64  scopeid 0x20<link>
        ether 02:42:82:48:dc:c2  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 5  bytes 526 (526.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.195.153.247  netmask 255.255.255.192  broadcast 10.195.153.255
        inet6 fe80::215:5dff:fe98:7818  prefixlen 64  scopeid 0x20<link>
        ether 00:15:5d:98:78:18  txqueuelen 1000  (Ethernet)
        RX packets 2865213  bytes 568362434 (568.3 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 202548  bytes 17350585 (17.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 1431714  bytes 333256081 (333.2 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1431714  bytes 333256081 (333.2 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
В Windows:
```
C:\Windows\system32>ipconfig /all

Настройка протокола IP для Windows

   Имя компьютера  . . . . . . . . . : PVV-00050
   Основной DNS-суффикс  . . . . . . : podsvirov.ru
   Тип узла. . . . . . . . . . . . . : Гибридный
   IP-маршрутизация включена . . . . : Нет
   WINS-прокси включен . . . . . . . : Нет
   Порядок просмотра суффиксов DNS . : podsvirov.ru

Адаптер Ethernet VirtualBox Host-Only Network:

   DNS-суффикс подключения . . . . . :
   Описание. . . . . . . . . . . . . : VirtualBox Host-Only Ethernet Adapter
   Физический адрес. . . . . . . . . : 0A-00-27-00-00-07
   DHCP включен. . . . . . . . . . . : Нет
   Автонастройка включена. . . . . . : Да
   Локальный IPv6-адрес канала . . . : fe80::75fa:2041:9b21:2f55%7(Основной)
   IPv4-адрес. . . . . . . . . . . . : 192.168.56.1(Основной)
   Маска подсети . . . . . . . . . . : 255.255.255.0
   Основной шлюз. . . . . . . . . :
   IAID DHCPv6 . . . . . . . . . . . : 671744039
   DUID клиента DHCPv6 . . . . . . . : 00-01-00-01-28-1C-4E-B6-10-78-D2-53-2B-4C
   DNS-серверы. . . . . . . . . . . : fec0:0:0:ffff::1%1
                                       fec0:0:0:ffff::2%1
                                       fec0:0:0:ffff::3%1
   NetBios через TCP/IP. . . . . . . . : Включен

Адаптер Ethernet Ethernet:

   DNS-суффикс подключения . . . . . :
   Описание. . . . . . . . . . . . . : Realtek PCIe GbE Family Controller
   Физический адрес. . . . . . . . . : 10-78-D2-53-2B-4C
   DHCP включен. . . . . . . . . . . : Нет
   Автонастройка включена. . . . . . : Да
   Локальный IPv6-адрес канала . . . : fe80::9aa:60da:4092:25a%12(Основной)
   IPv4-адрес. . . . . . . . . . . . : 10.195.154.99(Основной)
   Маска подсети . . . . . . . . . . : 255.255.255.224
   Основной шлюз. . . . . . . . . : 10.195.154.97
   IAID DHCPv6 . . . . . . . . . . . : 101742802
   DUID клиента DHCPv6 . . . . . . . : 00-01-00-01-28-1C-4E-B6-10-78-D2-53-2B-4C
   DNS-серверы. . . . . . . . . . . : 10.195.153.231
                                       10.132.16.200
   NetBios через TCP/IP. . . . . . . . : Включен
```

2. Какой протокол используется для распознавания соседа по сетевому интерфейсу? Какой пакет и команды есть в Linux для этого?

***Ответ:***
```
Протокол: lldp
Пакет: lldpd
Команда: lldpctl
```

3. Какая технология используется для разделения L2 коммутатора на несколько виртуальных сетей? Какой пакет и команды есть в Linux для этого? Приведите пример конфига.

***Ответ:***
```
На коммутаторах технология называется: VLAN (Virtual Area Network)

В Linux используется пакет: VLAN

Пример конфикурационного файла:
# cat /etc/network/interfaces
auto eth0.1400
iface eth0.1400 inet static
        address 192.168.1.1
        netmask 255.255.255.0
        vlan_raw_device eth0
```

4. Какие типы агрегации интерфейсов есть в Linux? Какие опции есть для балансировки нагрузки? Приведите пример конфига.

***Ответ:***

Типы агрегации интерфейсов в Linux:

**Mode-0(balance-rr)** - Режим используется по умолчанию. Balance-rr обеспечивается балансировку нагрузки и отказоустойчивость. В данном режиме сетевые пакеты отправляются “по кругу”, от первого интерфейса к последнему. Если выходят из строя интерфейсы, пакеты отправляются на остальные оставшиеся. Дополнительной настройки коммутатора не требуется при нахождении портов в одном коммутаторе. При разностных коммутаторах требуется дополнительная настройка.

**Mode-1(active-backup)** – Один из интерфейсов работает в активном режиме, остальные в ожидающем. При обнаружении проблемы на активном интерфейсе производится переключение на ожидающий интерфейс. Не требуется поддержки от коммутатора.

**Mode-2(balance-xor)** – Передача пакетов распределяется по типу входящего и исходящего трафика по формуле ((MAC src) XOR (MAC dest)) % число интерфейсов. Режим дает балансировку нагрузки и отказоустойчивость. Не требуется дополнительной настройки коммутатора/коммутаторов.

**Mode-3(broadcast)** – Происходит передача во все объединенные интерфейсы, тем самым обеспечивая отказоустойчивость. Рекомендуется только для использования MULTICAST трафика.

**Mode-4(802.3ad)** – динамическое объединение одинаковых портов. В данном режиме можно значительно увеличить пропускную способность входящего так и исходящего трафика. Для данного режима необходима поддержка и настройка коммутатора/коммутаторов.

**Mode-5(balance-tlb)** – Адаптивная балансировки нагрузки трафика. Входящий трафик получается только активным интерфейсом, исходящий распределяется в зависимости от текущей загрузки канала каждого интерфейса. Не требуется специальной поддержки и настройки коммутатора/коммутаторов.

**Mode-6(balance-alb)** – Адаптивная балансировка нагрузки. Отличается более совершенным алгоритмом балансировки нагрузки чем Mode-5). Обеспечивается балансировку нагрузки как исходящего так и входящего трафика. Не требуется специальной поддержки и настройки коммутатора/коммутаторов.


```Пример конфигурационного файла:
# The bond0 network interface
auto bond0
allow-hotplug bond0
iface bond0 inet static
address <ip-address>
netmask <netmask>
network <network-address>
broadcast <broadcast-address>
gateway <gateway-address>
dns-nameservers <nameserver-one> <nameserver-two>
dns-search <domain-name>
up /sbin/ifenslave bond0 eth0
up /sbin/ifenslave bond0 eth1
 
# The bond1 network interface
auto bond1
allow-hotplug bond1
iface bond1 inet static
address <ip-address>
netmask <netmask>
network <network-address>
broadcast <broadcast-address>
gateway <gateway-address>
dns-nameservers <nameserver-one> <nameserver-two>
dns-search <domain-name>
up /sbin/ifenslave bond1 eth2
up /sbin/ifenslave bond1 eth3
```


5. Сколько IP адресов в сети с маской /29 ? Сколько /29 подсетей можно получить из сети с маской /24. Приведите несколько примеров /29 подсетей внутри сети 10.10.10.0/24.

***Ответ:***
```
В сети с маской /29 8 IP-адресов, но 2 из них зарезервинованы, пример:
Сеть - 10.10.10.0/29
10.10.10.0 - зарезервинованный IP-адрес сети
10.10.10.2 - 10.10.10.6 - IP-адреса для хостов
10.10.10.7 - широковедательный IP-адрес

# ipcalc 10.10.10.0/29
Address:   10.10.10.0           00001010.00001010.00001010.00000 000
Netmask:   255.255.255.248 = 29 11111111.11111111.11111111.11111 000
Wildcard:  0.0.0.7              00000000.00000000.00000000.00000 111
=>
Network:   10.10.10.0/29        00001010.00001010.00001010.00000 000
HostMin:   10.10.10.1           00001010.00001010.00001010.00000 001
HostMax:   10.10.10.6           00001010.00001010.00001010.00000 110
Broadcast: 10.10.10.7           00001010.00001010.00001010.00000 111
Hosts/Net: 6                     Class A, Private Internet
```

В сети с маской /24 возможно создать 256 сетей с маской /29, пример:
```
# ipcalc 10.10.10.10/29
Address:   10.10.10.10          00001010.00001010.00001010.00001 010
Netmask:   255.255.255.248 = 29 11111111.11111111.11111111.11111 000
Wildcard:  0.0.0.7              00000000.00000000.00000000.00000 111
=>
Network:   10.10.10.8/29        00001010.00001010.00001010.00001 000
HostMin:   10.10.10.9           00001010.00001010.00001010.00001 001
HostMax:   10.10.10.14          00001010.00001010.00001010.00001 110
Broadcast: 10.10.10.15          00001010.00001010.00001010.00001 111
Hosts/Net: 6                     Class A, Private Internet
```


6. Задача: вас попросили организовать стык между 2-мя организациями. Диапазоны 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 уже заняты. Из какой подсети допустимо взять частные IP адреса? Маску выберите из расчета максимум 40-50 хостов внутри подсети.

***Ответ:***

Воспользуюсь выбором из подсети: 100.64.0.0 - 100.127.255.255

К примеру:
```
# ipcalc 100.64.0.0/27
Address:   100.64.0.0           01100100.01000000.00000000.000 00000
Netmask:   255.255.255.224 = 27 11111111.11111111.11111111.111 00000
Wildcard:  0.0.0.31             00000000.00000000.00000000.000 11111
=>
Network:   100.64.0.0/27        01100100.01000000.00000000.000 00000
HostMin:   100.64.0.1           01100100.01000000.00000000.000 00001
HostMax:   100.64.0.30          01100100.01000000.00000000.000 11110
Broadcast: 100.64.0.31          01100100.01000000.00000000.000 11111
Hosts/Net: 30                    Class A
```

7. Как проверить ARP таблицу в Linux, Windows? Как очистить ARP кеш полностью? Как из ARP таблицы удалить только один нужный IP?

***Ответ:***

```
Для проверки ARP таблицы как в Linux так и в Windows возможно воспользоваться командой:
Linux: 
# arp -a
Windows:
ARP.EXE -a

Для очистики кеша: netsh interface ip delete arpcache

Для удаления конкретного ip адреса: arp -d 192.168.100.25
```