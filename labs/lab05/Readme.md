<h1> Лабораторная работа 5. Маршрутизация на основе политик (PBR) </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/topology-lab05.png>

<h2> Задачи </h2>

<ol>
  <li> Настроить политику маршрутизации в офисе Чокурдах. </li>
  <li> Распределить трафик между 2 линками. </li>
  <li> Настроить для офиса Лабытнанги маршрут по умолчанию. </li>
</ol>

<h2> Решение: </h2>

<p> Настроить политику маршрутизации в офисе Чокурдах: </p>

<p> Настроим политику следующим образом - трафик на Лабытнаги идет через R25; трафик на Москву и СПб через R26. </p>

<p> Создаем два соответствующих access-листа </p>

<blockquote>
ip access-list extended acl1
 permit ip any 10.89.0.0 0.0.255.255
ip access-list extended acl2
 permit ip any 10.77.0.0 0.0.255.255
 permit ip any 10.78.0.0 0.0.255.255
</blockquote>

<p> Добавляем на оба интерфейса проверку доступности линка до провайдера </p>

<blockquote>
ip sla 1
 icmp-echo 24.16.137.253 source-interface Ethernet0/0
 threshold 1000
 timeout 1500
 frequency 10
ip sla schedule 1 life forever start-time now

ip sla 2
 icmp-echo 193.116.238.157 source-interface Ethernet0/1
 threshold 1000
 timeout 1500
 frequency 10
ip sla schedule 2 life forever start-time now

track 1 ip sla 1 reachability

track 2 ip sla 2 reachability
</blockquote>

<p> И наконец настраиваем политику маршрутизации </p>

<blockquote>
route-map PBR_SLA permit 10
 match ip address acl1
 set ip next-hop verify-availability 193.116.238.157 1 track 1

route-map PBR_SLA permit 20
 match ip address acl2
 set ip next-hop verify-availability 24.16.137.253 2 track 2
</blockquote>

<p> Видно состояние линков, а также маршрутизация  </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/track.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/route-map.png>

<p> При проверке доступа видно что разные офисы доступны по разным интерфейсам/провайдерам </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/trace_89.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/trace_78.png>

<p> Настроить для офиса Лабытнанги маршрут по умолчанию: </p>

<p> Для Лабытнаги добавлен маршрут по умолчанию до R25 и маршрут до 10.14.0.0/16 </p>

<blockquote>
ip default-gateway 146.55.30.129
ip route 10.14.0.0 255.255.0.0 Ethernet0/0
</blockquote>