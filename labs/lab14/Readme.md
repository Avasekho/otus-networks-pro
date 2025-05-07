<h1> Лабораторная работа 14. IPSec over DmVPN </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/topology-lab14.png>

<h2> Задачи </h2>

<ol>
  <li> Настроить GRE поверх IPSec между офисами Москва и С.-Петербург. </li>
  <li> Настроить DMVPN поверх IPSec между Москва и Чокурдах, Лабытнанги. </li>
  <li> Все узлы в офисах в лабораторной работе должны иметь IP связность. </li>

</ol>

<h2> Решение: </h2>

<h3>Настроить GRE поверх IPSec между офисами Москва и С.-Петербург </h3>

<p>R15</p>

<blockquote>
<p>crypto ikev2 proposal r15-p1</p>
<p> encryption aes-cbc-128</p>
<p> integrity md5</p>
<p> group 2</p>
<p></p>
<p>crypto ikev2 policy ikev2-plc</p>
<p> proposal r15-p1</p>
<p></p>
<p>crypto ikev2 profile r15-ikev2</p>
<p> match address local interface Ethernet0/2</p>
<p> match identity remote address 111.213.154.177 255.255.255.255</p>
<p> authentication remote pre-share key r15r18ipsec</p>
<p> authentication local pre-share key r15r18ipsec</p>
<p></p>
<p>crypto isakmp policy 5</p>
<p> hash sha256</p>
<p></p>
<p>crypto ipsec transform-set TS esp-aes esp-md5-hmac</p>
<p> mode tunnel</p>
<p></p>
<p>crypto ipsec profile r15-ipsec</p>
<p> set transform-set TS</p>
<p> set ikev2-profile r15-ikev2</p>
</blockquote>

<blockquote>
<p>interface Tunnel0</p>
<p> ip address 10.99.10.1 255.255.255.252</p>
<p> ip mtu 1400</p>
<p> ip tcp adjust-mss 1360</p>
<p> tunnel source 89.186.112.105</p>
<p> tunnel destination 111.213.154.177</p>
<p> tunnel protection ipsec profile r15-ipsec</p>
</blockquote>


<p>R18</p>

<blockquote>
<p>crypto ikev2 proposal r18-p1</p>
<p> encryption aes-cbc-128</p>
<p> integrity md5</p>
<p> group 2</p>
<p></p>
<p>crypto ikev2 policy ikev2-plc</p>
<p> proposal r18-p1</p>
<p></p>
<p>crypto ikev2 profile r18-ikev2</p>
<p> match address local interface Ethernet0/2</p>
<p> match identity remote address 89.186.112.105 255.255.255.255</p>
<p> authentication remote pre-share key r15r18ipsec</p>
<p> authentication local pre-share key r15r18ipsec</p>
<p></p>
<p>crypto isakmp policy 5</p>
<p> hash sha256</p>
<p></p>
<p>crypto ipsec transform-set TS esp-aes esp-md5-hmac</p>
<p> mode tunnel</p>
<p></p>
<p>crypto ipsec profile r18-ipsec</p>
<p> set transform-set TS</p>
<p> set ikev2-profile r18-ikev2</p>
</blockquote>

<blockquote>
<p>interface Tunnel0</p>
<p> ip address 10.99.10.2 255.255.255.252</p>
<p> ip mtu 1400</p>
<p> ip tcp adjust-mss 1360</p>
<p> tunnel source 111.213.154.177</p>
<p> tunnel destination 89.186.112.105</p>
<p> tunnel protection ipsec profile r18-ipsec</p>
</blockquote>


<p>Проверим состояние ipsec-сессии</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r15_ping.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r15_crypto_session.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r18_ping.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r18_crypto_session.png>

<p>Пинг проходит, пакеты шифруются</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r15_ipsec_sa.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r18_ipsec_sa.png>


<h3>Настроить DMVPN поверх IPSec между Москва и Чокурдах, Лабытнанги </h3>

<p>R14</p>

<blockquote>
<p>crypto ikev2 proposal r14-p1</p>
<p> encryption aes-cbc-128</p>
<p> integrity md5</p>
<p> group 2</p>
<p></p>
<p>crypto ikev2 policy ikev2-plc</p>
<p> match fvrf any</p>
<p> proposal r14-p1</p>
<p></p>
<p>crypto ikev2 keyring ikev2-key</p>
<p> peer DMVPN</p>
<p> address 0.0.0.0 0.0.0.0</p>
<p> pre-shared-key r14r28r27ipsec</p>
<p></p>
<p>crypto ikev2 profile r14-ikev2</p>
<p> match address local interface Ethernet0/2</p>
<p> match fvrf any</p>
<p> match identity remote any</p>
<p> authentication remote pre-share</p>
<p> authentication local pre-share</p>
<p> keyring local ikev2-key</p>
<p></p>
<p>crypto isakmp policy 5</p>
<p> hash sha256</p>
<p></p>
<p>crypto ipsec transform-set TS esp-aes esp-md5-hmac</p>
<p> mode tunnel</p>
<p></p>
<p>crypto ipsec profile r14-ipsec</p>
<p> set transform-set TS</p>
<p> set ikev2-profile r14-ikev2</p>
</blockquote>

<blockquote>
<p>interface Tunnel0</p>
<p> ip address 10.99.20.1 255.255.255.0</p>
<p> ip mtu 1400</p>
<p> ip nhrp map multicast dynamic</p>
<p> ip nhrp network-id 77</p>
<p> ip tcp adjust-mss 1360</p>
<p> tunnel source Ethernet0/2</p>
<p> tunnel mode gre multipoint</p>
<p> tunnel protection ipsec profile r14-ipsec</p>
</blockquote>


<p>R28</p>

<blockquote>
<p>crypto ikev2 proposal r28-p1</p>
<p> encryption aes-cbc-128</p>
<p> integrity md5</p>
<p> group 2</p>
<p></p>
<p>crypto ikev2 policy ikev2-plc</p>
<p> match fvrf any</p>
<p> proposal r28-p1</p>
<p></p>
<p>crypto ikev2 keyring ikev2-key</p>
<p> peer DMVPN</p>
<p> address 0.0.0.0 0.0.0.0</p>
<p> pre-shared-key r14r28r27ipsec</p>
<p></p>
<p>crypto ikev2 profile r28-ikev2</p>
<p> match address local interface Ethernet0/0</p>
<p> match fvrf any</p>
<p> match identity remote any</p>
<p> authentication remote pre-share</p>
<p> authentication local pre-share</p>
<p> keyring local ikev2-key</p>
<p></p>
<p>crypto isakmp policy 5</p>
<p> hash sha256</p>
<p></p>
<p>crypto ipsec transform-set TS esp-aes esp-md5-hmac</p>
<p> mode tunnel</p>
<p></p>
<p>crypto ipsec profile r28-ipsec</p>
<p> set transform-set TS</p>
<p> set ikev2-profile r28-ikev2</p>
</blockquote>

<blockquote>
<p>interface Tunnel0</p>
<p> ip address 10.99.20.2 255.255.255.0</p>
<p> ip mtu 1400</p>
<p> ip nhrp map multicast 77.58.86.53</p>
<p> ip nhrp map 10.99.20.1 77.58.86.53</p>
<p> ip nhrp network-id 77</p>
<p> ip nhrp nhs 10.99.20.1</p>
<p> ip tcp adjust-mss 1360</p>
<p> tunnel source Ethernet0/0</p>
<p> tunnel mode gre multipoint</p>
<p> tunnel protection ipsec profile r28-ipsec</p>
</blockquote>

<p>R27</p>

<blockquote>
<p>crypto ikev2 proposal r27-p1</p>
<p> encryption aes-cbc-128</p>
<p> integrity md5</p>
<p> group 2</p>
<p></p>
<p>crypto ikev2 policy ikev2-plc</p>
<p> match fvrf any</p>
<p> proposal r27-p1</p>
<p></p>
<p>crypto ikev2 keyring ikev2-key</p>
<p> peer DMVPN</p>
<p> address 0.0.0.0 0.0.0.0</p>
<p> pre-shared-key r14r28r27ipsec</p>
<p></p>
<p>crypto ikev2 profile r27-ikev2</p>
<p> match address local interface Ethernet0/0</p>
<p> match fvrf any</p>
<p> match identity remote any</p>
<p> authentication remote pre-share</p>
<p> authentication local pre-share</p>
<p> keyring local ikev2-key</p>
<p></p>
<p>crypto isakmp policy 5</p>
<p> hash sha256</p>
<p></p>
<p>crypto ipsec transform-set TS esp-aes esp-md5-hmac</p>
<p> mode tunnel</p>
<p></p>
<p>crypto ipsec profile r27-ipsec</p>
<p> set transform-set TS</p>
<p> set ikev2-profile r27-ikev2</p>
</blockquote>

<blockquote>
<p>interface Tunnel0</p>
<p> ip address 10.99.20.3 255.255.255.0</p>
<p> ip mtu 1400</p>
<p> ip nhrp map multicast 77.58.86.53</p>
<p> ip nhrp map 10.99.20.1 77.58.86.53</p>
<p> ip nhrp network-id 77</p>
<p> ip nhrp nhs 10.99.20.1</p>
<p> ip tcp adjust-mss 1360</p>
<p> tunnel source Ethernet0/0</p>
<p> tunnel mode gre multipoint</p>
<p> tunnel protection ipsec profile r27-ipsec</p>
</blockquote>

<p>Проверим состояние ipsec-сессии</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r14_ping.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r14_crypto_session.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r28_ping.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r28_crypto_session.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r27_ping.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r27_crypto_session.png>

<p>Пинг проходит, пакеты шифруются</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r14_crypto_ipsec_sa1.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r14_crypto_ipsec_sa2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r28_crypto_ipsec_sa1.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r28_crypto_ipsec_sa2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r27_crypto_ipsec_sa1.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab14/r27_crypto_ipsec_sa2.png>