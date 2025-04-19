<h1> Лабораторная работа 8. Настройка EIGRP </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab08/topology-lab08.png>

<h2> Задачи </h2>

<ol>
  <li> В офисе С.-Петербург настроить EIGRP. </li>
  <li> R32 получает только маршрут по умолчанию. </li>
  <li> R16-17 анонсируют только суммарные префиксы. </li>
  <li> Использовать EIGRP named-mode для настройки сети. </li>
</ol>

<h2> Решение: </h2>

<p>Начнем настройку сразу в именованном режиме:</p>

<h4>R16</h4>

<p>Т.к. для R32 маршрутизатор R16 является шлюзом сделаем суммарный префикс на интерфейсе e0/3 сразу 0.0.0.0/0; 
на интерфейс e0/1 (на R18) суммарный префикс - 10.78.0.0/16.</p>

<blockquote>
<p>router eigrp NG</p>
<p> !</p>
<p> address-family ipv4 unicast autonomous-system 78</p>
<p>  !</p>
<p>  af-interface Ethernet0/1</p>
<p>   summary-address 10.78.0.0 255.255.0.0</p>
<p>  exit-af-interface</p>
<p>  !</p>
<p>  af-interface Ethernet0/3</p>
<p>   summary-address 0.0.0.0 0.0.0.0</p>
<p>  exit-af-interface</p>
<p>  !</p>
<p>  topology base</p>
<p>  exit-af-topology</p>
<p>  network 10.78.34.0 0.0.0.3</p>
<p>  network 10.78.48.0 0.0.0.3</p>
<p>  network 10.78.99.0 0.0.0.255</p>
<p>  network 10.78.106.0 0.0.0.255</p>
<p>  network 10.78.108.0 0.0.0.255</p>
<p>  network 10.78.199.16 0.0.0.0</p>
<p>  eigrp router-id 10.78.199.16</p>
<p> exit-address-family</p>
</blockquote>

<p>Для того чтобы анонсировать на R32 маршрут по умолчанию (0.0.0.0/0), таже добавим на R16 в список сетей 0.0.0.0:</p>

<blockquote>
<p>router eigrp NG</p>
<p> !</p>
<p> address-family ipv4 unicast autonomous-system 78</p>
<p>  !</p>
<p>  network 0.0.0.0 0.0.0.0</p>
</blockquote>

<p>Добавим 0.0.0.0/0 в префикс-лист</p>

<blockquote>
<p>ip prefix-list R32 seq 10 permit 0.0.0.0/0 le 32</p>
</blockquote>

<p>И распространим префикс-лист на интерфейсе e0/3</p>

<blockquote>
<p>topology base</p>
<p> distribute-list prefix R32 out Ethernet0/3</p>
</blockquote>

<h4>R17</h4>

<p>На интерфейс e0/1 (на R18) суммарный интерфейс - 10.78.0.0/16.</p>

<blockquote>
<p> router eigrp NG</p>
<p> !</p>
<p> address-family ipv4 unicast autonomous-system 78</p>
<p>  !</p>
<p>  af-interface Ethernet0/1</p>
<p>   summary-address 10.78.0.0 255.255.0.0</p>
<p>  exit-af-interface</p>
<p>  !</p>
<p>  topology base</p>
<p>  exit-af-topology</p>
<p>  network 10.78.35.0 0.0.0.3</p>
<p>  network 10.78.99.0 0.0.0.255</p>
<p>  network 10.78.106.0 0.0.0.255</p>
<p>  network 10.78.108.0 0.0.0.255</p>
<p>  network 10.78.199.17 0.0.0.0</p>
<p>  eigrp router-id 10.78.199.17</p>
<p> exit-address-family</p>
</blockquote>

<p>Остальные аналогично:</p>

<h4>R18</h4>

<blockquote>
<p>router eigrp NG</p>
<p> !</p>
<p> address-family ipv4 unicast autonomous-system 78</p>
<p>  !</p>
<p>  topology base</p>
<p>  exit-af-topology</p>
<p>  network 10.78.34.0 0.0.0.3</p>
<p>  network 10.78.35.0 0.0.0.3</p>
<p>  network 10.78.199.18 0.0.0.0</p>
<p>  eigrp router-id 10.78.199.18</p>
<p> exit-address-family</p>
</blockquote>

<h4>R32</h4>

<blockquote>
<p>router eigrp NG</p>
<p> !</p>
<p> address-family ipv4 unicast autonomous-system 78</p>
<p>  !</p>
<p>  topology base</p>
<p>  exit-af-topology</p>
<p>  network 10.78.48.0 0.0.0.3</p>
<p>  network 10.78.199.32 0.0.0.0</p>
<p>  eigrp router-id 10.78.199.32</p>
<p> exit-address-family</p>
</blockquote>

<p>Маршруты:</p>

<h4>R16</h4>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab08/r16_routes.png>

<h4>R17</h4>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab08/r17_routes.png>

<h4>R18</h4>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab08/r18_routes.png>

<h4>R32</h4>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab08/r32_routes.png>


<p>Доступность устройств:</p>

<p>R18 - R32</p>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab08/ping_r32.png>

<p>R18 - VPC8</p>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab08/ping_vpc8.png>

<p>R32 - VPC6</p>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab08/ping_vpc6.png>
