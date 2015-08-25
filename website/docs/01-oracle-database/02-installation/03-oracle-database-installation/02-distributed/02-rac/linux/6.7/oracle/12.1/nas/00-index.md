---
layout: page
title: Инсталляция Oracle RAC 12.1 в операционной системе Oracle Linux 6.7 x86_64 (NFS)
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/
---

# [Инсталляция Oracle RAC 12.1]: Инсталляция Oracle RAC 12.1 в операционной системе Oracle Linux 6.7 (NFS)


<br/>

В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Oracle Linux в конфигурации Real Application Cluster (RAC).


В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, пишите мне адрес эл. почты:


<div>
	<img src="http://img.fotografii.org/a3333333mail.gif" border="0">
</div>

<br/><br/>



## Документация:

<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/docs/">Официальная документация</a><br/></li>
</ul>


<br/><br/>


## Описание окружения для инсталляции Oracle RAC:

<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/environment-description/">Описание окружения для инсталляции Oracle RAC</a><br/></li>
</ul>



<br/><br/>
<h2>Дистрибутивы:</h2>


<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/distrib/">Дистрибутивы баз данных и дополнительное программное обеспечение</a><br/></li>
</ul>

<br/><br/>


# Заменить название

-- Ошибки в DNS корневой каталог

### Инсталляция DNS сервера:

<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/setup-dns-server/">Настройка DNS сервера</a><br/></li>
</ul>



### Подготовка окружения для инсталляции RAC:


<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/setup-os-parameters-before-begin/">Предварительные настройки</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/setup-dns-server/">Настройка DNS сервера</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/network-interfaces/">Настройка конфигурации сетевых интерфейсов</a><br/></li>


	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/install-mandatory-packages/">Инсталляция необходимых пакетов</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/autostart-only-packages-what-needed/">Выбор пакетов для автозапуска</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/setup-actual-time/">Настройка сервисов отвечающих за синхронизацию времени</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/users-and-groups-creation/">Создание пользователя oracle12 и административных групп</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/secure-shell-between-nodes/">Настройка Secure Shell между узлами кластера</a><br/></li>


	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/prepare-storage/">Подготовка RAID на сервере storage. Расшаривание RAID</a><br/></li>


	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/prepare-hdd-to-install-oracle/">Подготовка дисков на узлах кластера</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/mount-raid-on-nodes/">Монтирование RAID на узлах кластера</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/prepare-kernel-parameters-and-user-environments/">Изменение параметров ядра и параметров учетной записи администратора базы данных</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/create-folder-structure-and-user-permissions/">Создание структуры каталогов и назначение необходимых прав</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/copy-oracle-distrib-on-server/">Копирование дистрибутивов базы данных на сервер</a><br/></li>


	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/check-environment-before-install/">Проверка конфигурации кластера перед инсталляцией RAC</a><br/></li>


</ul>

<br/><br/>

## Инсталляция RAC и создание экземпляров баз данных:


<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/grid-installation/">Инсталляция Grid</a><br/></li>

	<li><a href=" /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/oracle-database-software-installation/">Инсталляция Oracle Database Software</a><br/></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/oracle-instance-creation/">Создание экземпляра (instance) базы данных</a><br/></li>

</ul>


<br/><br/>

## Шаги, выполняемые после развертывания RAC:


<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/post-installation-tasks/">После инсталляции</a><br/></li>
</ul>
