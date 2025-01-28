<h1> Лабораторная работа 2. Развертывание коммутируемой сети с резервными каналами </h1> 

<h2> Топология </h2>
<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/topology.png>

<h2> Таблица адресации </h2>

| Устройство |  Интерфейс  |   IP-адрес    |  Маска подсети  |
|:----------:|:-----------:|:-------------:|:---------------:|
| S1         | VLAN 1      | 192.168.1.1   | 255.255.255.0   |
| S2         | VLAN 1      | 192.168.1.2   | 255.255.255.0   |
| S3         | VLAN 1      | 192.168.1.3   | 255.255.255.0   |

<h2> Задачи </h2>

<ol>
  <li> Создание сети и настройка основных параметров устройства. </li>
  <li> Выбор корневого моста. </li>
  <li> Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов. </li>
  <li> Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов. </li>
</ol>

<h2> Решение: </h2>

<p> Настраиваем базовую конфигурацию в соответствии с заданием. Создаем VLANы на коммутаторах,спользуемые порты: </p>

<p> Проверяем связь между маршрутизаторами: </p>

<p> Эхо-запрос от коммутатора S1 на коммутатор S2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/s1_to_s2_ping.png>

<p> Эхо-запрос от коммутатора S1 на коммутатор S3: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/s1_to_s3_ping.png>

<p> Эхо-запрос от коммутатора S2 на коммутатор S3: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/s2_to_s3_ping.png>


<p> Определение корневого моста: </p>

<p> Настраиваем порты в качестве транковых. Включаем в нашем случае порты G0/1 и G0/3. </p>

<p> Результат spanning tree: </p>

<p> S1: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S1_stp.png>

<p> S2: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp.png>

<p> S3: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp.png>


<p> Схема: </p>

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/schema.png>

<blockquote>
Какой коммутатор является корневым мостом?
</blockquote>
S1


<blockquote>
Почему этот коммутатор был выбран протоколом spanning-tree в качестве корневого моста?
</blockquote>
Приоритет у всех трех коммутаторов одинаковый, следовательно выбирается по меньшему значению MAC-адреса


<blockquote>
Какие порты на коммутаторе являются корневыми портами?
</blockquote>
G0/3 (F0/3 на схеме) на S2 и G0/1 (F0/1 на схеме) на S3


<blockquote>
Какие порты на коммутаторе являются назначенными портами?
</blockquote>
G0/1 и G0/3 (F0/1 и F0/3 на схеме) на S1 и G0/1 (F0/1 на схеме) на S3


<blockquote>
Какой порт отображается в качестве альтернативного и в настоящее время заблокирован?
</blockquote>
G0/3 (F0/3 на схеме) на S2


<blockquote>
Почему протокол spanning-tree выбрал этот порт в качестве невыделенного (заблокированного) порта?
</blockquote>
Стоимость пути от корневого моста до этого порта выше чем до другого порта на том же устройстве.


<h2> Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов </h2>


Определим коммутатор с заблокированным портом:

S2:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp_2.png>

S3:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp_2.png>

Коммутатор с заблокированным портом - S3




Изменим стоимость порта для корневого порта на S3. Т.е. стоимость по умолчанию задана 4, уменьшим стоимость до трех:

S2:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp_3.png>

S3:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp_3.png>

Теперь заблокированный порт назначен на порт G0/1 коммутатора S2


<blockquote>
Почему протокол spanning-tree заменяет ранее заблокированный порт на назначенный порт и блокирует порт, который был назначенным портом на другом коммутаторе?
</blockquote>
Если ранее на основании сравнения идентификаторов BID при идентичном значении приоритета портов из-за MAC-адреса топология выглядела как S3 -> S2 -> S1;
то теперь исходя из приоритета корневого порта стоимость порта G0/1 на коммутаторе S3 изменилась и он стал более приоритетным относительно порта G0/1 на коммутаторе S2.
Новая топология представляет собой S3 -> S1 -> S2.


Удалим изменения стоимости порта - порты вернулись в исходное состояние

S2:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp_4.png>

S3:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp_4.png>


<h2> Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов </h2>

Включим все подключенные порты на коммутаторах:

S1:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S1_stp_2.png>

S2:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S2_stp_5.png>

S3:

<img src=https://github.com/Avasekho/otus-networks-pro/blob/main/labs/lab02/S3_stp_5.png>


<blockquote>
Какой порт выбран протоколом STP в качестве порта корневого моста на каждом коммутаторе некорневого моста?
</blockquote>
<p>S2 - G0/2</p>
<p>S3 - G0/0</p>


<blockquote>
Почему протокол STP выбрал эти порты в качестве портов корневого моста на этих коммутаторах
</blockquote>
<p>Порты получили наименьшее значение по сравнению значений в следующем порядке:</p>
<p>Root Bridge ID -> Цена (Cost) -> Sender Bridge ID -> Sender Port ID -> Reciever Port ID</p>

<p> На примере порта S2 - G0/2: </p>
<p> - S1 (Root Bridge) отправляет пакеты с S1 - G0/2 на S2 - G0/2 и с S1 - G0/3 на S2 - G0/3. </p>
<p> - Root Bridge ID - идентичен </p>
<p> - Цена (Cost) идентичны (1гбит == 4) </p>
<p> - Sender Bridge ID - идентичен </p>
<p> - Sender Port ID - отличаются; G0/2 на S2 меньше G0/3 на S2 и соответственно корневым портом на S1 выбран G0/2 </p>


<blockquote>
1.	Какое значение протокол STP использует первым после выбора корневого моста, чтобы определить выбор порта?
</blockquote>
Цена (Cost)


<blockquote>
2.	Если первое значение на двух портах одинаково, какое следующее значение будет использовать протокол STP при выборе порта?
</blockquote>
Sender Bridge ID


<blockquote>
3.	Если оба значения на двух портах равны, каким будет следующее значение, которое использует протокол STP при выборе порта?
</blockquote>
Sender Port ID, если и он идентичен, то Reciever Port ID который уже должен быть уникальным