<h1> Лабораторная работа 7. Настройка IS-IS </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab07/topology-lab07.png>

<h2> Задачи </h2>

<ol>
  <li> Настроить IS-IS офисе Триада. </li>
</ol>

<h2> Решение: </h2>

<p>Добавим настройки isis router и укажем им соответствующие идентификаторы сети, на основании Area ID из задания и адреса Loopback интерфейса маршрутизатора. </p>
<p>Чтобы маршрутизаторы нормально общались между зонами сразу укажем им level-2. </p>

<h3> R23 и R25 находятся в зоне 2222. </h3>

<p>R23 </p>

<blockquote>
<p>router isis 23 </p>
<p> net 49.2222.1007.7019.9023.00 </p>
<p> is-type level-2-only </p>
</blockquote>

<p>и привяжем IS-IS к интерфейсам внутри провайдера Триада: </p>

<blockquote>
<p>interface Ethernet0/1 </p>
<p> ip address 13.33.48.1 255.255.255.252 </p>
<p> ip router isis 23 </p>
<p>! </p>
<p>interface Ethernet0/2 </p>
<p> ip address 13.33.47.1 255.255.255.252 </p>
<p> ip router isis 23 </p>
</blockquote>

<p>И про Loopback интерфейс не забудем: </p>

<blockquote>
<p>interface Loopback1 </p>
<p> ip address 10.77.199.23 255.255.255.255 </p>
<p> ip router isis 23 </p>
</blockquote>

<p>R25 </p>

<blockquote>
<p>router isis 25 </p>
<p> net 49.2222.1007.7019.9025.00 </p>
<p> is-type level-2-only </p>
<p> </p>
<p>interface Ethernet0/0 </p>
<p> ip address 13.33.48.2 255.255.255.252 </p>
<p> ip router isis 25 </p>
<p>! </p>
<p>interface Ethernet0/2 </p>
<p> ip address 13.33.51.1 255.255.255.252 </p>
<p> ip router isis 25 </p>
<p> </p>
<p>interface Loopback1 </p>
<p> ip address 10.77.199.25 255.255.255.255 </p>
<p> ip router isis 25 </p>
</blockquote>

<h3> R24 находится в зоне 24. </h3>

<p>R24 </p>

<blockquote>
<p>router isis 24 </p>
<p> net 49.0024.1007.7019.9024.00 </p>
<p> is-type level-2-only </p>
<p> </p>
<p>interface Ethernet0/1 </p>
<p> ip address 13.33.50.1 255.255.255.252 </p>
<p> ip router isis 24 </p>
<p>! </p>
<p>interface Ethernet0/2 </p>
<p> ip address 13.33.47.2 255.255.255.252 </p>
<p> ip router isis 24 </p>
<p> </p>
<p>interface Loopback1 </p>
<p> ip address 10.77.199.24 255.255.255.255 </p>
<p> ip router isis 24 </p>
</blockquote>

<h3> R26 находится в зоне 26. </h3>

<p>R26 </p>

<blockquote>
<p>router isis 26 </p>
<p> net 49.0026.1007.7019.9026.00 </p>
<p> is-type level-2-only </p>
<p> </p>
<p>interface Ethernet0/0 </p>
<p> ip address 13.33.50.2 255.255.255.252 </p>
<p> ip router isis 26 </p>
<p>! </p>
<p>interface Ethernet0/2 </p>
<p> ip address 13.33.51.2 255.255.255.252 </p>
<p> ip router isis 26 </p>
<p> </p>
<p>interface Loopback1 </p>
<p> ip address 10.77.199.26 255.255.255.255 </p>
<p> ip router isis 26 </p>
</blockquote>

<p>В результате маршрутизаторы видят друг друга по соседству </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab07/r23_isis.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab07/r24_isis.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab07/r25_isis.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab07/r26_isis.png>

<p>А также доступен пинг до не соединенных напрямую маршрутизаторов, при не заданных маршрутах по умолчанию </p>

<p>R23-R26 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab07/ping_r23_r26.png>

<p>R24-R25 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab07/ping_r24_r25.png>

<p>// IPv6 в схеме не используется </p>
