---
layout: page
title: Инсталляция Oracle DataBase
permalink: /database/installation/
---

# Инсталляция Oracle DataBase


## Для информации:


<br/>

Если нет задачи поставить Oracle на какую-то конкретную операционную систему и задача, в первую очередь, сводится к изучению Oracle,  рекомендую ставить базу на Oracle Linux. Oracle взяла исходники RedHat и собрала свой дистрибутив. В публичном репозитории Oracle Linux имеются пакеты, которые могут сильно упростить инсталляцию базы и дополнительные пакеты, расширяющие стандартные возможности. В дополнении ко всему вышесказанному, вы можете использовать допиленное ядро UEK, которое вроде как в некоторых случаях имеет некоторые преимущесва перед стандартным. Но здесь нужно проводить тесты конкретного приложения. Ссылки на дистрибутив Oracle Lunux в теме для инсталляции.


По поводу Centos 7.X и возможных версий Oracle Linux 7.X. <br/>
Я пока на эту ветку смотреть не собираюсь. Подождем появления версии 7.2, не ранее.

<br/><br/>

## Подготовка к инсталляции базы данных Oracle:

<br/>

(Использовать, если в самом документе отстуствует информация о том как это делается)

<ul>
	<li><a href="http://sysadm.ru/linux/virtual/virtualbox/installation/centos/6/">Инсталляция VirtualBox на Centos 6.4 Server без графического интерфейса (GUI)</a></li>
	<li><a href="http://sysadm.ru/linux/virtual/virtualbox/installation/ubuntu/14.04/">Инсталляция VirtualBox в операционной системе Ubuntu в консоли</a></li>

	<li><a href="/database/installation/virtualbox-mashines/windows/2008/">Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle под Windows</a></li>

	<li><a href="/database/installation/virtualbox-mashines/oracle-linux/">Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle под Linux</a></li>

	<li><a href="/database/installation/oracle-linux-installation/6.x/">Инсталляция Oracle Linux 6.7 x86 64 bit</a></li>

	<li><a href="https://docs.google.com/document/d/1awpSIKnu2akCwEh7fbe4bY_W9G3VIr1t5Ps4hg2q2gs/edit">Инсталляция Oracle Linux 5.8 x86 64 bit</a></li>
</ul>


<br/><br/>

# Single-Instance Architecture


<br/>

## Инсталляция базы данных Oracle в операционной системе Microsoft Windows:


<br/>

<ul>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/"><strong>Инсталляция Oracle Database 12c Release 1 в операционной системе Microsoft Windows 2008 Server</strong></a> (может где и напутал вначале)</li>

	<li><a href="http://odba.ru/showthread.php?t=294"><strong>Инсталляция Oracle Database 11g Release 2 в операционной системе Microsoft Windows 2003 Server</strong></a></li>

	<li><a href="http://odba.ru/showthread.php?t=297"><strong>Инсталляция Oracle Database 10g Release 2 в операционной системе Microsoft Windows 2003 Server</strong></a> </li>
</ul>


<br/>

## Инсталляция базы данных Oracle в операционной системе Oracle Linux:

<br/>

<ul>
	<li><a href="http://odba.ru/showthread.php?t=331"><strong>Команды редактора VI</strong></a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/"><strong>Инсталляция Oracle DataBase Server (12.1.0.1) в операционной системе Oracle Linux 6.7</strong></a></li>

	<!--
	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/"><strong>Инсталляция Oracle DataBase Server (12.1.0.1) в операционной системе Oracle Linux (6.4 x86_64)</strong></a> (Server Linux -- рабочая станция Linux) (Предыдущий документ!)</li>

	-->

	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/"><strong>Инсталляция Oracle DataBase Server (11.2.0.3) в операционной системе Oracle Linux (6.3 x86_64)</strong></a> (Server Linux -- рабочая станция Windows)</li>
</li>
</ul>



<br/>
<br/>

<strong>Дополнительно инсталляция с использованием ASM:</strong>
<br/><br/>

<ul>

<li><a href="http://odba.ru/showthread.php?t=60">Информация о ASM (Automatic Storage Management) </a></li>

<li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/">Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID</a></li>

</ul>


ASM - более "правильный" способ подготовки окружения Oracle.
Суть в том, что для хранения данных используется не файловая система (например, ext*), заточенная
для обычных операций в операционной системе, а файловая система разработанная специалистами из Oracle для хранения данных.


"Сырые" (RAW) жесткие диски без файловой системы объединяются в пулы специальными средствами Oracle, что позволяет их логически организовывать и иметь какие-то преимущества по сравнению с файловой системой операционной системы.


При этом создается дополнительный экземпляр Oracle, инсталлируется GRID,
появляются еще какие-то дополнительные возможности. Администрирование несколько усложняется.


Лично мне, не приходилось плотно работать с окружением, где бы использовался ASM
(поэтому может чего и не знаю), но приходилось устанавливать  (установил, отдал и забыл)
и настраивать ASM в окружении для RAC.


Если я понял что-то неправильно, поправьте.

<br/>

## Инсталляция Oracle Client:


Oracle Client нужен, чтобы подключиться к базе с помощью большого количества программ для работы с базами данных, например таких как PL/SQL Developer, SQL Navigator, TOAD.

Программой SQL Developer от Oracle можно подключиться без установки Oracle Client.

<ul>
	<li><a href="/client/installation/windows/7/oracle/12.1/">Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)</a> (C 64 битным клиентом не работают такие программы как PL/SQL Developer)</li>

	<li><a href="https://docs.google.com/document/d/1VTV0bBZff-lyXmRTXE67tuZjXcHAlWTrq4g_c2mfoJI/edit">Инсталляция Oracle Client 11G R2 32 bit в операционной системе Windows XP 32 bit</a></li>

	<li><a href="/database/installation/oracle-client-installation/linux/6.3/oracle/11.2/">Инсталляция Oracle Instantclient в OEL 6.3 x86-64</a></li>
</ul>


<br/>
Instantclient - альтернатива стандартному Oracle Client. Проще в установке на Linux (если нужно поставить client на Ubuntu, то лучше исользовать его). А так это минимальный набор библиотек для удаленного подключения к серверу баз данных. В дополнение, я обычно устанавливаю утилиту командной строки SQLPlus. И все, больше ничего для нормальной работы и не требуется.


<br/>

## Инсталляция базы данных Oracle в других операционных системах:


<ul>
	<li><a href="http://odba.ru/showthread.php?t=303"><strong>Инсталляция Oracle Database 11g Release 2 в Oracle Solaris 10</strong></a> (Необходимо переделать!)</li>
</ul>



<br/>

## Инсталляция бесплатных версий баз данных Oracle:

<ul>
	<li><a href="http://odba.ru/showthread.php?t=742"><strong>Инструкция по инсталляции базы данных Oracle 11g XE на сервер Oracle Enterprise Linux 5.8</strong></a></li>
	<li><a href="http://odba.ru/showthread.php?t=400"><strong>Инструкция по инсталляции базы данных Oracle 10g XE на сервер Oracle Enterprise Linux 4.8</strong></a></li>
	<li><a href="http://odba.ru/showthread.php?t=296"><strong>Инсталляция Oracle Database 10g Express Edition в ОС Windows 2003 Server </strong></a></li>

</ul>


<br/>

# Distributed System Architectures:

<br/>

### DataGuard (Standby)


<ul>

	<li><a href="/database/installation/distributed/dataguard/linux/6.7/oracle/12.1/">Oracle Active Data Guard (Beta версия докумена)</a></li>

	<li><a href="http://odba.ru/showthread.php?t=469">Oracle Data Guard: Развертывание физического Standby средствами Oracle Database</a></li>

</ul>


<br/>

### Real Application Cluster (RAC)

<ul>

	<li><a href="/database/installation/distributed/rac/">Инсталляция Real Application Cluster (RAC)</a></li>

</ul>

<br/>
<br/>

## Streams, GoldenGate


У Oracle было решение по репликации данных между базами данных под названием Streams. Большая корпорация купила конкурента этой технологии, одного из лидеров по этому классу задач - Golden Gate. Со Streams не работал, Golden Gate настраивать приходилось.


<ul>
<li><a href="http://odba.ru/forumdisplay.php?f=116">GoldenGate</a></li>
<li>[HabraHabr] <a href="http://habrahabr.ru/post/238521/" rel="nofollow">Настройка двухсторонней синхронизации БД Oracle (Oracle Streams)</a></li>
</ul>
