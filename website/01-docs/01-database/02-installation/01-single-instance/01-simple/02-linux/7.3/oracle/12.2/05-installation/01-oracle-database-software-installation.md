---
layout: page
title: Oracle DataBase 12c - Linux - Инсталляция СУБД Oracle (DataBase SoftWare)
permalink: /database/installation/single-instance/simple/linux/7.3/oracle/12.2/oracle-database-software-installation/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Инсталляция СУБД Oracle (DataBase SoftWare)


### Проверка конфигурации перед инсталляцией:


	$ cd /distrib/oracle/12.2/database/


<br/>

	$ ./runInstaller -executeSysPrereqs


<br/>

	Starting Oracle Universal Installer...

	Checking Temp space: must be greater than 500 MB.   Actual 26663 MB    Passed
	Checking swap space: must be greater than 150 MB.   Actual 3967 MB    Passed
	Checking monitor: must be configured to display at least 256 colors.    Actual 16777216    Passed
	Exiting Oracle Universal Installer, log for this session can be found at /tmp/OraInstall2015-09-15_09-20-12PM/installActions2015-09-15_09-20-12PM.log



<br/>

### Запуск программы инсталляции базы данных:


Если переменная DISPLAY не задана.

	$ export DISPLAY=192.168.1.5:0.0

<br/>

	$ ./runInstaller


В некоторых случаях приходится запускать инсталляцию с игнорированием системных сообщений


	$ ./runInstaller -ignoreSysPrereqs


<br/><br/>
Если все нормально, появится картинка:

<br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_01.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_02.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_03.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_04.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_05.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_06.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_07.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_08.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_09.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_10.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_11.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_12.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_13.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>


<br/><br/>

После появления следующего окна, необходимо выполнить под учетной записью root следующие скрипты. Рекомендуется подключиться к серверу баз данных еще одной сессией и выполнить команды в ней.

<br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_14.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>


	# /u01/oraInventory/orainstRoot.sh


<br/>


	Changing permissions of /u01/oraInventory.
	Adding read,write permissions for group.
	Removing read,write,execute permissions for world.

	Changing groupname of /u01/oraInventory to oinstall.
	The execution of the script is complete.


<br/>


	# /u01/oracle/database/12.1/root.sh


	# /u01/oracle/database/12.1/root.sh
	Performing root user operation.

	The following environment variables are set as:
	    ORACLE_OWNER= oracle12
	    ORACLE_HOME=  /u01/oracle/database/12.1

	Enter the full pathname of the local bin directory: [/usr/local/bin]: [Enter]
	   Copying dbhome to /usr/local/bin ...
	   Copying oraenv to /usr/local/bin ...
	   Copying coraenv to /usr/local/bin ...


	Creating /etc/oratab file...
	Entries will be added to the /etc/oratab file as needed by
	Database Configuration Assistant when a database is created
	Finished running generic part of root script.
	Now product-specific root actions will be performed.



<br/><br/>

<img src="http://img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/6.7/oracle/12.1/02_database_software_installation/oracle12R1_database_software_installation_15.png" border="0" alt="Oracle 12 relese 1 installation on Linux"><br/><br/>
