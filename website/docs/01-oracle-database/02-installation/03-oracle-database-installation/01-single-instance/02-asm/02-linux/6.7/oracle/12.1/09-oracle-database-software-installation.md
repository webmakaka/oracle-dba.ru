---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Инсталляция СУБД Oracle (DataBase SoftWare)
permalink: /docs/oracle-database/installation/oracle-database-installation/single/asm/linux/6.7/oracle/12.1/oracle-database-software-installation/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Инсталляция СУБД Oracle (DataBase SoftWare)


Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle12

<br/>

	$ source ~/.bash_profile

<br/>

	$ cd /tmp/oracle/12.1/database/


Определите системную переменную DISPLAY следующим образом.

	$ export DISPLAY=192.168.1.5:0.0

В данном случае 192.168.1.5 - ip адрес компьютера, с которого происходит процесс управления установкой.

	$ ./runInstaller


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_01.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_02.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_03.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_04.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_05.png" border="0" alt="oracle database software installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_06.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_07.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_08.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_09.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_10.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_11.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_12.png" border="0" alt="oracle database software installation"><br/><br/>

<br/><br/>

	# /u01/oracle/database/12.1/root.sh
	Performing root user operation.

	The following environment variables are set as:
	    ORACLE_OWNER= oracle12
	    ORACLE_HOME=  /u01/oracle/database/12.1

	Enter the full pathname of the local bin directory: [/usr/local/bin]:
	The contents of "dbhome" have not changed. No need to overwrite.
	The contents of "oraenv" have not changed. No need to overwrite.
	The contents of "coraenv" have not changed. No need to overwrite.

	Entries will be added to the /etc/oratab file as needed by
	Database Configuration Assistant when a database is created
	Finished running generic part of root script.
	Now product-specific root actions will be performed.

<br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/03-oracle-database-software-installation/oracle-database-software-installation_13.png" border="0" alt="oracle database software installation"><br/><br/>
