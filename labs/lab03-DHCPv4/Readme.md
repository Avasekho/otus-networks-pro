<h1> Лабораторная работа 3. Реализация DHCPv4 </h1> 
<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/topology.png>

<h2> Таблица адресации </h2>

| Устройство |  Интерфейс  |   IP-адрес    |  Маска подсети  |  Шлюз по умолчанию  |
|:----------:|:-----------:|:-------------:|:---------------:|:-------------------:|
| R1         | G0/0        | 10.0.0.1      | 255.255.255.252 | -                   |
|            | G0/1        | -             | -               | -                   |
|            | G0/1.100    | 192.168.1.1   | 255.255.255.192 | -                   |
|            | G0/1.200    | 192.168.1.65  | 255.255.255.224 | -                   |
|            | G0/1.1000   | -             | -               | -                   |
| R2         | G0/0        | 10.0.0.2      | 255.255.255.252 | -                   |
|            | G0/1        | 192.168.1.97  | 255.255.255.240 | -                   |
| S1         | VLAN 200    | 192.168.1.66  | 255.255.255.224 | 192.168.1.65        |
| S2         | VLAN 1      | 192.168.1.98  | 255.255.255.240 | 192.168.1.97        |
| PC-A       | NIC         | DHCP          | DHCP            | DHCP                |
| PC-B       | NIC         | DHCP          | DHCP            | DHCP                |

<h2> Таблица VLAN </h2>

|  VLAN  |     Имя     |   Интерфейс   |
|:------:|:-----------:|:-------------:|
| 1      |      -      | S2: G0/3      |
| 100    | Clients     | S1: G0/2      |
| 200    | Management  | S1: VLAN 200  |
| 999    | Parking_Lot | S1: G0/0,G0/3 |
| 1000   | Native      | -             |

<h2> Задачи </h2>

<ol>
  <li> 1. Создание сети и настройка основных параметров устройства. </li>
  <li> 2. Настройка и проверка двух серверов DHCPv4 на R1. </li>
  <li> 3. Настройка и проверка DHCP-ретрансляции на R2. </li>
</ol>

<h2> Решение: </h2>

<p> Часть 1. Подбираем адреса для подсетей: </p>

<p> Подсеть A, требуется 58 хостов. Минимальный размер сети - 64 хоста. Маска сети /26 или 255.255.255.192; пул адресов - 192.168.1.1 - 192.168.1.62 </p>

<p> Подсеть B, требуется 28 хоста. Минимальный размер сети - 32 хоста. Маска сети /27 или 255.255.255.224; пул адресов - 192.168.1.65 - 192.168.1.94 </p>

<p> Подсеть C, требуется 12 хостов. Минимальный размер сети - 16 хостов. Маска сети /28 или 255.255.255.240; пул адресов - 192.168.1.97 - 192.168.1.110 </p>

<p> Настраиваем базовую конфигурацию маршрутизаторов в соответствии с заданием. Настраиваем субинтерфейсы на R1; настраиваем шлюз по умолчанию для R1 и R2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_vlans.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R2_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_ping_R2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R2_ping_R1.png>

<p> Пинг с R2 на второй интерфейс не работает, добавляем статикой адреса других сетей: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R2_ping_R1_err.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_ping_R2_2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R2_ping_R1_2.png>

<p> Настраиваем базовую конфигурацию коммутаторов в соответствии с заданием. Создаем VLANы на коммутаторах, присваиваем их соответствующим портам, отключаем неиспользуемые порты. Настраиваем транк 802.1Q между коммутаторами: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S1_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S1_vlans_q.png>

<blockquote>
Почему интерфейс S1 G0/1 был указан в VLAN 1? 
</blockquote>
<p>  Это сеть по умолчанию, а данный порт не настраивался на другие сети. После настройки его в качестве магистрального порта он больгше не отображается в результатах команды show vlan brief. </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S1_vlans.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S1_trunk.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S2_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S2_vlans.png>

<blockquote>
Какой IP-адрес был бы у ПК, если бы он был подключен к сети с помощью DHCP? 
</blockquote>
<p>  G0/2 - порт доступа для VLAN 100, значит адрес из пула 192.168.1.2 - 192.168.1.62 </p>

<p> Часть 2. Настройка и проверка двух серверов DHCPv4 на R1: </p>

<p> Настраиваем DHCP-сервер в соответствии с заданием. Проверяем статистику на сервере и ПК-клиенте: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_1.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_3.png>

<p> ПК получает адрес, интерфейсы маршрутизатора доступны: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-A_dhcp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-A_ping.png>


<p> Часть 3. Настройка и проверка DHCP-транслятора на R2. Добавляем DHCP-ретранслятор на интерфейс на R2. </p>

<p> Долго не мог найти сервер DHCP, т.к. он был настроен на подсеть B а не на подсеть С </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/dhcp_err.png>

<p> Долго не мог найти сервер DHCP, т.к. второй пул был настроен на подсеть B а не на подсеть С </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_4.png>

<p> После внесения изменений ПК смог получить адрес </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-B_dhcp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-B_dhcp_2.png>

<p> Интерфейс R1 также доступен </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-B_ping.png>

<p> На DHCP-сервере есть записи обоих выданных адресов для ПК </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_3.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_3.png>
