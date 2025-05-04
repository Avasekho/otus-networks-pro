<h1> Лабораторная работа 11. Настройка BGP - Фильтрация </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/topology-lab11.png>

<h2> Задачи </h2>

<ol>
  <li> Настроить фильтрацию для офиса Москва </li>
  <li> Настроить фильтрацию для офиса С.-Петербург </li>

</ol>

<h2> Решение: </h2>

<h3>Настроить фильтрацию в офисе Москва так, чтобы не появилось транзитного трафика(As-path). </h3>

<p>Нам надо разрешить маршруты локальной AS и запретить остальное. Заодно уберем из анонсов bgp ранее настроенные врутренние сети МСК. </p>

<p>R14 </p>

<p>// no redistribute ospf 14 </p>
<p>// no network 10.77.0.0 mask 255.255.0.0 </p>

<blockquote>
<p>ip as-path access-list 1 permit ^1001$ </p>
<p>ip as-path access-list 1 deny .* </p>
<p></p>
<p>router bgp 1001 </p>
<p> bgp log-neighbor-changes </p>
<p> network 10.77.199.14 mask 255.255.255.255 </p>
<p> neighbor 10.77.25.2 remote-as 1001 </p>
<p> neighbor 10.77.26.1 remote-as 1001 </p>
<p> neighbor 10.77.27.1 remote-as 1001 </p>
<p> neighbor 10.77.33.2 remote-as 1001 </p>
<p> neighbor 10.77.199.15 remote-as 1001 </p>
<p> neighbor 10.77.199.15 update-source Loopback1 </p>
<p> neighbor 10.77.199.15 next-hop-self </p>
<p> neighbor 77.58.86.54 remote-as 101 </p>
<p> neighbor 77.58.86.54 filter-list 1 out </p>
</blockquote>

<p>R15 </p>

<p>// no redistribute ospf 15 </p>

<blockquote>
<p>ip as-path access-list 1 permit ^1001$ </p>
<p>ip as-path access-list 1 deny .* </p>
<p></p>
<p>router bgp 1001 </p>
<p> bgp log-neighbor-changes </p>
<p> bgp default local-preference 65535 </p>
<p> network 10.77.199.15 mask 255.255.255.255 </p>
<p> neighbor 10.10.199.21 remote-as 301 </p>
<p> neighbor 10.10.199.21 update-source Loopback1 </p>
<p> neighbor 10.77.25.1 remote-as 1001 </p>
<p> neighbor 10.77.27.2 remote-as 1001 </p>
<p> neighbor 10.77.28.1 remote-as 1001 </p>
<p> neighbor 10.77.35.2 remote-as 1001 </p>
<p> neighbor 10.77.199.14 remote-as 1001 </p>
<p> neighbor 10.77.199.14 update-source Loopback1 </p>
<p> neighbor 10.77.199.14 next-hop-self </p>
<p> neighbor 89.186.112.106 remote-as 301 </p>
<p> neighbor 89.186.112.106 filter-list 1 out </p>
</blockquote>

<p>Ламас </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/r21_bgp.png>

<p>Киторн </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/r22_bgp.png>


<h3>Настроить фильтрацию в офисе С.-Петербург так, чтобы не появилось транзитного трафика(Prefix-list). </h3>

<p>Разрешим наружу адреса с префиксом сети СПБ, остальное запретим  </p>

<p>// no redistribute eigrp 78 </p>

<blockquote>
<p>ip prefix-list SPB seq 5 permit 10.78.0.0/16 le 32 </p>
<p>ip prefix-list SPB seq 10 deny 0.0.0.0/0 </p>
<p></p>
<p>router bgp 2042 </p>
<p> bgp log-neighbor-changes </p>
<p> network 10.78.199.18 mask 255.255.255.255 </p>
<p> neighbor 10.78.34.1 remote-as 2042 </p>
<p> neighbor 10.78.35.1 remote-as 2042 </p>
<p> neighbor 111.213.154.178 remote-as 520 </p>
<p> neighbor 111.213.154.178 prefix-list SPB out </p>
<p> neighbor 129.218.17.222 remote-as 520 </p>
<p> neighbor 129.218.17.222 prefix-list SPB out </p>
<p> maximum-paths 2 </p>
</blockquote>

<p>R24 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/r24_bgp.png>

<p>R26 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/r26_bgp.png>


<h3>Настроить провайдера Киторн так, чтобы в офис Москва отдавался только маршрут по умолчанию. </h3>

<p>Разрешим 0.0.0.0/0 и запретим все остальные, добавим раздачу на соседа маршрута по умолчанию </p>

<blockquote>
<p>ip prefix-list ISP22 seq 5 permit 0.0.0.0/0 </p>
<p>ip prefix-list ISP22 seq 10 deny 0.0.0.0/0 le 32 </p>
<p></p>
<p>route-map default-r22 permit 10 </p>
<p>match ip address prefix-list ISP22 </p>
<p></p>
<p>router bgp 1001 </p>
<p>neighbor 77.58.86.53 default-originate default-r22 </p>
<p>neighbor 77.58.86.53 route-map default-r22 out </p>
</blockquote>

<h3>Настроить провайдера Ламас так, чтобы в офис Москва отдавался только маршрут по умолчанию и префикс офиса С.-Петербург. </h3>

<p>Разрешим 0.0.0.0/0 и 10.78.0.0/16, запретим все остальные, добавим раздачу на соседа маршрута по умолчанию </p>

<blockquote>
<p>ip prefix-list ISP21 seq 5 permit 0.0.0.0/0 </p>
<p>ip prefix-list ISP21 seq 10 permit 10.78.0.0/16 le 32 </p>
<p>ip prefix-list ISP21 seq 15 deny 0.0.0.0/0 le 32 </p>
<p></p>
<p>route-map default-r21 permit 10 </p>
<p>match ip address prefix-list ISP21 </p>
<p></p>
<p>router bgp 1001 </p>
<p>neighbor 89.186.112.105 default-originate default-r21 </p>
<p>neighbor 89.186.112.105 route-map default-r21 out </p>
</blockquote>

<p>R14 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/r14_bgp.png>

<p>R15 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/r15_bgp.png>

<h3>Все сети в лабораторной работе должны иметь IP связность. </h3>

<p>Провайдеры и СПб доступны из Москвы </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/r14_ping.png>

<p>Провайдеры и Москва доступны из СПб </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab11/r18_ping.png>
