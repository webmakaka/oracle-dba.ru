---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Windows 2008 Server
description: Инсталляция Oracle DataBase Server 12.1 в Windows 2008 Server
keywords: Oracle DataBase, Installation, Windows 2008
permalink: /database/installation/single-instance/simple/windows/2008/oracle/12.1/
---

# Инсталляция Oracle DataBase Server 12.1 в Windows 2008 Server

<br/>

В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Microsoft Windows 2008 Server.

Использовать его следует, если вы только приступаете к изучению основ администрирования баз данных Oracle. В случае необходимости использования в промышленной среде, необходимо обязательно обеспечить резервное копирование, мультиплексирование критичных для работы базы данных файлов и правильно настроить системные параметры.

В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, <a href="/chat/">пишите в чат или на адрес эл. почты</a>.

<br/><br/>

<h2>Документация:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/docs/">Официальная документация</a><br/></li>
</ul>

<br/><br/>

<h2>Дистрибутивы:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/distrib/">Дистрибутивы баз данных и дополнительное программное обеспечение</a><br/></li>
</ul>

<br/><br/>

<h2>Перед инсталляцией:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/steps-before-installaion/">Перед инсталляцией</a></li>
</ul>

<br/><br/>

<h2>Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle в Windows 2008 Server:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/virtualbox-machines/windows/2008/">Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle в Windows 2008 Server</a></li>
</ul>

<br/><br/>

<h2>Инсталляция базы данных:</h2>
<ul>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-database-software-installation/">Инсталляция СУБД Oracle (DataBase SoftWare)</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-listener-creation/">Создание службы удаленного подключения к серверу (Listener)</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-instance-creation/">Создание экземпляра базы данных (Instance)</a></li>
</ul>

<br/><br/>

<h2>После инсталляции:</h2>
<ul>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/steps-after-installation/">После инсталляции</a></li>
</ul>

<br/><br/>

<h2>Обеспечение дополнительной отказоустойчивости и надежности:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-setup-fast-recovery-area-params/">Задание параметров FAST RECOVERY AREA</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-cold-backup/"> Создание резервной копии созданной базы данных (холодный бекап)</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-multiplex-controlfiles/">Мультиплексирование controlfiles</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-multiplex-redologs/">Мультиплексирование redologs</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/enable-archivelog-mod/">Включить режим работы ARCHIVELOG</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-multiplex-archivelogs/">Мультиплексирование archivelog</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-change-default-datafile-location/">Изменение расположения файлов данных</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-additionals-datafiles/">Расширение табличных пространств (создание дополнительных файлов для табличных пространств)</a></li>
	<li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/enable-flashback-mod/">Включить режим работы FLASH BACK</a></li>

    <li><a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-final-hot-backup/">Контрольный backup (горячий backup)</a></li>

</ul>

<br/><br/>

<h2>Подключиться к базе с клиентского компьютера:</h2>

<ul>

    <li><a href="/client/installation/windows/7/oracle/12.1/">Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)</a> (C 64 битным клиентом не работают такие программы как PL/SQL Developer)</li>

</ul>
