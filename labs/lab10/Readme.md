<h1> Лабораторная работа 10. Настройка iBGP </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/topology-lab10.png>

<h2> Задачи </h2>

<ol>
  <li> Настроить iBGP в офисе Москва </li>
  <li> Настроить iBGP в сети провайдера Триада </li>
  <li> Организовать полную IP связанность всех сетей </li>

</ol>

<h2> Решение: </h2>

<h3>Настроить iBGP в офисом Москва между маршрутизаторами R14 и R15. </h3>

<p>Добавляем на R14 и R15 указатели друг на друга </p>

<p>R14 </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.199.15 remote-as 1001 </p>
<p> neighbor 10.77.199.15 update-source Loopback1 </p>
<p> neighbor 10.77.199.15 next-hop-self </p>
</blockquote>

<p>R15 </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.199.14 remote-as 1001 </p>
<p> neighbor 10.77.199.14 update-source Loopback1 </p>
<p> neighbor 10.77.199.14 next-hop-self </p>
</blockquote>

<p>В списке маршрутов появились iBGP записи </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r14_ibgp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r15_ibgp.png>


<h3>Настроить iBGP в провайдере Триада, с использованием RR. </h3>

<p>Настроим в Триада соседей и клиентов Route-reflector </p>

<p>R23 </p>

<blockquote>
<p>router bgp 520 </p>
<p> neighbor 10.10.199.24 remote-as 520 </p>
<p> neighbor 10.10.199.24 update-source Loopback1 </p>
<p> neighbor 10.10.199.24 route-reflector-client </p>
<p> neighbor 10.10.199.25 remote-as 520 </p>
<p> neighbor 10.10.199.25 update-source Loopback1 </p>
<p> neighbor 10.10.199.26 remote-as 520 </p>
<p> neighbor 10.10.199.26 update-source Loopback1 </p>
<p> neighbor 10.10.199.26 route-reflector-client </p>
</blockquote>

<p>R24 </p>

<blockquote>
<p>router bgp 520 </p>
<p> neighbor 10.10.199.23 remote-as 520 </p>
<p> neighbor 10.10.199.23 update-source Loopback1 </p>
<p> neighbor 10.10.199.25 remote-as 520 </p>
<p> neighbor 10.10.199.25 update-source Loopback1 </p>
</blockquote>

<p>R25 </p>

<blockquote>
<p>router bgp 520 </p>
<p> neighbor 10.10.199.23 remote-as 520 </p>
<p> neighbor 10.10.199.23 update-source Loopback1 </p>
<p> neighbor 10.10.199.24 remote-as 520 </p>
<p> neighbor 10.10.199.24 update-source Loopback1 </p>
<p> neighbor 10.10.199.24 route-reflector-client </p>
<p> neighbor 10.10.199.26 remote-as 520 </p>
<p> neighbor 10.10.199.26 update-source Loopback1 </p>
<p> neighbor 10.10.199.26 route-reflector-client </p>
</blockquote>

<p>R26 </p>

<blockquote>
<p>router bgp 520 </p>
<p> neighbor 10.10.199.23 remote-as 520 </p>
<p> neighbor 10.10.199.23 update-source Loopback1 </p>
<p> neighbor 10.10.199.25 remote-as 520 </p>
<p> neighbor 10.10.199.25 update-source Loopback1 </p>
</blockquote>
 
<p>Route-reflector получает маршруты от клиентов </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r23_rr.png>


<h3>Настройть офис Москва так, чтобы приоритетным провайдером стал Ламас. </h3>

<p>Т.к. других маршрутов пока не планируется, поставим на R15 local-preference по умолчанию </p>

<p>R15 </p>

<blockquote>
<p>router bgp 1001 </p>
<p>bgp default local-preference 65535 </p>
</blockquote>

<p>Маршруты на R14 идут на R15 (10.77.199.15) и Ламас </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r14_ip_routes_.png>


<h3>Настройть офис С.-Петербург так, чтобы трафик до любого офиса распределялся по двум линкам одновременно. </h3>

<p>Добавим multipath в настройки BGP </p>

<p>R18 </p>

<blockquote>
<p>router bgp 2042 </p>
<p>maximum-paths 2 </p>
</blockquote>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r18_multipath.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r18_trace.png>

<h3>Все сети в лабораторной работе должны иметь IP связность. </h3>

<p>Москва - Санкт-Петербург </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r14_to_r18.png>

<p>Москва - Киторн </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r14_to_r21.png>

<p>Москва - Ламас </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r14_to_r22.png>

<p>Москва - Триада </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r14_to_r26.png>

<p>Санкт-Петербург - Москва </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r18_to_r14.png>

<p>Санкт-Петербург - Киторн </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r18_to_r21.png>

<p>Санкт-Петербург - Ламас </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r18_to_r22.png>

<p>Санкт-Петербург - Триада </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab10/r18_to_r26.png>


