---
layout: page
title: Инсталляция Oracle RAC 12.1 в операционной системе Oracle Linux 6.7 (SHARED FILE SYSTEM)
description: Инсталляция Oracle RAC 12.1 в операционной системе Oracle Linux 6.7 (SHARED FILE SYSTEM)
keywords: Oracle DataBase 12.1, Oracle Linux 6.7, RAC, SHARED FILE SYSTEM
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/
---

# Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM в операционной системе Oracle Linux 6.7

<br/>

В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Oracle Linux в конфигурации Real Application Cluster (RAC).

В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, пишите мне адрес эл. почты:

<div>
	<img src="/img/a3333333mail.gif" alt="Marley" border="0">
</div>

<br/><br/>

## Документация:

<ul>
	<li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/docs/">Официальная документация</a></li>
</ul>

<br/><br/>

## Описание окружения для инсталляции Oracle RAC:

<ul>
	<li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/environment-description/">Описание окружения для инсталляции Oracle RAC</a></li>
</ul>

<br/><br/>

<h2>Дистрибутивы:</h2>

<ul>
	<li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/distrib/">Дистрибутивы баз данных и дополнительное программное обеспечение</a></li>
</ul>

<br/>

### Конфиги виртуальных машин virtualbox:

<ul>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/vm/">Конфиги виртуальных машин virtualbox</a></li>

</ul>

<br/>

### Подготовка окружения для инсталляции RAC:

<ul>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/network-interfaces/">Настройка сетевых интерфейсов и файл hosts</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/setup-os-parameters-before-begin/">Предварительные настройки</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/setup-dns-server/">Настройка DNS сервера</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/install-mandatory-packages/">Инсталляция обязательных пакетов</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/autostart-only-packages-what-needed/">Выбор пакетов для автозапуска</a> (Необязательный шаг, можно пропустить)</li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/setup-actual-time/">Настройка сервисов отвечающих за синхронизацию времени</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/users-and-groups-creation/">Создание пользователя oracle12 и административных групп</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/secure-shell-between-nodes/">Настройка Secure Shell между узлами кластера</a></li>


    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/prepare-storage/">Подготовка сервера storage (RAID, NFS)</a></li>


    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/prepare-hdd-to-install-oracle/">Подготовка локальных дисков на узлах кластера для инсталляции на них Oracle Database Software</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/mount-raid-on-nodes/">Монтирование RAID на узлах кластера</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/configure-kernel-parameters-and-user-environments/">Изменение параметров ядра и параметров учетной записи администратора базы данных</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/create-folder-structure-and-user-permissions/">Создание структуры каталогов и назначение необходимых прав</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/copy-oracle-distrib-on-server/">Копирование дистрибутивов базы данных на сервер</a></li>


    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/check-environment-before-install/">Проверка конфигурации кластера перед инсталляцией RAC</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/check-display-manager/">Проверка работы Display Manager на компьютере с GUI</a></li>

</ul>

<br/><br/>

## Инсталляция RAC и создание экземпляров баз данных:

<ul>
	<li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/grid-installation/">Инсталляция Grid</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/oracle-database-software-installation/">Инсталляция Oracle Database Software</a></li>

    <li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/oracle-instance-creation/">Создание экземпляра (instance) базы данных</a></li>

</ul>

<br/><br/>

## Шаги, выполняемые после развертывания RAC:

<ul>
	<li><a href="/database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/post-installation-tasks/">После инсталляции</a></li>
</ul>
