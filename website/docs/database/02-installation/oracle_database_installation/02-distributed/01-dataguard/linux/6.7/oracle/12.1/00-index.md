---
layout: page
title: Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/
---


<a href="http://docs.oracle.com/cd/B28359_01/server.111/b28294/rcmbackp.htm"> Creating a Standby Database with Active Database Duplication</a>




# В разработке!  

# В разработке!  

## Помогайте, кому нечем заняться!  

## Пока не работает!!!

# В разработке!  

# В разработке!  





Технология Oracle Data Guard предалагает решение для обеспечения высокой доступности, повышенной производительности и автоматического преодоления последствий сбоя.

Изменения в основной базе данных могут быть переданы в резернвые базы данных с гарантией отсутствия потерь данных в процессе передачи.


Поддерживаются 2 типа резервных баз данных - с осуществлением физического и логическог резервирования.
Физическая резервная база данных содержит те же самые структуры, что и основная. Логическая - может иметь другие внутренние структуры (например, дополнительные индексы, используемые для генерации отчетов). Синхронизация основной базы данных с резервными осуществляется путем передачи журнальных данных через SQL - операторы, выполняемые над резервной базой данных.

Физическая резервная база данных является поблочной копией первичной базы данных. Во время восстановления в аварийных ситуациях, резервная база даных в точности похожа на основную базу данных.

Логическая база данных - используется для подготовки отчетов (при подготовке отчетов требуются существенные ресурсы системы). В этом случае резервная база данных открывается только для чтения и пользователи, которым необходимо сформировать отчеты работают с ней. При этом основная база данных продолжает работать на прием данных от операторов.


<br/><br/>

У меня нет environment, где бы я постоянно работал с dataguard. Здесь я постараюсь его настроить. Буду обновлять по мере появления новых знаний.

В случае обнаружения ошибок, неточностей, опечаток или вам известны лучшие способы, пишите мне на адрес эл. почты:


<div>
	<img src="http://img.fotografii.org/a3333333mail.gif" border="0">
</div>


<br/>
<br/>

<!--

<div style="padding:10px; border:thin solid black;">

Для информации:

<br/>

db_name - должно быть одинаковое на узлах  
db_unique_name - должно быть разными на узлах  

</div>

-->

<br/>

## Подготовка виртуальных машин:


<ul>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/info-about-env/">Описание системы, которое будет настраиваться</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/prepare-env/">Предварительные шаги по настройке environment</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/prepare-instance/">Предварительные шаги по настройке параметров instance</a></li>

</ul>



<br/>


## Подготовка дупликата:

<ul>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/setup-oracle-network-services/">Настройка сетевых служб Oracle для создания standby дупликата</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/copy-passwords-file/">Копирование файла паролей с primary на standby</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/startup-instance-on-standby/">Стартую instance на standby</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/check-duplicate-env/">Проверяем, что файловая система схожа на 2-х серверах</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-connection-check/">Проверка подключения RMAN к обоим Instance</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-script-for-duplicate-instance/">Создание rman скрипта для дупликата и его выполнение</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-script-for-duplicate-instance/">Создание rman скрипта для дупликата и его выполнение</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-on-primary/">Шаги, выполняемые после создания дупликата на Primary</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-standby-redologs/">Создание standby redologs</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/check-redo-apply/">Проверка применения redo</a></li>

</ul>
