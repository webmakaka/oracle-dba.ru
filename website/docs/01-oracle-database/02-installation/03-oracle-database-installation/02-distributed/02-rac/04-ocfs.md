---
layout: page
title: Oracle RAC OCFS2
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/ocfs/
---

# [Инсталляция Oracle RAC]: OCFS2


Для возможности одновременной записи на 2 ноды (primary/primary) кластера, следует использовать кластерную файловую систему, например ocfs2.


OCFS2 это кластерная файловая система общего назначения, разработанная Oracle специально для кластеризации файлов баз данных, доступна пока только для RHEL и OEL. Она может использоваться для размещения файлов Oracle Clusterware, датафайлов Oracle RAC, приложения Oracle или любых других файлов. Вторая версия OCFS имеет значительные изменения, новшества коснулись настройки использования датафайлов и файлов Oracle Clusterware.

Файловая система ocfs2, предназначенная для совместного использования двумя или более Linux-системами, т.е. мы имеем возможность одновременно монтировать разделы в режиме RW на нескольких узлах.

OCFS2 свободно распространяется Oracle в трех RPM-пакетах: модуле ядра, наборе утилит и графической консоли. Для каждой версии ядра ОС следует использовать соответствующий пакет.

Возвращаемся на шаг предшествующий созданию ASM дисков.

<!--

https://oraclelabs.wordpress.com/virtual-oracle-rac-oracle-installation/

-->

<br/>

**Конфигурация такая же как и в документе RAC 12 iSCSI + ASM**


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">


<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>


	# yum install -y \
	ocfs2-tools \
	ocfs2-tools-devel

<br/>

Если нужна gui консоль, то можно еще установить

	# yum install -y \
	ocfs2console

<br/>

	# chkconfig --level 345 o2cb on

<br/>

	 # mkfs.ocfs2 /dev/mapper/iscsi-disk1

<br/>

	# mkdir -p /u02
	# mkdir -p /etc/ocfs2/

<br/>

	# vi /etc/ocfs2/cluster.conf

<br/>

	cluster:
	    node_count = 2
	    name = ocfs2

	node:
	    ip_port = 7777
	    ip_address = 192.168.3.11
	    number = 0
	    name = rac1
	    cluster = ocfs2

	node:
	    ip_port = 7777
	    ip_address = 192.168.3.12
	    number = 1
	    name = rac2
	    cluster = ocfs2


<br/>

	# /etc/init.d/o2cb offline ocfs2
	# /etc/init.d/o2cb unload
	# /etc/init.d/o2cb configure


// Поднимаем на 2-х узлах

	# /etc/init.d/o2cb online ocfs2


Чтобы модуль поддержки OCFS2 активировался при загрузке, на каждой ноде выполняется:

	# /etc/init.d/o2cb enable

<br/>


	# /etc/init.d/o2cb load

<br/>

	# /etc/init.d/o2cb status

<br/>

### Монтирование OCFS2.

Для файловой системы, содержащей датафайлы и файлы Oracle Clusterware должно соблюдаться условие, что все операции ввода-вывода для файлов используют механизм прямого ввода-вывода I/O (O_DIRECT). Поэтому всегда используйте опцию "datavolume" при каждом монтировании файловой системы. Без этой опции отказ системы может привести к потере данных.


	# mount -t ocfs2 /dev/mapper/iscsi-disk1 -o datavolume /u02

Смонтируйте раздел OCFS2 к остальным нодам.


Чтобы файловая система монтировалась каждый раз при загрузке, на каждой ноде в /etc/fstab прописывается:

	# vi /etc/fstab

	/dev/mapper/iscsi-disk1 /u02 ocfs2 _netdev,datavolume,nointr 0 0

Для отключения периодической проверки файловой системы на ошибки выполните команду:

	/sbin/tune2fs -i 0 -c 0 /u02


<br/>

### Дополнительные команды

Возможно когда-нибудь понадобятся команды:

	/etc/init.d/ocfs2 restart
	/etc/init.d/o2cb force-reload
