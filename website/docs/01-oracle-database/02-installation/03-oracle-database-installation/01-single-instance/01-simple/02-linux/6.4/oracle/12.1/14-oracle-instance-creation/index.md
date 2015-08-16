---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /oracle-database-installation/linux/6.4/oracle/12.1/oracle-instance-creation/
---

# <a href="/oracle-database-installation/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Создание экземпляра базы данных (Instance)



Выполните команду:

	$ dbca


<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_01.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_02.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_03.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_04.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>

<pre>

Oracle предлагает создать экземпляр базы данных на основе одного из подготовленных шаблонов.

1. Система обработки транзакций (OLTP) - когда необходимо оптимизировать ввод данных в базу данных. Преимущественно операции по добавлению и изменению данных.
2. База данных общего назначения (custom database) - вам предлагается самостоятельно выбрать системные параметры базы данных. (самый оптимальный вариант).
3. Хранилище данных (warehouse) - когда необходимо оптимизировать работу с данными в базе данных. Преимущество операции чтения данных и подстроения аналитических отчетов.

При необходимости, данные параметры можно будет изменить в pfile или spfile.

</pre>

<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_05.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_06.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_07.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_08.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_09.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_10.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>

<pre>

Предлагается выбрать дополнительные компоненты. Если не предполагается их использовать, то скорее всего их и не следует устанавливать.

Oracle Text  - обеспечивает индексирование слов и поиск
http://docs.oracle.com/cd/B10501_01/text.920/a96517/cdefault.htm

Oracle OLAP - многомерный анализ данных, для аналитических приложений.
http://www.oracle.com/technetwork/documentation/olap-101824.html

Oracle Spatial -  для Geographic Information System (GIS) (Наверное, что-то вроде карт google maps)
http://docs.oracle.com/html/A88805_01/sdo_intr.htm

Oracle Multimedia - нужна в случае, если предполагается хранить в базе картинки, аудио, видео.
http://docs.oracle.com/cd/E11882_01/appdev.112/e10777/ch_intr.htm#i610845

Oracle JVM - нужна если нужно вызывать программы (процедуры, функции и т.д.), написанные на java непосредственно внутри базы данных.

Application Express -  приложение, с помощью которого можно достаточно просто с помощью "вайзардов" создавать приложения, работающие с базой данных. Имеет смысл оставить, только если предполагается с ним работать.

</pre>

<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_11.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_12.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>

<pre>

Если не планируется на сервере создавать еще один экземпляр базы данных, имеет смысл выделить для сервера побольше памяти.  (> 90%).

Вы также можете самостоятельно задать системные параметры создаваемой базы данных.
</pre>

<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_13.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_14.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>

<pre>
Если в базе будут использоваться русские буквы, рекомендуется выбрать кодировку, которая поддерживает данную возможность. Unicode, где каждый символ кодируется 2 байтами, вполне подходит для этой задачи.

</pre>
<br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_15.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>

<ul>
	<li>Dedicated Server Mode - для каждого соединения создается отдельный сервис. </li>
	<li>Shared Server Mode - создается пул соединений, и все клиенты подключаются к базе данных через этот пул. Имеет смысл использовать только в случае нехватки ресурсов сервера на создание выделенных сервисов.</li>
</ul>

<br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_16.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_17.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_18.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_19.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>


На этом шаге прогресс установки как бы останавливается и ничего не происходит какое-то время.
<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_20.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>




<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_21.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_22.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>

Под Firefox у меня Enterprise Manager не запустился. Правда он у меня перегружен всякими плагинами, блокирующими и активные компоненты сайтов.
<br/><br/>


<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_23.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_24.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_25.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/instance/oracle12R1_database_instance_creation_26.png" border="0" alt="Oracle 12 relese 1 Instance Creation"><br/><br/>


	$ sqlplus / as sysdba


<br/><br/>


	SQL*Plus: Release 12.1.0.1.0 Production on Sun Aug 18 17:43:29 2013

	Copyright (c) 1982, 2013, Oracle.  All rights reserved.


	Connected to:
	Oracle Database 12c Enterprise Edition Release 12.1.0.1.0 - 64bit Production
	With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options
