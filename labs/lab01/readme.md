<h1> ������������ ������ 1.  </h1> 

<h2> ��������� </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/topology.png>

<h2> ������� ��������� </h2>

| ���������� |  ���������  |   IP-�����    |  ����� �������  | ���� �� ��������� |
|:----------:|:-----------:|:-------------:|:---------------:|:-----------------:|
| R1         | G0/0.3      | 192.168.3.1  | 255.255.255.0   |         -          |
|            | G0/0.4      | 192.168.4.1  | 255.255.255.0   |         -          |
|            | G0/0.8      |      -       |        -        |         -          |
| S1         | VLAN 3      | 192.168.3.11 | 255.255.255.0   | 192.168.3.1        |
| S2         | VLAN 3      | 192.168.3.12 | 255.255.255.0   | 192.168.3.1        |
| PC-A       | NIC         | 192.168.3.3  | 255.255.255.0   | 192.168.3.1        |
| PC-B       | NIC         | 192.168.4.3  | 255.255.255.0   | 192.168.4.1        |

<h2> ������� VLAN </h2>

|   VLAN   |     ���      |     ����������� ���������     |
|:--------:|:------------:|:-----------------------------:|
| 3        | Management   | S1: VLAN 3                    |
|          |              | S2: VLAN 3                    |
|          |              | S1: G0/2                      |
| 4        | Operations   | S2: G0/2                      |
| 7        | ParkingLot   | S1: G0/3                      |
|          |              | S2: G0/0, G0/3                |
| 8        | Native       |               -               |

<h2> ������ </h2>

<ol>
  <li> �������� ���� � ��������� �������� ���������� ����������. </li>
  <li> �������� ����� VLAN � ���������� ������ �����������. </li>
  <li> ��������� ������ 802.1Q ����� �������������. </li>
  <li> ��������� ������������� ����� ������ VLAN. </li>
  <li> �������� ������ ������������� ����� ������ VLAN. </li>
</ol>

<h2> �������: </h2>

<p> ����������� ������� ������������ � ������������ � ��������. ������� VLAN� �� ������������, ����������� �� ��������������� ������, ��������� �������������� �����. ����������� ����� 802.1Q ����� �������������: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/r1_interfaces.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/r1_vlans.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/s1_interfaces.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/s1_vlans.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/s2_interfaces.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/s2_vlans.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-a_ip.png>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-b_ip.png>

<p> ��������� ������������� ����� ������: </p>

<p> ���� �� PC-A �� ����� �� ���������: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-a_to_gateway.png>

<p> ���� �� PC-A �� PC-B: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-a_to_pc-b.png>

<p> ���� �� PC-A �� S2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/pc-a_to_s2.png>

<p> ����������� �� PC-B �� PC-A: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab01/trace_pc-b_to_pc-a.png>