---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /database/installation/distributed/rac/linux/5.8/oracle/11.2/
---

# [Инсталляция Oracle RAC 11.2]: В конфигурации с использованием iSCSI и ASM в операционной системе Oracle Linux 5.8 x86_64


<br/>


В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Oracle Linux в конфигурации Real Application Cluster (RAC).


В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, пишите мне адрес эл. почты:


<div>
	<img src="http://img.fotografii.org/a3333333mail.gif" alt="Marley" border="0">
</div>

<br/><br/>

### Документация:

<ul>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/docs/">Официальная документация</a><br/></li>
</ul>


<br/>

### Описание окружения для инсталляции Oracle RAC:

<ul>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/environment-description/">Описание окружения для инсталляции Oracle RAC</a><br/></li>
</ul>


<br/><br/>
<h2>Дистрибутивы:</h2>


<ul>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/distrib/">Дистрибутивы баз данных и дополнительное программное обеспечение</a><br/></li>
</ul>

<br/><br/>

### Подготовка окружения для инсталляции RAC:

<ul>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/setup-os-parameters-before-begin/">Предварительные настройки</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/setup-actual-time/">Настройка сервисов отвечающих за синхронизацию времени</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/setup-dns-server/">Настройка DNS сервера</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/network-interfaces/">Настройка сетевых интерфейсов и файл hosts</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/users-and-groups-creation/">Создание пользователя oracle11 и групп</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/secure-shell-between-nodes/">Настройка Secure Shell между узлами кластера</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/install-mandatory-packages/">Инсталляция необходимых пакетов</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/autostart-only-packages-what-needed/">Выбор пакетов для автозапуска</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/prepare-hdd-to-install-oracle/">Подготовка дисков</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/prepare-iscsi-discs/">Инсталляция ISCSI и монтирование iscsi дисков</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/prepare-asm-discs/">Инсталляция и конфигурирование ASM</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/prepare-kernel-parameters-and-user-environments/">Изменение параметров ядра и параметров учетной записи администратора базы данных</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/create-folder-structure-and-user-permissions/">Создание структуры каталогов и назначение необходимых прав</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/check-environment-before-install/">Проверка конфигурации кластера перед инсталляцией RAC</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/copy-oracle-distrib-on-server/">Копирование дистрибутивов базы данных на сервер</a><br/></li>
</ul>


<br/>

### Инсталляция RAC и создание экземпляров баз данных:


<ul>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/grid-installation/">Инсталляция Grid</a><br/></li>
	<li><a href=" /database/installation/distributed/rac/linux/5.8/oracle/11.2/oracle-database-software-installation/">Инсталляция Oracle Database Software</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/oracle-instance-creation/">Создание экземпляра (instance) базы данных</a><br/></li>
</ul>


<br/>

### Шаги, выполняемые после развертывания RAC:


<ul>

	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/post-installation-tasks/">После инсталляции</a><br/></li>
	<li><a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/patching/">Применение патчей (11.2.0.3.2)</a><br/></li>
</ul>
