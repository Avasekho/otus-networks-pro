<h1> ������������ ������ 5. ������������� �� ������ ������� (PBR) </h1> 

<h2> ��������� </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/topology-lab05.png>

<h2> ������ </h2>

<ol>
  <li> ��������� �������� ������������� � ����� ��������. </li>
  <li> ������������ ������ ����� 2 �������. </li>
  <li> ��������� ��� ����� ���������� ������� �� ���������. </li>
</ol>

<h2> �������: </h2>

<h2> ��������� �������� ������������� � ����� ��������: </h2>

<p> �������� �������� ��������� ������� - ������ �� ��������� ���� ����� R25; ������ �� ������ � ��� ����� R26. </p>

<p> ������� ��� ��������������� access-�����: </p>

<blockquote>
<p>ip access-list extended acl1</p>
<p> permit ip any 10.89.0.0 0.0.255.255</p>
<p></p>
<p>ip access-list extended acl2</p>
<p> permit ip any 10.77.0.0 0.0.255.255</p>
<p> permit ip any 10.78.0.0 0.0.255.255</p>
</blockquote>

<p> ��������� �� ��� ���������� �������� ����������� ����� �� ����������: </p>

<blockquote>
<p>ip sla 1</p>
<p> icmp-echo 24.16.137.253 source-interface Ethernet0/0</p>
<p> threshold 1000</p>
<p> timeout 1500</p>
<p> frequency 10</p>
<p>ip sla schedule 1 life forever start-time now</p>
<p></p>
<p>ip sla 2</p>
<p> icmp-echo 193.116.238.157 source-interface Ethernet0/1</p>
<p> threshold 1000</p>
<p> timeout 1500</p>
<p> frequency 10</p>
<p>ip sla schedule 2 life forever start-time now</p>
<p></p>
<p>track 1 ip sla 1 reachability</p>
<p></p>
<p>track 2 ip sla 2 reachability</p>
</blockquote>

<p> � ������� ����������� �������� ������������� </p>

<blockquote>
<p>route-map PBR_SLA permit 10</p>
<p> match ip address acl1</p>
<p> set ip next-hop verify-availability 193.116.238.157 1 track 1</p>
<p></p>
<p>route-map PBR_SLA permit 20</p>
<p> match ip address acl2</p>
<p> set ip next-hop verify-availability 24.16.137.253 2 track 2</p>
</blockquote>

<p> ����� ��������� ������, � ����� �������������  </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/track.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/route-map.png>

<p> ��� �������� ������� ����� ��� ������ ����� �������� �� ������ �����������/����������� </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/trace_89.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/trace_78.png>

<p> ��������� ��� ����� ���������� ������� �� ���������: </p>

<h2> ��� ��������� �������� ������� �� ��������� �� R25 � ������� �� 10.14.0.0/16 </h2>

<blockquote>
<p>ip default-gateway 146.55.30.129</p>
<p>ip route 10.14.0.0 255.255.0.0 Ethernet0/0</p>
</blockquote>