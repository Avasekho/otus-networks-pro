<h1> ������������ ������ 3. ���������� DHCPv6 </h1> 
<h2> ��������� </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/topology.png>

<h2> ������� ��������� </h2>

| ���������� |  ���������  |       IPv6-�����        |
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

<h2> ������ </h2>

<ol>
  <li> 1. �������� ���� � ��������� �������� ���������� ����������. </li>
  <li> 2. �������� ���������� ������ SLAAC �� R1. </li>
  <li> 3. ��������� � �������� ������� Stateless DHCPv6 �� R1. </li>
  <li> 4. ��������� � �������� Stateful DHCPv6 ������� �� R1. </li>
  <li> 5. ��������� � �������� DHCPv6 Relay �� R2. </li>
</ol>


<h2> �������: </h2>

<p> ����� 1. C������� ���� � ��������� �������� ���������� ����������: </p>

<p> ����������� ������� ������������ ��������������� � ������������ � ��������. ����������� ������ �� R1 � R2; ����������� ���� �� ��������� ��� R1 � R2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/R1_ipv6_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/R2_ipv6_interfaces.png>

<p> ��������� ����������� � R1 ���������� G0/1 �� R2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/R1_ping_1.png>

<p> ����� 2. �������� ���������� ������ SLAAC �� R1: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-A_ipv6_1.png>

<blockquote>
������ ������� host-id ����� ������? 
</blockquote>
<p> ������������ �� ������ MAC-������ ����������. </p>

<p> ����� 3. ��������� � �������� ������� Stateless DHCPv6 �� R1: </p>

<p> ������ ��������� IPv6 �� PC-A: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-A_ipv6_2.png>

<p> ����������� Stateless DHCPv6 �� R1 � ������������ � ��������. ��������� ����������� ��������� IPv6 �� PC-A: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-A_ipv6_3.png>

<p> ��������� ���� �� ���������� G0/1 R2 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-A_ping_1.png>

<p> ����� 4. ��������� � �������� Stateful DHCPv6 ������� �� R1: </p>

<p> ����������� Stateful DHCPv6 �� R1 � ������������ � ��������. </p>

<p> ����� 5. ��������� � �������� DHCPv6 Relay �� R2: </p>

<p> ������ ��������� IPv6 �� PC-B: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-B_ipv6_1.png>

<p> ����������� DHCPv6 Relay �� R2 � ������������ � ��������. ��������� ����������� ��������� IPv6 �� PC-B: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-B_ipv6_2.png>

<p> ��������� ���� �� ���������� G0/1 R1 </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv6/PC-B_ping_1.png>