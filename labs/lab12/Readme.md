<h1> ������������ ������ 12. �������� ��������� ���� �������� </h1> 

<h2> ��������� </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/topology-lab12.png>

<h2> ������ </h2>

<ol>
  <li> ��������� DHCP � ����� ������ </li>
  <li> ��������� ������������� ������� � ����� ������ </li>
  <li> ��������� NAT � ����� ������, C.-��������� � �������� </li>

</ol>

<h2> �������: </h2>

<h3>��������� NAT(PAT) �� R14 � R15. ���������� ������ �������������� � ����� ���������� ������� AS1001. </h3>

<p>������� ����� ������� 10.77.200.0/24 � AS1001, ��� ������� ����� ��������������� ��������� ������.</p>

<p>R14</p>

<blockquote>
<p>interface Ethernet0/0</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet0/1</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet0/2</p>
<p> ip nat outside</p>
<p></p>
<p>interface Ethernet0/3</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet1/0</p>
<p> ip nat inside</p>
<p></p>
<p>router bgp 1001</p>
<p> network 10.77.200.0 mask 255.255.255.0</p>
<p></p>
<p></p>
<p>ip access-list extended R14-NAT</p>
<p> permit ip 10.77.0.0 0.0.255.255 any</p>
<p> deny   ip any any</p>
<p></p>
<p>ip nat pool R14-SPB 10.77.200.14 10.77.200.14 netmask 255.255.255.0</p>
<p></p>
<p>ip nat inside source list R14-NAT pool R14-SPB overload</p>
</blockquote>

<p>R15</p>

<blockquote>
<p>interface Ethernet0/0</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet0/1</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet0/2</p>
<p> ip nat outside</p>
<p></p>
<p>interface Ethernet0/3</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet1/0</p>
<p> ip nat inside</p>
<p></p>
<p>router bgp 1001</p>
<p> network 10.77.200.0 mask 255.255.255.0</p>
<p></p>
<p>ip access-list extended R15-NAT</p>
<p> permit ip 10.77.0.0 0.0.255.255 any</p>
<p> deny   ip any any</p>
<p></p>
<p>ip nat pool R15-SPB 10.77.200.15 10.77.200.15 netmask 255.255.255.0</p>
<p></p>
<p>ip nat inside source list R15-NAT pool R15-SPB overload</p>
</blockquote>

<p>�������� ������ ����������</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r14_pat.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r15_pat.png>


<h3>��������� NAT(PAT) �� R18. ���������� ������ �������������� � ��� �� 5 ������� ���������� ������� AS2042. </h3>

<p>������� ��� ������� - 10.78.200.0/29 ���������� ������� AS2042. ������� �� � ������ BGP.</p>

<p>R18</p>

<blockquote>
<p>interface Ethernet0/0</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet0/1</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet0/2</p>
<p> ip nat outside</p>
<p></p>
<p>interface Ethernet0/3</p>
<p> ip nat outside</p>
<p></p>
<p>ip access-list extended R18-NAT</p>
<p> permit ip 10.78.0.0 0.0.255.255 any</p>
<p> deny   ip any any</p>
<p></p>
<p>route-map ISP2 permit 10</p>
<p> match ip address R18-NAT</p>
<p> match interface Ethernet0/3</p>
<p></p>
<p>route-map ISP1 permit 10</p>
<p> match ip address R18-NAT</p>
<p> match interface Ethernet0/2</p>
<p></p>
<p>ip nat pool R18-SPB 10.78.200.1 10.78.200.6 255.255.255.248</p>
<p></p>
<p>ip nat inside source route-map ISP1 interface Ethernet0/2 pool R18-SPB</p>
<p>ip nat inside source route-map ISP2 interface Ethernet0/3 pool R18-SPB</p>
</blockquote>

<p>����� ����, ������ ��������, ������ ��� ���������� �������������.</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r18_nat1.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r18_nat2.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r18_ping.png>

<h3>��������� ����������� NAT ��� R20. </h3>

<p>R14</p>

<blockquote>
<p>ip nat inside source static 10.77.199.20 10.77.200.20 </p>
</blockquote>

<p>R15</p>

<blockquote>
<p>ip nat inside source static 10.77.199.20 10.77.200.20 </p>
</blockquote>

<p>���� ����, ������ �����������</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/ping_r18_r20.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r20_nat1.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r20_nat2.png>

<h3>��������� NAT ���, ����� R19 ��� �������� � ������ ���� ��� ���������� ����������. </h3>

<p>R14</p>

<blockquote>
<p>ip nat inside source static tcp 10.77.199.19 22 10.77.200.19 22 extendable</p>
</blockquote>

<p>R15</p>

<blockquote>
<p>ip nat inside source static tcp 10.77.199.19 22 10.77.200.19 22 extendable</p>
</blockquote>

<p>�������� ��� ���������� ��������. ����������� ������ � ssh ��� ����� ���, ��� ���������� Win10 � telnet �� 22 ����. ����� ������ �� �������� �� 22 ����.</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r29_to_r19_ssh.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r19_nat3.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r19_nat4.png>


<h3>��������� ����������� NAT(PAT) ��� ����� ��������. </h3>

<p>R28</p>

<blockquote>
<p>interface Ethernet0/0</p>
<p> ip address 24.16.137.254 255.255.255.252</p>
<p> ip nat outside</p>
<p> </p>
<p>interface Ethernet0/1</p>
<p> ip address 193.116.238.158 255.255.255.252</p>
<p> ip nat outside</p>
<p></p>
<p>interface Ethernet0/2.130</p>
<p> encapsulation dot1Q 130</p>
<p> ip address 10.14.130.1 255.255.255.0</p>
<p> ip nat inside</p>
<p></p>
<p>interface Ethernet0/2.131</p>
<p> encapsulation dot1Q 131</p>
<p> ip address 10.14.131.1 255.255.255.0</p>
<p> ip nat inside</p>
<p></p>
<p>ip access-list extended R28-NAT</p>
<p> permit ip 10.14.0.0 0.0.255.255 any</p>
<p> deny   ip any any</p>
<p></p>
<p>route-map ISP2 permit 10</p>
<p> match ip address R28-NAT</p>
<p> match interface Ethernet0/1</p>
<p></p>
<p>route-map ISP1 permit 10</p>
<p> match ip address R28-NAT</p>
<p> match interface Ethernet0/0</p>
<p></p>
<p>ip nat inside source route-map ISP1 interface Ethernet0/0 overload</p>
<p>ip nat inside source route-map ISP2 interface Ethernet0/1 overload</p>
</blockquote>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r28_nat.png>

<h3>��������� ��� IPv4 DHCP ������ � ����� ������ �� ��������������� R12 � R13. VPC1 � VPC7 ������ �������� ������� ��������� �� DHCP. </h3>

<p>R12</p>

<blockquote>
<p>ip dhcp excluded-address 10.77.101.1 10.77.101.99</p>
<p>ip dhcp pool VPC1_LAN</p>
<p>network 10.77.101.0 255.255.255.0</p>
<p>default-router 10.77.101.1</p>
<p>lease 2 12 30</p>
</blockquote>

<p>R13</p>

<blockquote>
<p>ip dhcp excluded-address 10.77.107.1 10.77.107.99</p>
<p>ip dhcp pool VPC7_LAN</p>
<p>network 10.77.107.0 255.255.255.0</p>
<p>default-router 10.77.107.1</p>
<p>lease 2 12 30</p>
</blockquote>

<p>VPC1</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/vpc1_dhcp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r12_dhcp.png>

<p>VPC7</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/vpc7_dhcp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r13_dhcp.png>

<h3>��������� NTP ������ �� R12 � R13. ��� ���������� � ����� ������ ������ ���������������� ����� � R12 � R13. </h3>

<p>�������� NTP-������ �� R12 � R13 � �������� ��������� ��������� �� �������� �������������� � � VLAN99 (��� ������������)</p>

<p>R12</p>

<blockquote>
<p>clock timezone msk 3</p>
<p>ntp master 4</p>
<p>ntp source Loopback1</p>
<p>ntp update-calendar</p>
<p></p>
<p>interface Ethernet0/2</p>
<p> ntp broadcast</p>
<p></p>
<p>interface Ethernet0/3</p>
<p> ntp broadcast</p>
<p></p>
<p>interface BVI99</p>
<p> ntp broadcast</p>
</blockquote>

<p>R13</p>

<blockquote>
<p>clock timezone msk 3</p>
<p>ntp master 4</p>
<p>ntp source Loopback1</p>
<p>ntp update-calendar</p>
<p></p>
<p>interface Ethernet0/2</p>
<p> ntp broadcast</p>
<p></p>
<p>interface Ethernet0/3</p>
<p> ntp broadcast</p>
<p></p>
<p>interface BVI99</p>
<p> ntp broadcast</p>
</blockquote>

<p>R14</p>

<blockquote>
<p>interface Ethernet0/0</p>
<p>ntp broadcast client</p>
<p></p>
<p>interface Ethernet0/1</p>
<p>ntp broadcast client</p>
<p></p>
<p></p>
<p>ntp server 10.77.199.12</p>
<p>ntp server 10.77.199.13</p>
</blockquote>

<p>R15</p>

<blockquote>
<p>interface Ethernet0/0</p>
<p>ntp broadcast client</p>
<p></p>
<p>interface Ethernet0/1</p>
<p>ntp broadcast client</p>
<p></p>
<p></p>
<p>ntp server 10.77.199.12</p>
<p>ntp server 10.77.199.13</p>
</blockquote>

<p>R19</p>

<blockquote>
<p>interface Ethernet0/0</p>
<p>ntp broadcast client</p>
<p></p>
<p>ntp server 10.77.199.12</p>
<p>ntp server 10.77.199.13</p>
</blockquote>

<p>R20</p>

<blockquote>
<p>interface Ethernet0/0</p>
<p>ntp broadcast client</p>
<p></p>
<p>ntp server 10.77.199.12</p>
<p>ntp server 10.77.199.13</p>
</blockquote>

<p>SW2-SW5</p>

<blockquote>
<p>interface Vlan 99</p>
<p>ntp broadcast client</p>
</blockquote>

<p>���������� �������� ���������</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/SW4_ntp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r15_ntp.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/R20_ntp.png>

<h3>��� ����� � ������������ ������ ������ ����� IP ���������. </h3>

<p>�������� ����������� �� ��� ���� ��������� ������</p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab12/r14_ping.png>
    