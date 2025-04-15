<h1> ������������ ������ 6. OSPF </h1> 

<h2> ��������� </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/topology-lab06.png>

<h2> ������ </h2>

<ol>
  <li> ��������� OSPF ����� ������. </li>
  <li> ��������� ���� �� ����. </li>
  <li> ��������� ���������� ����� ������. </li>
</ol>

<h2> �������: </h2>

<h2> ��������� OSPF ����� ������. </h2>

<h3> �������������� R14-R15 ��������� � ���� 0 - backbone. </h3>

<p>��� ���������� ������ backbone-area �������� ���� ����� ���������������� R14 � R15, ������ ��������� � ������������ 4. </p>

| ���������� |  ���������  |    IPv4-�����      |       �����������        |
|:----------:|:-----------:|:------------------:|:------------------------:|
| R14        | E1/0        | 10.77.29.1/30      | R14 to R15               |
| R15        | E1/0        | 10.77.29.2/30      | R15 to R14               |

<p>������� �� �������������� ������������ �� ����� � �������� ������� �� ��������� ��� ���������� �������� ��� �� ospf </p>

<p>R14 </p>

<blockquote>
<p>router ospf 14 </p>
<p> passive-interface e0/2 // �.� ������� � ��������, ����� �� ���� ���� ������ hello </p>
<p> network 10.77.26.0 0.0.0.3 area 10 </p>
<p> network 10.77.27.0 0.0.0.3 area 10 </p>
<p> network 10.77.29.0 0.0.0.3 area 0 </p>
<p> network 10.77.33.0 0.0.0.3 area 101 </p>
<p> network 10.77.199.14 0.0.0.0 area 0 </p>
<p> default-information originate </p>
<p> </p>
<p>ip route 0.0.0.0 0.0.0.0 Ethernet0/2 </p>
</blockquote>

<p>R15 </p>

<blockquote>
<p>router ospf 15 </p>
<p> passive-interface e0/2 // �.� ������� � ��������, ����� �� ���� ���� ������ hello </p>
<p> network 10.77.25.0 0.0.0.3 area 10 </p>
<p> network 10.77.28.0 0.0.0.3 area 10 </p>
<p> network 10.77.29.0 0.0.0.3 area 0 </p>
<p> network 10.77.35.0 0.0.0.3 area 102 </p>
<p> network 10.77.199.15 0.0.0.0 area 0 </p>
<p> default-information originate </p>
<p> </p>
<p>ip route 0.0.0.0 0.0.0.0 Ethernet0/2 </p>
</blockquote>

<p>������������ �������� ospf: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab06/r14_ospf_routes>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab06/r15_ospf_routes>

<h3> �������������� R12-R13 ��������� � ���� 10. ������������� � ��������� ������ �������� ������� �� ���������. </h3>

<p>R12 </p>

<blockquote>
<p>router ospf 12 </p>
<p> network 10.77.25.0 0.0.0.3 area 10 </p>
<p> network 10.77.26.0 0.0.0.3 area 10 </p>
<p> network 10.77.199.12 0.0.0.0 area 10 </p>
</blockquote>

<p>R13 </p>

<blockquote>
<p>router ospf 13 </p>
<p> network 10.77.27.0 0.0.0.3 area 10 </p>
<p> network 10.77.28.0 0.0.0.3 area 10 </p>
<p> network 10.77.199.13 0.0.0.0 area 10 </p>
</blockquote>

<p>������������ �������� ospf: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab06/r12_ospf_routes.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab06/r13_ospf_routes.png>

<h3> ������������� R19 ��������� � ���� 101 � �������� ������ ������� �� ���������. </h3>

<p>R19 </p>

<blockquote>
<p>router ospf 19 </p>
<p> network 10.77.33.0 0.0.0.3 area 101 </p>
<p> network 10.77.199.19 0.0.0.0 area 101 </p>
</blockquote>

<p>� ��������� ��������� � ���� 101 �� �������������� R14 ��������� ������: </p>

<blockquote>
<p>ip prefix-list filter-101 seq 5 deny 10.77.25.0/30 </p>
<p>ip prefix-list filter-101 seq 10 deny 10.77.26.0/30 </p>
<p>ip prefix-list filter-101 seq 15 deny 10.77.27.0/30 </p>
<p>ip prefix-list filter-101 seq 20 deny 10.77.28.0/30 </p>
<p>ip prefix-list filter-101 seq 25 deny 10.77.29.0/30 </p>
<p>ip prefix-list filter-101 seq 30 deny 10.77.35.0/30 </p>
<p>ip prefix-list filter-101 seq 35 deny 10.77.199.12/32 </p>
<p>ip prefix-list filter-101 seq 40 deny 10.77.199.13/32 </p>
<p>ip prefix-list filter-101 seq 45 deny 10.77.199.14/32 </p>
<p>ip prefix-list filter-101 seq 50 deny 10.77.199.15/32 </p>
<p>ip prefix-list filter-101 seq 55 deny 10.77.199.20/32 </p>
<p>ip prefix-list filter-101 seq 60 permit 0.0.0.0/0 le 32 </p>
<p> </p>
<p>router ospf 14 </p>
<p> area 101 filter-list prefix filter-101 in </p>
</blockquote>

<p>������������ �������� ospf: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab06/r19_ospf_routes.png>

<h3> ������������� R20 ��������� � ���� 102 � �������� ��� ��������, ����� ��������� �� ����� ���� 101. </h3>

<p>R20 </p>

<blockquote>
<p>router ospf 20 </p>
<p> network 10.77.35.0 0.0.0.3 area 102 </p>
<p> network 10.77.199.20 0.0.0.0 area 102 </p>
</blockquote>

<p>� ��������� ��������� � ���� 102 �� �������������� R15 ��������� ������: </p>

<blockquote>
<p>ip prefix-list filter-102 seq 5 deny 10.77.33.0/30 </p>
<p>ip prefix-list filter-102 seq 10 deny 10.77.199.19/32 </p>
<p>ip prefix-list filter-102 seq 15 permit 0.0.0.0/0 le 32 </p>
<p> </p>
<p>router ospf 15 </p>
<p> area 102 filter-list prefix filter-102 in </p>
</blockquote>

<p>������������ �������� ospf: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab06/r20_ospf_routes.png>

<h3> ��������� ��� IPv6 ��������� ������ IPv4. </h3>

<p>// IPv6 � ����� �� ������������ </p>
