<h1> ������������ ������ 3. ���������� DHCPv4 </h1> 
<h2> ��������� </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/topology.png>

<h2> ������� ��������� </h2>

| ���������� |  ���������  |   IP-�����    |  ����� �������  |  ���� �� ���������  |
|:----------:|:-----------:|:-------------:|:---------------:|:-------------------:|
| R1         | G0/0        | 10.0.0.1      | 255.255.255.252 | -                   |
|            | G0/1        | -             | -               | -                   |
|            | G0/1.100    | 192.168.1.1   | 255.255.255.192 | -                   |
|            | G0/1.200    | 192.168.1.65  | 255.255.255.224 | -                   |
|            | G0/1.1000   | -             | -               | -                   |
| R2         | G0/0        | 10.0.0.2      | 255.255.255.252 | -                   |
|            | G0/1        | 192.168.1.97  | 255.255.255.240 | -                   |
| S1         | VLAN 200    | 192.168.1.66  | 255.255.255.224 | 192.168.1.65        |
| S2         | VLAN 1      | 192.168.1.98  | 255.255.255.240 | 192.168.1.97        |
| PC-A       | NIC         | DHCP          | DHCP            | DHCP                |
| PC-B       | NIC         | DHCP          | DHCP            | DHCP                |

<h2> ������� VLAN </h2>

|  VLAN  |     ���     |   ���������   |
|:------:|:-----------:|:-------------:|
| 1      |      -      | S2: G0/3      |
| 100    | Clients     | S1: G0/2      |
| 200    | Management  | S1: VLAN 200  |
| 999    | Parking_Lot | S1: G0/0,G0/3 |
| 1000   | Native      | -             |

<h2> ������ </h2>

<ol>
  <li> 1. �������� ���� � ��������� �������� ���������� ����������. </li>
  <li> 2. ��������� � �������� ���� �������� DHCPv4 �� R1. </li>
  <li> 3. ��������� � �������� DHCP-������������ �� R2. </li>
</ol>

<h2> �������: </h2>

<p> ����� 1. ��������� ������ ��� ��������: </p>

<p> ������� A, ��������� 58 ������. ����������� ������ ���� - 64 �����. ����� ���� /26 ��� 255.255.255.192; ��� ������� - 192.168.1.1 - 192.168.1.62 </p>

<p> ������� B, ��������� 28 �����. ����������� ������ ���� - 32 �����. ����� ���� /27 ��� 255.255.255.224; ��� ������� - 192.168.1.65 - 192.168.1.94 </p>

<p> ������� C, ��������� 12 ������. ����������� ������ ���� - 16 ������. ����� ���� /28 ��� 255.255.255.240; ��� ������� - 192.168.1.97 - 192.168.1.110 </p>

<p> ����������� ������� ������������ ��������������� � ������������ � ��������. ����������� ������������� �� R1; ����������� ���� �� ��������� ��� R1 � R2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_vlans.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R2_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_ping_R2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R2_ping_R1.png>

<p> ���� � R2 �� ������ ��������� �� ��������, ��������� �������� ������ ������ �����: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R2_ping_R1_err.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_ping_R2_2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R2_ping_R1_2.png>

<p> ����������� ������� ������������ ������������ � ������������ � ��������. ������� VLAN� �� ������������, ����������� �� ��������������� ������, ��������� �������������� �����. ����������� ����� 802.1Q ����� �������������: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S1_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S1_vlans_q.png>

<blockquote>
������ ��������� S1 G0/1 ��� ������ � VLAN 1? 
</blockquote>
<p>  ��� ���� �� ���������, � ������ ���� �� ������������ �� ������ ����. ����� ��������� ��� � �������� �������������� ����� �� ������� �� ������������ � ����������� ������� show vlan brief. </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S1_vlans.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S1_trunk.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S2_interfaces.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/S2_vlans.png>

<blockquote>
����� IP-����� ��� �� � ��, ���� �� �� ��� ��������� � ���� � ������� DHCP? 
</blockquote>
<p>  G0/2 - ���� ������� ��� VLAN 100, ������ ����� �� ���� 192.168.1.2 - 192.168.1.62 </p>

<p> ����� 2. ��������� � �������� ���� �������� DHCPv4 �� R1: </p>

<p> ����������� DHCP-������ � ������������ � ��������. ��������� ���������� �� ������� � ��-�������: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_1.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_3.png>

<p> �� �������� �����, ���������� �������������� ��������: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-A_dhcp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-A_ping.png>


<p> ����� 3. ��������� � �������� DHCP-����������� �� R2. ��������� DHCP-������������ �� ��������� �� R2. </p>

<p> ����� �� ��� ����� ������ DHCP, �.�. �� ��� �������� �� ������� B � �� �� ������� � </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/dhcp_err.png>

<p> ����� �� ��� ����� ������ DHCP, �.�. ������ ��� ��� �������� �� ������� B � �� �� ������� � </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_4.png>

<p> ����� �������� ��������� �� ���� �������� ����� </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-B_dhcp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-B_dhcp_2.png>

<p> ��������� R1 ����� �������� </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/PC-B_ping.png>

<p> �� DHCP-������� ���� ������ ����� �������� ������� ��� �� </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_3.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab03-DHCPv4/R1_dhcp_3.png>
