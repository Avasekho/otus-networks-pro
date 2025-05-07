<h1> Лабораторная работа 13. VPN. GRE. DmVPN </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab13/topology-lab13.png>

<h2> Задачи </h2>

<ol>
  <li> Настроить GRE между офисами Москва и С.-Петербург. </li>
  <li> Настроить DMVMN между Москва и Чокурдах, Лабытнанги. </li>
  <li> Все узлы в офисах в лабораторной работе должны иметь IP связность </li>

</ol>

<h2> Решение: </h2>

<h3>Настроить GRE между офисами Москва и С.-Петербург </h3>

<p>R15</p>

<blockquote>
<p>interface Tunnel0</p>
<p> ip address 10.99.10.1 255.255.255.252</p>
<p> tunnel source 89.186.112.105</p>
<p> tunnel destination 111.213.154.177</p>
<p> ip mtu 1400</p>
<p> ip tcp adjust-mss 1360</p>
</blockquote>

<p>R18</p>

<blockquote>
<p>interface Tunnel0</p>
<p> ip address 10.99.10.2 255.255.255.252</p>
<p> tunnel source 111.213.154.177</p>
<p> tunnel destination 89.186.112.105</p>
<p> ip mtu 1400</p>
<p> ip tcp adjust-mss 1360</p>
</blockquote>

<p>Оба конца туннеля доступны</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab13/tunnel_ping.png>


<h3>Настроить DMVMN между Москва и Чокурдах, Лабытнанги. </h3>

<p>R14 (Hub)</p>

<blockquote>
<p>interface tunnel0</p>
<p> tunnel mode gre multipoint</p>
<p> ip address 10.99.20.1 255.255.255.0</p>
<p> tunnel source Ethernet0/2</p>
<p> ip mtu 1400</p>
<p> ip tcp adjust-mss 1360</p>
<p> ip nhrp network-id 77</p>
<p> ip nhrp authentication r14r28r27</p>
<p> ip nhrp map multicast dynamic</p>
</blockquote>

<p>R28 (Spoke)

<blockquote>
<p>interface tunnel0</p>
<p> tunnel mode gre multipoint</p>
<p> ip address 10.99.20.2 255.255.255.0</p>
<p> tunnel source Ethernet0/0</p>
<p> ip mtu 1400</p>
<p> ip tcp adjust-mss 1360</p>
<p> ip nhrp network-id 77</p>
<p> ip nhrp authentication r14r28r27</p>
<p> ip nhrp map multicast 77.58.86.53</p>
<p> ip nhrp nhs 10.99.20.1</p>
<p> ip nhrp map 10.99.20.1 77.58.86.53</p>
</blockquote>

<p>R27 (Spoke)

<blockquote>
<p>interface tunnel0</p>
<p> tunnel mode gre multipoint</p>
<p> ip address 10.99.20.3 255.255.255.0</p>
<p> tunnel source Ethernet0/0</p>
<p> ip mtu 1400</p>
<p> ip tcp adjust-mss 1360</p>
<p> ip nhrp network-id 77</p>
<p> ip nhrp authentication r14r28r27</p>
<p> ip nhrp map multicast 77.58.86.53</p>
<p> ip nhrp nhs 10.99.20.1</p>
<p> ip nhrp map 10.99.20.1 77.58.86.53</p>
</blockquote>

<p>Проверим доступность</p>

<p>R14</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab13/R14_ping.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab13/R14_dmvpn.png>

<p>R28</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab13/R28_ping.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab13/R28_dmvpn.png>

<p>R27</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab13/R27_ping.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab13/R27_dmvpn.png>