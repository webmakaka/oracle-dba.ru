---
layout: page
title: Создание экземпляра базы данных (Instance)
permalink: /oracle-database-installation/single/asm/linux/6.7/oracle/12.1/oracle-instance-creation/
---

# <a href="/oracle-database-installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Создание экземпляра базы данных (Instance)


Определите системную переменную DISPLAY следующим образом (если она не поределена).

	$ export DISPLAY=192.168.1.5:0.0


	$ dbca


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_01.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_02.png" border="0" alt="oracle database software installation"><br/><br/>


<br/><br/>

В режиме Advanced, можно более оптимально настроить параметры. Исключить из установки лишнее. Например, JVM, Enterprise Manager, Multimedia. Можно выделить побольше ресурсов памяти.  
http://oracle-dba.ru/oracle-database-installation/linux/6.4/oracle/12.1/oracle-instance-creation/



<br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_03.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_04.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_05.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_06.png" border="0" alt="oracle database software installation"><br/><br/>


<br/>
<br/>

Узнать порт подключения к EM:

	SQL> select dbms_xdb_config.gethttpsport() from dual;

	DBMS_XDB_CONFIG.GETHTTPSPORT()
	------------------------------
				  5500



Можно подключиться к EM:  
https://192.168.1.11:5500/em/


<br/>

### После инсталляционные шаги



	$ vi /etc/oratab

<br/>

	+ASM:/u01/oracle/grid/12.1:N
	orcl12:/u01/oracle/database/12.1:N

меняю на

	+ASM:/u01/oracle/grid/12.1:Y
	orcl12:/u01/oracle/database/12.1:Y



<br/>

	SQL> select name, total_mb, free_mb from v$asm_diskgroup;

	NAME				 TOTAL_MB    FREE_MB
	------------------------------ ---------- ----------
	DATA				   163836     159704
	ARCH				    81918      81452
