---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-database-software-installation/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Инсталляция СУБД Oracle (DataBase SoftWare)


Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle11

<br/>

	$ cd /tmp

<br/>

	$ unzip p10404530_112030_Linux-x86-64_1of7.zip; \
	unzip p10404530_112030_Linux-x86-64_2of7.zip

<br/>
		$ cd /tmp/database

Определите переменную окружения DISPLAY следующим образом.

	$ export DISPLAY=192.168.1.200:0.0

В данном случае 192.168.1.200 - ip адрес компьютера, с которого происходит процесс управления установкой. На этом компьютере должен быть стартован xserver, например XMing (под windows).


Если установка происходит с linux, можно посмотреть инстукции как и что настраивается в версии докумена с базой oracle 12.

### Проверка конфигурации перед инсталляцией:

	$ ./runInstaller -executeSysPrereqs


<br/>

	Starting Oracle Universal Installer...

	Checking Temp space: must be greater than 120 MB.   Actual 27697 MB    Passed
	Checking swap space: must be greater than 150 MB.   Actual 4031 MB    Passed
	Checking monitor: must be configured to display at least 256 colors.    Actual 65536    Passed
	Exiting Oracle Universal Installer, log for this session can be found at /tmp/OraInstall2012-06-10_03-03-29AM/installActions2012-06-10_03-03-29AM.log



### Запус программы инсталляции базы данных:

	$ ./runInstaller

В некоторых случаях приходится запускать инсталляцию с игнорированием системных сообщений. Крайне не рекомендуется.

	$ ./runInstaller -ignoreSysPrereqs


Если все нормально, появится картинка:  



<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_01.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_02.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_03.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_04.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_05.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_06.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_07.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_08.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_09.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_10.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_11.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_12.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_13.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_14.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_15.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_16.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/oracle11_database_software_installation_17.PNG" border="0" alt="Oracle RAC installation"><br/><br/>



После появления следующего окна, необходимо выполнить под учетной записью root следующие скрипты. Рекомендуется подключиться к серверу баз данных еще одной сессией putty.

<br/>


	# /u01/oraInventory/orainstRoot.sh



<br/>


	Changing permissions of /u01/oraInventory.
	Adding read,write permissions for group.
	Removing read,write,execute permissions for world.

	Changing groupname of /u01/oraInventory to oinstall.
	The execution of the script is complete.


<br/>


	# /u01/oracle/database/11.2/root.sh


<br/>

	Performing root user operation for Oracle 11g

	The following environment variables are set as:
	    ORACLE_OWNER= oracle11
	    ORACLE_HOME=  /u01/oracle/database/11.2

	Enter the full pathname of the local bin directory: [/usr/local/bin]:
	   Copying dbhome to /usr/local/bin ...
	   Copying oraenv to /usr/local/bin ...
	   Copying coraenv to /usr/local/bin ...


	Creating /etc/oratab file...
	Entries will be added to the /etc/oratab file as needed by
	Database Configuration Assistant when a database is created
	Finished running generic part of root script.
	Now product-specific root actions will be performed.
	Finished product-specific root actions.



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
