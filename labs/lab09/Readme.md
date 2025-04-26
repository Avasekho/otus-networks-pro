<h1> Лабораторная работа 9. Настройка BGP </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/topology-lab09.png>

<h2> Задачи </h2>

<ol>
  <li> Настроить eBGP между офисом Москва и двумя провайдерами - Киторн и Ламас. </li>
  <li> Настроить eBGP между провайдерами Киторн и Ламас. </li>
  <li> Настроить eBGP между Ламас и Триада. </li>
  <li> Настроить eBGP между офисом С.-Петербург и провайдером Триада. </li>
  <li> Организовать IP доступность между пограничным роутерами офисами Москва и С.-Петербург. </li>
</ol>

<h2> Решение: </h2>

<p>// Чтобы избежать возможных конфликтов при агрегации адресов 10.77.0.0/16 (сеть МСК) с Loopback адресами, адреса маршрутизаторов провайдеров изменены с 10.78.199.х на 10.10.199.х; изменения отражены в таблице в лабораторной 4. </p>

<h3>Начнем с офиса Москва:</h3>

<p>R14: </p>

<p>Создаем bgp AS1001, добавим для анонсирования Loopback-интерфейс, укажем всех напрямую подключенных соседей. Также добавим маршруты которые настроены по ospf. </p>

<blockquote>
<p>router bgp 1001 </p>
<p> network 10.77.199.14 mask 255.255.255.255 </p>
<p> redistribute ospf 14 </p>
<p> neighbor 10.77.25.2 remote-as 1001 </p>
<p> neighbor 10.77.26.1 remote-as 1001 </p>
<p> neighbor 10.77.27.1 remote-as 1001 </p>
<p> neighbor 10.77.33.2 remote-as 1001 </p>
<p> neighbor 77.58.86.54 remote-as 101 </p>
</blockquote>

<p>Аналогично второй пограничный маршрутизатор: </p>

<p>R15: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> network 10.77.199.15 mask 255.255.255.255 </p>
<p> redistribute ospf 15 </p>
<p> neighbor 10.77.25.1 remote-as 1001 </p>
<p> neighbor 10.77.27.2 remote-as 1001 </p>
<p> neighbor 10.77.28.1 remote-as 1001 </p>
<p> neighbor 10.77.35.2 remote-as 1001 </p>
<p> neighbor 89.186.112.106 remote-as 301 </p>
</blockquote>

<p>На остальных маршрутизаторах для этой AS укажем соседей </p>

<p>R12: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.25.2 remote-as 1001 </p>
<p> neighbor 10.77.26.2 remote-as 1001 </p>
</blockquote>

<p>R13: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.27.2 remote-as 1001 </p>
<p> neighbor 10.77.28.2 remote-as 1001 </p>
</blockquote>

<p>R19: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.33.1 remote-as 1001 </p>
</blockquote>

<p>R20: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.35.1 remote-as 1001 </p>
</blockquote>

<h3>Киторн:</h3>

<p>Создаем bgp AS101, добавим для анонсирования Loopback-интерфейс, укажем соседей - Ламас и Москва. Также добавим маршруты которые подключены напрямую. </p>

<blockquote>
<p>router bgp 101 </p>
<p> network 10.10.199.22 mask 255.255.255.255 </p>
<p> redistribute connected </p>
<p> neighbor 61.100.104.137 remote-as 301 </p>
<p> neighbor 77.58.86.53 remote-as 1001 </p>
</blockquote>

<h3>Ламас:</h3>

<p>Создаем bgp AS301, добавим для анонсирования Loopback-интерфейс, укажем всех напрямую подключенных соседей. Также добавим маршруты которые подключены напрямую. </p>

<blockquote>
<p>router bgp 301 </p>
<p> network 10.10.199.21 mask 255.255.255.255 </p>
<p> redistribute connected </p>
<p> neighbor 61.100.104.138 remote-as 101 </p>
<p> neighbor 68.146.22.162 remote-as 520 </p>
<p> neighbor 89.186.112.105 remote-as 1001 </p>
</blockquote>

<p>Получившиеся маршруты: </p>

<p>R14: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r14_sh_bgp.png>

<p>R15: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r15_sh_bgp.png>

<p>R21: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r21_sh_bgp.png>

<p>R22: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r22_sh_bgp.png>

<p>С пограничных маршрутизаторов МСК доступны Киторн и Ламас: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/ping_r14_r22.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/ping_r15_r21.png>


<h3>Триада:</h3>

<p>Создаем bgp AS520, добавим для анонсирования Loopback-интерфейс, укажем всех напрямую подключенных соседей. Также добавим маршруты ISIS. </p>


<p>R23: </p>

<blockquote>
<p>router bgp 520 </p>
<p> network 10.10.199.23 mask 255.255.255.255 </p>
<p> redistribute isis 23 level-2 </p>
<p> neighbor 13.33.47.2 remote-as 520 </p>
<p> neighbor 13.33.48.2 remote-as 520 </p>
</blockquote>

<p>R24: </p>

<blockquote>
<p>router bgp 520 </p>
<p> network 10.10.199.24 mask 255.255.255.255 </p>
<p> redistribute isis 24 level-2 </p>
<p> neighbor 13.33.47.1 remote-as 520 </p>
<p> neighbor 13.33.50.2 remote-as 520 </p>
<p> neighbor 68.146.22.161 remote-as 301 </p>
<p> neighbor 111.213.154.177 remote-as 2042 </p>
</blockquote>

<p>R25:

<blockquote>
<p>router bgp 520 </p>
<p> network 10.10.199.25 mask 255.255.255.255 </p>
<p> redistribute isis 25 level-2 </p>
<p> redistribute isis </p>
<p> neighbor 13.33.48.1 remote-as 520 </p>
<p> neighbor 13.33.51.2 remote-as 520 </p>
</blockquote>

<p>R26: </p>

<blockquote>
<p>router bgp 520 </p>
<p> network 10.10.199.26 mask 255.255.255.255 </p>
<p> redistribute isis 26 level-2 </p>
<p> neighbor 13.33.50.1 remote-as 520 </p>
<p> neighbor 13.33.51.1 remote-as 520 </p>
<p> neighbor 129.218.17.221 remote-as 2042 </p>
</blockquote>

<h3>С.-Петербург:</h3>

<p>Создаем bgp AS2042, добавим для анонсирования Loopback-интерфейс, укажем всех напрямую подключенных соседей. Также добавим маршруты EIGRP. </p>

<p>R18: </p>

<blockquote>
<p>router bgp 2042 </p>
<p> network 10.78.199.18 mask 255.255.255.255 </p>
<p> redistribute eigrp 78 </p>
<p> neighbor 10.78.34.1 remote-as 2042 </p>
<p> neighbor 10.78.35.1 remote-as 2042 </p>
<p> neighbor 111.213.154.178 remote-as 520 </p>
<p> neighbor 129.218.17.222 remote-as 520 </p>
</blockquote>

<p>R16: </p>

<blockquote>
<p>router bgp 2042 </p>
<p> neighbor 10.78.34.2 remote-as 2042 </p>
<p> neighbor 10.78.48.2 remote-as 2042 </p>
</blockquote>

<p>R17:

<blockquote>
<p>router bgp 2042 </p>
<p> neighbor 10.78.35.2 remote-as 2042 </p>
</blockquote>

<p>R32: </p>

<blockquote>
<p>router bgp 2042 </p>
<p> neighbor 10.78.48.1 remote-as 2042 </p>
</blockquote>

<p>Получившиеся маршруты: </p>

<p>R18: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r18_sh_bgp.png>

<p>Из МСК доступен пограничный маршрутизатор Санкт-Петербурга: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/ping_r14_r18.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/ping_r15_r18.png>

<p>И они даже идут по разным маршрутам: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/trace_r14_r18.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/trace_r15_r18.png>


<p>Обратно из СПБ в МСК маршрутизаторы также доступны: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r18_to_msk.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/trace_r18_r14.png>