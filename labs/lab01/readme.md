<h1> Лабораторная работа 1.  </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/topology.png>

<h2> Таблица адресации </h2>

| Устройство |  Интерфейс  |   IP-адрес    |  Маска подсети  | Шлюз по умолчанию |
|:----------:|:-----------:|:-------------:|:---------------:|:-----------------:|
| R1         | G0/0.3      | 192.168.3.1  | 255.255.255.0   |         -          |
|            | G0/0.4      | 192.168.4.1  | 255.255.255.0   |         -          |
|            | G0/0.8      |      -       |        -        |         -          |
| S1         | VLAN 3      | 192.168.3.11 | 255.255.255.0   | 192.168.3.1        |
| S2         | VLAN 3      | 192.168.3.12 | 255.255.255.0   | 192.168.3.1        |
| PC-A       | NIC         | 192.168.3.3  | 255.255.255.0   | 192.168.3.1        |
| PC-B       | NIC         | 192.168.4.3  | 255.255.255.0   | 192.168.4.1        |

<h2> Таблица VLAN </h2>

|   VLAN   |     Имя      |     Назначенный интерфейс     |
|:--------:|:------------:|:-----------------------------:|
| 3        | Management   | S1: VLAN 3                    |
|          |              | S2: VLAN 3                    |
|          |              | S1: G0/2                      |
| 4        | Operations   | S2: G0/2                      |
| 7        | ParkingLot   | S1: G0/3                      |
|          |              | S2: G0/0, G0/3                |
| 8        | Native       |               -               |

<h2> Задачи </h2>

<ol>
  <li> Создание сети и настройка основных параметров устройства. </li>
  <li> Создание сетей VLAN и назначение портов коммутатора. </li>
  <li> Настройка транка 802.1Q между коммутаторами. </li>
  <li> Настройка маршрутизации между сетями VLAN. </li>
  <li> Проверка работы маршрутизации между сетями VLAN. </li>
</ol>

<h2> Решение: </h2>

<p> Настраиваем базовую конфигурацию в соответствии с заданием. Создаем VLANы на коммутаторах, присваиваем их соответствующим портам, отключаем неиспользуемые порты. Настраиваем транк 802.1Q между коммутаторами: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/r1_interfaces.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/r1_vlans.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/s1_interfaces.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/s1_vlans.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/s2_interfaces.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/s2_vlans.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-a_ip.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-b_ip.png>

<p> Проверяем маршрутизацию между сетями: </p>

<p> Пинг от PC-A до шлюза по умолчанию: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-a_to_gateway.png>

<p> Пинг от PC-A до PC-B: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-a_to_pc-b.png>

<p> Пинг от PC-A до S2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-a_to_s2.png>

<p> Трассировка от PC-B до PC-A: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/trace_pc-b_to_pc-a.png>