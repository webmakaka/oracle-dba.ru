---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /oracle-database-installation/linux/6.4/oracle/12.1/enable-flashback-mod/
---

# <a href="/oracle-database-installation/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Включить режим работы FLASH BACK




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


<br/>

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
