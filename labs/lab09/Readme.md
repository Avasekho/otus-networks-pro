<h1> ������������ ������ 9. ��������� BGP </h1> 

<h2> ��������� </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/topology-lab09.png>

<h2> ������ </h2>

<ol>
  <li> ��������� eBGP ����� ������ ������ � ����� ������������ - ������ � �����. </li>
  <li> ��������� eBGP ����� ������������ ������ � �����. </li>
  <li> ��������� eBGP ����� ����� � ������. </li>
  <li> ��������� eBGP ����� ������ �.-��������� � ����������� ������. </li>
  <li> ������������ IP ����������� ����� ����������� ��������� ������� ������ � �.-���������. </li>
</ol>

<h2> �������: </h2>

<p>// ����� �������� ��������� ���������� ��� ��������� ������� 10.77.0.0/16 (���� ���) � Loopback ��������, ������ ��������������� ����������� �������� � 10.78.199.� �� 10.10.199.�; ��������� �������� � ������� � ������������ 4. </p>

<h3>������ � ����� ������:</h3>

<p>R14: </p>

<p>������� bgp AS1001, ������� ��� ������������� Loopback-���������, ������ ���� �������� ������������ �������. ����� ������� �������� ������� ��������� �� ospf. </p>

<blockquote>
<p>router bgp 1001 </p>
<p> network 10.77.199.14 mask 255.255.255.255 </p>
<p> redistribute ospf 14 </p>
<p> neighbor 10.77.25.2 remote-as 1001 </p>
<p> neighbor 10.77.26.1 remote-as 1001 </p>
<p> neighbor 10.77.27.1 remote-as 1001 </p>
<p> neighbor 10.77.33.2 remote-as 1001 </p>
<p> neighbor 77.58.86.54 remote-as 101 </p>
</blockquote>

<p>���������� ������ ����������� �������������: </p>

<p>R15: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> network 10.77.199.15 mask 255.255.255.255 </p>
<p> redistribute ospf 15 </p>
<p> neighbor 10.77.25.1 remote-as 1001 </p>
<p> neighbor 10.77.27.2 remote-as 1001 </p>
<p> neighbor 10.77.28.1 remote-as 1001 </p>
<p> neighbor 10.77.35.2 remote-as 1001 </p>
<p> neighbor 89.186.112.106 remote-as 301 </p>
</blockquote>

<p>�� ��������� ��������������� ��� ���� AS ������ ������� </p>

<p>R12: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.25.2 remote-as 1001 </p>
<p> neighbor 10.77.26.2 remote-as 1001 </p>
</blockquote>

<p>R13: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.27.2 remote-as 1001 </p>
<p> neighbor 10.77.28.2 remote-as 1001 </p>
</blockquote>

<p>R19: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.33.1 remote-as 1001 </p>
</blockquote>

<p>R20: </p>

<blockquote>
<p>router bgp 1001 </p>
<p> neighbor 10.77.35.1 remote-as 1001 </p>
</blockquote>

<h3>������:</h3>

<p>������� bgp AS101, ������� ��� ������������� Loopback-���������, ������ ������� - ����� � ������. ����� ������� �������� ������� ���������� ��������. </p>

<blockquote>
<p>router bgp 101 </p>
<p> network 10.10.199.22 mask 255.255.255.255 </p>
<p> redistribute connected </p>
<p> neighbor 61.100.104.137 remote-as 301 </p>
<p> neighbor 77.58.86.53 remote-as 1001 </p>
</blockquote>

<h3>�����:</h3>

<p>������� bgp AS301, ������� ��� ������������� Loopback-���������, ������ ���� �������� ������������ �������. ����� ������� �������� ������� ���������� ��������. </p>

<blockquote>
<p>router bgp 301 </p>
<p> network 10.10.199.21 mask 255.255.255.255 </p>
<p> redistribute connected </p>
<p> neighbor 61.100.104.138 remote-as 101 </p>
<p> neighbor 68.146.22.162 remote-as 520 </p>
<p> neighbor 89.186.112.105 remote-as 1001 </p>
</blockquote>

<p>������������ ��������: </p>

<p>R14: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r14_sh_bgp.png>

<p>R15: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r15_sh_bgp.png>

<p>R21: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r21_sh_bgp.png>

<p>R22: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r22_sh_bgp.png>

<p>� ����������� ��������������� ��� �������� ������ � �����: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/ping_r14_r22.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/ping_r15_r21.png>


<h3>������:</h3>

<p>������� bgp AS520, ������� ��� ������������� Loopback-���������, ������ ���� �������� ������������ �������. ����� ������� �������� ISIS. </p>


<p>R23: </p>

<blockquote>
<p>router bgp 520 </p>
<p> network 10.10.199.23 mask 255.255.255.255 </p>
<p> redistribute isis 23 level-2 </p>
<p> neighbor 13.33.47.2 remote-as 520 </p>
<p> neighbor 13.33.48.2 remote-as 520 </p>
</blockquote>

<p>R24: </p>

<blockquote>
<p>router bgp 520 </p>
<p> network 10.10.199.24 mask 255.255.255.255 </p>
<p> redistribute isis 24 level-2 </p>
<p> neighbor 13.33.47.1 remote-as 520 </p>
<p> neighbor 13.33.50.2 remote-as 520 </p>
<p> neighbor 68.146.22.161 remote-as 301 </p>
<p> neighbor 111.213.154.177 remote-as 2042 </p>
</blockquote>

<p>R25:

<blockquote>
<p>router bgp 520 </p>
<p> network 10.10.199.25 mask 255.255.255.255 </p>
<p> redistribute isis 25 level-2 </p>
<p> redistribute isis </p>
<p> neighbor 13.33.48.1 remote-as 520 </p>
<p> neighbor 13.33.51.2 remote-as 520 </p>
</blockquote>

<p>R26: </p>

<blockquote>
<p>router bgp 520 </p>
<p> network 10.10.199.26 mask 255.255.255.255 </p>
<p> redistribute isis 26 level-2 </p>
<p> neighbor 13.33.50.1 remote-as 520 </p>
<p> neighbor 13.33.51.1 remote-as 520 </p>
<p> neighbor 129.218.17.221 remote-as 2042 </p>
</blockquote>

<h3>�.-���������:</h3>

<p>������� bgp AS2042, ������� ��� ������������� Loopback-���������, ������ ���� �������� ������������ �������. ����� ������� �������� EIGRP. </p>

<p>R18: </p>

<blockquote>
<p>router bgp 2042 </p>
<p> network 10.78.199.18 mask 255.255.255.255 </p>
<p> redistribute eigrp 78 </p>
<p> neighbor 10.78.34.1 remote-as 2042 </p>
<p> neighbor 10.78.35.1 remote-as 2042 </p>
<p> neighbor 111.213.154.178 remote-as 520 </p>
<p> neighbor 129.218.17.222 remote-as 520 </p>
</blockquote>

<p>R16: </p>

<blockquote>
<p>router bgp 2042 </p>
<p> neighbor 10.78.34.2 remote-as 2042 </p>
<p> neighbor 10.78.48.2 remote-as 2042 </p>
</blockquote>

<p>R17:

<blockquote>
<p>router bgp 2042 </p>
<p> neighbor 10.78.35.2 remote-as 2042 </p>
</blockquote>

<p>R32: </p>

<blockquote>
<p>router bgp 2042 </p>
<p> neighbor 10.78.48.1 remote-as 2042 </p>
</blockquote>

<p>������������ ��������: </p>

<p>R18: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r18_sh_bgp.png>

<p>�� ��� �������� ����������� ������������� �����-����������: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/ping_r14_r18.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/ping_r15_r18.png>

<p>� ��� ���� ���� �� ������ ���������: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/trace_r14_r18.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/trace_r15_r18.png>


<p>������� �� ��� � ��� �������������� ����� ��������: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/r18_to_msk.png>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab09/trace_r18_r14.png>