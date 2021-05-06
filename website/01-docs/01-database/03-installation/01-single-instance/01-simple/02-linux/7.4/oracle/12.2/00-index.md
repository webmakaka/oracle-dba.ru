---
layout: page
title: Инсталляция Oracle DataBase 12.2 в Oracle Linux 7.4
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, Инсталляция
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/
---

<br/>

# [Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4]

<br/>

### В последний раз инсталлирвовал по данной инструкции для тестовых задач 24.11.2017. (Необходимо поправить материал в настройках параметров ядра.)

<br/>

В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Oracle Linux.

Использовать его следует, если вы только приступаете к изучению основ администрирования баз данных Oracle. В случае необходимости использования в промышленной среде, необходимо обязательно обеспечить резервное копирование, мультиплексирование критичных для работы базы данных файлов и правильно настроить системные параметры.

В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, <a href="/chat/">пишите в чат или на адрес эл. почты</a>.

<br/>

<strong>Самые последние версии (на момент написания):</strong>

<ul>
	<li>Oracle Linux - 7.4</li>
	<li>Oracle DataBase - 12.2</li>
</ul>

<br/>

Инсталляция происходит на удаленный сервер без GUI.

Управление процессом установки и настройки происходит с рабочей станции с помощью SSH клиента. В Windows это может быть Putty в linux стандартный Terminal.

<br/>

## Дистрибутивы:

В этот раз дистрибутивы я взял с официального сайта Oracle. Это база данных и это oracle Linux.

Oracle linux можно скачать на сайте linux.oracle.com. Обращаю внимани, что кликать нужно на кнопку "Download" а не пытаться залогиниться.
Базу данных я скачал на сайте oracle.com будучи залогиненым пользователем. В новом интерфейсе сайта достаточно сложно найти что нужно.

<br/>

## Создание виртуальной машины VirtualBox для инсталляции базы данных:

<ul>
	<li><a href="/database/installation/single-instance/simple/oel/7.4/oracle/db/12.2/">Создание виртуальной машины VirtualBox для инсталляции базы данных</a><br/></li>
</ul>

<br/>

## Инсталляция Oracle Linux 7.4:

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oel-7.4-installation/">Инсталляция Oracle Linux 7.4</a><br/></li>
</ul>

<br/><br/>

## Подготовка операционной системы Linux к инсталляции базы данных Oracle:

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/network-interfaces/">Настройка сетевых интерфейсов</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/setup-os-parameters-before-we-start/">Установка параметров ОС перед стартом</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/install-mandatory-packages/">Инсталляция обязательных пакетов</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/setup-actual-time/">Настройка сервисов отвечающих за синхронизацию времени</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/prepare-hdd-to-install-oracle/">Подготовка жестких дисков к инсталляции базы данных</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/prepare-kernel-parameters-and-user-environments/">Конфигурирование системных пользователей, настройка параметров системы</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/create-folder-structure-and-user-permissions/">Создание структуры каталогов и назначение необходимых прав</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/setup-display-manager/">Настройка Display Manger</a></li>

  <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/copy-oracle-distrib-on-server/">Копирование дистрибутивов базы данных на сервер</a></li>

</ul>

<br/><br/>

## Инсталляция базы данных:

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-database-software-installation/">Инсталляция СУБД Oracle (DataBase SoftWare)</a></li>

    <li><a href="/database/installation/single-instance/linux/7.3/oracle/12.2/oracle-listener-creation/">Создание службы удаленного подключения к серверу (Listener)</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-instance-creation/">Создание экземпляра базы данных (Instance)</a></li>

</ul>

<br/><br/>

## После инсталляции:

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/autorstart-oracle-after-restart/">Настройка автозапуска Oracle после перезагрузки</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-setup-fast-recovery-area-params/">Задание параметров FAST RECOVERY AREA</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-cold-backup/">Создание резервной копии созданной базы данных (холодный backup)</a></li>

    <li>Обновление базы патчами, рекомендованными Oracle (Нет у меня сейчас доступа, чтобы скачать патчи. Демонстрировалось при инсталляции 11 версии Oracle)</li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-restrict-root-access/">Запретить удаленное подключение к серверу баз данных пользователем root</a></li>

    <li>Разрешить удаленное подключение к серверу по ssh только с определенных ip адресов, создав правила в iptables (возможное улучшение, здесь не описывается)</li>

    <li>Блокировать возможность подключения к серверу при вводе неправильного пароля более 5 раз (Fail2ban) (возможное улучшение, здесь не описывается)</li>

</ul>

<br/><br/>

## Обеспечение дополнительной отказоустойчивости и надежности:

<ul>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-controlfiles-multiplexing/">Мультиплексирование controlfiles</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-redologs-multiplexing/">Мультиплексирование redologs</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/enable-archivelog-mod/">Включить режим работы ARCHIVELOG</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-archivelogs-multiplexing/">Мультиплексирование archivelog</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-change-default-datafile-location/">Изменение расположения файлов данных</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-additionals-datafiles/">Расширение табличных пространств (создание дополнительных файлов для табличных пространств)</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/enable-flashback-mod/">Включить режим работы FLASH BACK</a></li>

    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-final-hot-backup/">Контрольный backup (горячий backup)</a></li>

</ul>

<br/><br/>

## Подключиться к базе с клиентского компьютера:

<ul>

    <li><a href="/client/installation/windows/7/oracle/12.1/">Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)</a> (C 64 битным клиентом не работают такие программы как PL/SQL Developer)</li>

</ul>

<br/><br/>

<div style="padding:10px; border:thin solid black;" align="center">

  <h3>Есди есть предложения по улучшению, пишите!</h3>

</div>
