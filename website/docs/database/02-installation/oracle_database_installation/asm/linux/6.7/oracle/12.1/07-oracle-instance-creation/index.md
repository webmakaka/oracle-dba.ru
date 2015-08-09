---
layout: page
title: Создание экземпляра базы данных (Instance)
permalink: /oracle_database_installation/asm/linux/6.7/oracle/12.1/oracle-instance-creation/
---

# <a href="/oracle_database_installation/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Создание экземпляра базы данных (Instance)


	$ dbca


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-instance-creation/oracle-instance-creation_01.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-instance-creation/oracle-instance-creation_02.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-instance-creation/oracle-instance-creation_03.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-instance-creation/oracle-instance-creation_04.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-instance-creation/oracle-instance-creation_05.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-instance-creation/oracle-instance-creation_06.png" border="0" alt="oracle database software installation"><br/><br/>

	$ vi /etc/oratab

<br/>

	+ASM:/u01/oracle/grid/12.1:N            # line added by Agent
	ora121:/u01/oracle/database/12.1:N              # line added by Agent

меняю на

	+ASM:/u01/oracle/grid/12.1:Y            # line added by Agent
	ora121:/u01/oracle/database/12.1:Y              # line added by Agent
