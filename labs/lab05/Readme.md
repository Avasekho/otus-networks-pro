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

<p> ��������� �������� ������������� � ����� ��������: </p>

<p> �������� �������� ��������� ������� - ������ �� ��������� ���� ����� R25; ������ �� ������ � ��� ����� R26. </p>

<p> ������� ��� ��������������� access-����� </p>

<blockquote>
ip access-list extended acl1
 permit ip any 10.89.0.0 0.0.255.255
ip access-list extended acl2
 permit ip any 10.77.0.0 0.0.255.255
 permit ip any 10.78.0.0 0.0.255.255
</blockquote>

<p> ��������� �� ��� ���������� �������� ����������� ����� �� ���������� </p>

<blockquote>
ip sla 1
 icmp-echo 24.16.137.253 source-interface Ethernet0/0
 threshold 1000
 timeout 1500
 frequency 10
ip sla schedule 1 life forever start-time now

ip sla 2
 icmp-echo 193.116.238.157 source-interface Ethernet0/1
 threshold 1000
 timeout 1500
 frequency 10
ip sla schedule 2 life forever start-time now

track 1 ip sla 1 reachability

track 2 ip sla 2 reachability
</blockquote>

<p> � ������� ����������� �������� ������������� </p>

<blockquote>
route-map PBR_SLA permit 10
 match ip address acl1
 set ip next-hop verify-availability 193.116.238.157 1 track 1

route-map PBR_SLA permit 20
 match ip address acl2
 set ip next-hop verify-availability 24.16.137.253 2 track 2
</blockquote>

<p> ����� ��������� ������, � ����� �������������  </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/track.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/route-map.png>

<p> ��� �������� ������� ����� ��� ������ ����� �������� �� ������ �����������/����������� </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/trace_89.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab05/trace_78.png>

<p> ��������� ��� ����� ���������� ������� �� ���������: </p>

<p> ��� ��������� �������� ������� �� ��������� �� R25 � ������� �� 10.14.0.0/16 </p>

<blockquote>
ip default-gateway 146.55.30.129
ip route 10.14.0.0 255.255.0.0 Ethernet0/0
</blockquote>