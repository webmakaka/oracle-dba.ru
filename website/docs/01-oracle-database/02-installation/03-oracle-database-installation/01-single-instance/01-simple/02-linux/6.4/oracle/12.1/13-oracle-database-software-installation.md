---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-database-software-installation/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Инсталляция СУБД Oracle (DataBase SoftWare)


### Проверка конфигурации перед инсталляцией:


<br/><br/>

Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.


	# su - oracle
	$ cd /tmp

<br/>

	$ unzip linuxamd64_12c_database_1of2.zip; \
unzip linuxamd64_12c_database_2of2.zip


<br/>

	$ cd /tmp/database


<br/>

	$ export DISPLAY=192.168.1.5:0.0


<br/>

	$ ./runInstaller -executeSysPrereqs


<br/>


	Starting Oracle Universal Installer...

	Checking Temp space: must be greater than 500 MB.   Actual 27124 MB    Passed
	Checking swap space: must be greater than 150 MB.   Actual 3967 MB    Passed
	Checking monitor: must be configured to display at least 256 colors.    Actual 16777216    Passed
	Exiting Oracle Universal Installer, log for this session can be found at /tmp/OraInstall2013-09-06_03-31-58AM/installActions2013-09-06_03-31-58AM.log



### Запуск программы инсталляции базы данных:

	$ ./runInstaller


В некоторых случаях приходится запускать инсталляцию с игнорированием системных сообщений


	$ ./runInstaller -ignoreSysPrereqs


<br/><br/>
Если все нормально, появится картинка:

<br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_01.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_02.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_03.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_04.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_05.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_06.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_07.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_08.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_09.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_10.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_11.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_12.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_13.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<br/><br/>

После появления следующего окна, необходимо выполнить под учетной записью root следующие скрипты. Рекомендуется подключиться к серверу баз данных еще одной сессией.

<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_14.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>


	# /u01/oraInventory/orainstRoot.sh


<br/>


	Changing permissions of /u01/oraInventory.
	Adding read,write permissions for group.
	Removing read,write,execute permissions for world.

	Changing groupname of /u01/oraInventory to oinstall.
	The execution of the script is complete.



	# /u01/oracle/database/12.1/root.sh


	Performing root user operation for Oracle 12c

	The following environment variables are set as:
	    ORACLE_OWNER= oracle
	    ORACLE_HOME=  /u01/oracle/database/12.1

	Enter the full pathname of the local bin directory: [/usr/local/bin]:
	   Copying dbhome to /usr/local/bin ...
	   Copying oraenv to /usr/local/bin ...
	   Copying coraenv to /usr/local/bin ...


	Creating /etc/oratab file...
	Entries will be added to the /etc/oratab file as needed by
	Database Configuration Assistant when a database is created
	Finished running generic part of root script.
	Now product-specific root actions will be performed.


<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/12.1/software/oracle12R1_database_software_installation_15.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
