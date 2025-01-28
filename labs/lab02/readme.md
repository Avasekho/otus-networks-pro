<h1> ������������ ������ 2. ������������� ������������� ���� � ���������� �������� </h1> 

<h2> ��������� </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/topology.png>

<h2> ������� ��������� </h2>

| ���������� |  ���������  |   IP-�����    |  ����� �������  |
|:----------:|:-----------:|:-------------:|:---------------:|
| S1         | VLAN 1      | 192.168.1.1   | 255.255.255.0   |
| S2         | VLAN 1      | 192.168.1.2   | 255.255.255.0   |
| S3         | VLAN 1      | 192.168.1.3   | 255.255.255.0   |

<h2> ������ </h2>

<ol>
  <li> �������� ���� � ��������� �������� ���������� ����������. </li>
  <li> ����� ��������� �����. </li>
  <li> ���������� �� ��������� ������ ���������� STP �����, ������ �� ��������� ������. </li>
  <li> ���������� �� ��������� ������ ���������� STP �����, ������ �� ���������� ������. </li>
</ol>

<h2> �������: </h2>

<p> ����������� ������� ������������ � ������������ � ��������. ������� VLAN� �� ������������,����������� �����: </p>

<p> ��������� ����� ����� ����������������: </p>

<p> ���-������ �� ����������� S1 �� ���������� S2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/s1_to_s2_ping.png>

<p> ���-������ �� ����������� S1 �� ���������� S3: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/s1_to_s3_ping.png>

<p> ���-������ �� ����������� S2 �� ���������� S3: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/s2_to_s3_ping.png>


<p> ����������� ��������� �����: </p>

<p> ����������� ����� � �������� ���������. �������� � ����� ������ ����� G0/1 � G0/3. </p>

<p> ��������� spanning tree: </p>

<p> S1: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S1_stp.png>

<p> S2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp.png>

<p> S3: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp.png>


<p> �����: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/schema.png>

<blockquote>
����� ���������� �������� �������� ������?
</blockquote>
S1


<blockquote>
������ ���� ���������� ��� ������ ���������� spanning-tree � �������� ��������� �����?
</blockquote>
��������� � ���� ���� ������������ ����������, ������������� ���������� �� �������� �������� MAC-������


<blockquote>
����� ����� �� ����������� �������� ��������� �������?
</blockquote>
G0/3 (F0/3 �� �����) �� S2 � G0/1 (F0/1 �� �����) �� S3


<blockquote>
����� ����� �� ����������� �������� ������������ �������?
</blockquote>
G0/1 � G0/3 (F0/1 � F0/3 �� �����) �� S1 � G0/1 (F0/1 �� �����) �� S3


<blockquote>
����� ���� ������������ � �������� ��������������� � � ��������� ����� ������������?
</blockquote>
G0/3 (F0/3 �� �����) �� S2


<blockquote>
������ �������� spanning-tree ������ ���� ���� � �������� ������������� (����������������) �����?
</blockquote>
��������� ���� �� ��������� ����� �� ����� ����� ���� ��� �� ������� ����� �� ��� �� ����������.


<h2> ���������� �� ��������� ������ ���������� STP �����, ������ �� ��������� ������ </h2>


��������� ���������� � ��������������� ������:

S2:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp_2.png>

S3:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp_2.png>

���������� � ��������������� ������ - S3




������� ��������� ����� ��� ��������� ����� �� S3. �.�. ��������� �� ��������� ������ 4, �������� ��������� �� ����:

S2:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp_3.png>

S3:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp_3.png>

������ ��������������� ���� �������� �� ���� G0/1 ����������� S2


<blockquote>
������ �������� spanning-tree �������� ����� ��������������� ���� �� ����������� ���� � ��������� ����, ������� ��� ����������� ������ �� ������ �����������?
</blockquote>
���� ����� �� ��������� ��������� ��������������� BID ��� ���������� �������� ���������� ������ ��-�� MAC-������ ��������� ��������� ��� S3 -> S2 -> S1;
�� ������ ������ �� ���������� ��������� ����� ��������� ����� G0/1 �� ����������� S3 ���������� � �� ���� ����� ������������ ������������ ����� G0/1 �� ����������� S2.
����� ��������� ������������ ����� S3 -> S1 -> S2.


������ ��������� ��������� ����� - ����� ��������� � �������� ���������

S2:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp_4.png>

S3:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp_4.png>


<h2> ���������� �� ��������� ������ ���������� STP �����, ������ �� ���������� ������ </h2>

������� ��� ������������ ����� �� ������������:

S1:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S1_stp_2.png>

S2:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp_5.png>

S3:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp_5.png>


<blockquote>
����� ���� ������ ���������� STP � �������� ����� ��������� ����� �� ������ ����������� ����������� �����?
</blockquote>
<p>S2 - G0/2</p>
<p>S3 - G0/0</p>


<blockquote>
������ �������� STP ������ ��� ����� � �������� ������ ��������� ����� �� ���� ������������
</blockquote>
<p>����� �������� ���������� �������� �� ��������� �������� � ��������� �������:</p>
<p>Root Bridge ID -> ���� (Cost) -> Sender Bridge ID -> Sender Port ID -> Reciever Port ID</p>

<p> �� ������� ����� S2 - G0/2: </p>
<p> - S1 (Root Bridge) ���������� ������ � S1 - G0/2 �� S2 - G0/2 � � S1 - G0/3 �� S2 - G0/3. </p>
<p> - Root Bridge ID - ��������� </p>
<p> - ���� (Cost) ��������� (1���� == 4) </p>
<p> - Sender Bridge ID - ��������� </p>
<p> - Sender Port ID - ����������; G0/2 �� S2 ������ G0/3 �� S2 � �������������� �������� ������ �� S1 ������ G0/2 </p>


<blockquote>
1.	����� �������� �������� STP ���������� ������ ����� ������ ��������� �����, ����� ���������� ����� �����?
</blockquote>
���� (Cost)


<blockquote>
2.	���� ������ �������� �� ���� ������ ���������, ����� ��������� �������� ����� ������������ �������� STP ��� ������ �����?
</blockquote>
Sender Bridge ID


<blockquote>
3.	���� ��� �������� �� ���� ������ �����, ����� ����� ��������� ��������, ������� ���������� �������� STP ��� ������ �����?
</blockquote>
Sender Port ID, ���� � �� ���������, �� Reciever Port ID ������� ��� ������ ���� ����������