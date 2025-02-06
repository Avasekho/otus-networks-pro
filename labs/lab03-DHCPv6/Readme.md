<h1> Лабораторная работа 3. Реализация DHCPv6 </h1> 
<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/topology.png>

<h2> Таблица адресации </h2>

| Устройство |  Интерфейс  |       IPv6-адрес        |
|:----------:|:-----------:|:-----------------------:|
| R1         | G0/0        | 2001:db8:acad:2::1 /64  |
|            |             | fe80::1                 |
|            | G0/1        | 2001:db8:acad:1::1/64   |
|            |             | fe80::1                 |
| R2         | G0/0        | 2001:db8:acad:2::2/64   |
|            |             | fe80::2                 |
|            | G0/1        | 2001:db8:acad:3::1 /64  |
|            |             | fe80::1                 |
| PC-A       | NIC         | DHCP                    |
| PC-B       | NIC         | DHCP                    |

<h2> Задачи </h2>

<ol>
  <li> 1. Создание сети и настройка основных параметров устройства. </li>
  <li> 2. Проверка назначения адреса SLAAC от R1. </li>
  <li> 3. Настройка и проверка сервера Stateless DHCPv6 на R1. </li>
  <li> 4. Настройка и проверка Stateful DHCPv6 сервера на R1. </li>
  <li> 5. Настройка и проверка DHCPv6 Relay на R2. </li>
</ol>


<h2> Решение: </h2>

<p> Часть 1. Cоздание сети и настройка основных параметров устройства: </p>

<p> Настраиваем базовую конфигурацию маршрутизаторов в соответствии с заданием. Настраиваем адреса на R1 и R2; настраиваем шлюз по умолчанию для R1 и R2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/R1_ipv6_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/R2_ipv6_interfaces.png>

<p> Проверяем доступность с R1 интерфейса G0/1 на R2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/R1_ping_1.png>

<p> Часть 2. Проверка назначения адреса SLAAC от R1: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-A_ipv6_1.png>

<blockquote>
Откуда взялась host-id часть адреса? 
</blockquote>
<p> Генерируется на основе MAC-адреса интерфейса. </p>

<p> Часть 3. Настройка и проверка сервера Stateless DHCPv6 на R1: </p>

<p> Полные настройки IPv6 на PC-A: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-A_ipv6_2.png>

<p> Настраиваем Stateless DHCPv6 на R1 в соответствии с заданием. Проверяем обновленные настройки IPv6 на PC-A: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-A_ipv6_3.png>

<p> Проверяем пинг до интерфейса G0/1 R2 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-A_ping_1.png>

<p> Часть 4. Настройка и проверка Stateful DHCPv6 сервера на R1: </p>

<p> Настраиваем Stateful DHCPv6 на R1 в соответствии с заданием. </p>

<p> Часть 5. Настройка и проверка DHCPv6 Relay на R2: </p>

<p> Полные настройки IPv6 на PC-B: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-B_ipv6_1.png>

<p> Настраиваем DHCPv6 Relay на R2 в соответствии с заданием. Проверяем обновленные настройки IPv6 на PC-B: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-B_ipv6_2.png>

<p> Проверяем пинг до интерфейса G0/1 R1 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-B_ping_1.png>