---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /database/installation/single-instance/simple/linux/6.4/oracle/12.1/
---


# [Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]


<br/>

В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Oracle Linux.


Использовать его следует, если вы только приступаете к изучению основ администрирования баз данных Oracle. В случае необходимости использования в промышленной среде, необходимо обязательно обеспечить резервное копирование, мультиплексирование критичных для работы базы данных файлов и правильно настроить системные параметры.


В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, пишите мне адрес эл. почты:


<div>
	<img src="http://img.fotografii.org/a3333333mail.gif" border="0">
</div>

<br/>

<strong>Самые последние версии (на момент написания):</strong>

<ul>
	<li>Oracle Linux - 6.4</li>
	<li>Oracle DataBase - 12.1</li>
</ul>


<br/><br/>
Инсталляция происходит на удаленный сервер без GUI.

Управление процессом установки и настройки происходит с рабочей станции под управлением Linux по SSH. Если вы будете управлять процессом установки базы данных с рабочей станции под windows, скорее всего вам понадобятся putty и xming. Именно таким образом описывалась установка <a href="/database/installation/single-instance/simple/linux/6.3/oracle/12.1/">Oracle 11.2</a>.


<br/><br/>
<h2>Документация:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/docs/">Официальная документация</a><br/></li>
</ul>



<h2>Дистрибутивы:</h2>


<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/distrib/">Дистрибутивы баз данных и дополнительное программное обеспечение</a><br/></li>
</ul>

<br/><br/>

<h2>Подготовка операционной системы Linux к инсталляции базы данных Oracle:</h2>


<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/network-interfaces/">Настройка сетевых интерфейсов</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/setup-os-parameters-before-we-start/">Установка параметров ОС перед стартом</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/install-mandatory-packages/">Инсталляция обязательных пакетов</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/setup-actual-time/">Настройка актуального времени</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/prepare-hdd-to-install-oracle/">Подготовка жестких дисков к инсталляции базы данных</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/prepare-kernel-parameters-and-user-environments/">Конфигурурование системных пользователей, настройка параметров системы</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/autostart-only-packages-what-needed/">Автозапуск только выбранных программ</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/create-folder-structure-and-user-permissions/">Создание структуры каталогов и назначение необходимых прав</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/setup-display-manager/">Настройка Display Manger</a></li>

</ul>


<br/><br/>

<h2>Инсталляция базы данных:</h2>
<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/copy-oracle-distrib-on-server/">Копирование дистрибутивов базы данных на сервер</a></li>



	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-database-software-installation/">Инсталляция СУБД Oracle (DataBase SoftWare)</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-listener-creation/">Создание службы удаленного подключения к серверу (Listener)</a></li>


	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-instance-creation/">Создание экземпляра базы данных (Instance)</a></li>
</ul>



<br/><br/>

<h2>После инсталляции:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/autorstart-oracle-after-restart/">Настройка автозапуска Oracle после перезагрузки</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-setup-fast-recovery-area-params/">Задание параметров FAST RECOVERY AREA</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-cold-backup/">Создание резервной копии созданной базы данных (холодный backup)</a></li>


	<li>Обновление базы патчами, рекомендованными Oracle (Демонстрировалось в предыдущей версии документа)</li>


	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-restrict-root-access/">Запретить удаленное подключение к сереверу баз данных пользователем root</a></li>

	<li>Разрешить удаленное подключение к серверу по ssh только с определенных ip адресов, создав правила в iptables</li>

	<li>Блокировать возможность подключения к серверу при вводе неправильного пароля более 5 раз (Fail2ban)</li>
</ul>


<br/><br/>

<h2>Обеспечение дополнительной отказоустойчивости и надежности:</h2>
<ul>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-multiplex-controlfiles/">Мультиплексирование controlfiles</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-multiplex-redologs/">Мультиплексирование redologs</a></li>


	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/enable-archivelog-mod/">Включить режим работы ARCHIVELOG</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-multiplex-archivelogs/">Мультиплексирование archivelog</a></li>


	<li><a href="oracle-change-default-datafile-location">Изменение расположения файлов данных</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-additionals-datafiles/">Расширение табличных пространств (создание дополнительных файлов для табличных пространств)</a></li>


	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/enable-flashback-mod/">Включить режим работы FLASH BACK</a></li>

	<li><a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-final-hot-backup/">Контрольный backup (горячий backup)</a></li>
</ul>





<br/><br/>
Если вы захотите подключиться к базе данных с помощью программы <strong>SQL Developer, PL/SQL Developer, TOAD, SQL Navigator</strong> и другие,
возможно вам поможет вот <a href="http://odba.ru/showthread.php?t=294">этот материал</a>.
