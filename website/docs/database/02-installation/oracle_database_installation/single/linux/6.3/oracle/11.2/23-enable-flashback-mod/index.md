---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /oracle_database_installation/linux/6.3/oracle/11.2/enable-flashback-mod/
---

# <a href="/oracle_database_installation/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Включить режим работы FLASH BACK:


<br/>


FlashBack бывает полезен, когда нужно откатить изменения или посмотреть предыдущее состояние объектов в базе данных.
Как следствие растет нагрузка на сервер, т.к. приходится хранить дополнительную информацию.


	$ sqlplus / as sysdba



<br/>


	SQL> shutdown immediate;
	SQL> startup mount exclusive;
	SQL> alter database flashback on;
	SQL> alter database open;


<br/>

	SQL> select flashback_on from v$database;

<br/>

	FLASHBACK_ON
	------------------
	YES



UNDO_RETENTION - (при включенном FLASHBACK) определяет минимальное время в секундах, за которое можно отменить (посмотреть) изменение в базе данных. При этом данные будут храниться в UNDO_TABLESPACE (необходимо обеспечить достаточный размер табличного пространства) и перезаписываться по мере необходимости, обеспечивая минимальное значение, указанное в UNDO_RETENTION. Не поддерживается для LOB.


Задаю параметр UNDO_RETENTION равный 30 минутам


	SQL> alter system set UNDO_RETENTION = 1800;
	SQL> alter tablespace UNDO RETENTION GUARANTEE;


<br/>

	SQL> show parameter UNDO_RETENTION


<br/>

	NAME                                 TYPE        VALUE
	------------------------------------ ----------- ------------------------------
	undo_retention                       integer     1800


<br/>

	SQL> quit
