---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Инсталляция СУБД Oracle (DataBase SoftWare)
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-database-software-installation/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Инсталляция СУБД Oracle (DataBase SoftWare)


<br/>

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

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_01.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_02.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_03.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_04.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_05.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_06.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_07.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_08.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_09.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_10.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_11.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>


<br/><br/>

После появления следующего окна, необходимо выполнить под учетной записью root следующие скрипты. Рекомендуется подключиться к серверу баз данных еще одной сессией и выполнить команды в ней.

<br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_12.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>



    # /u01/oraInventory/orainstRoot.sh
    # /u01/oracle/database/12.2/root.sh



<br/><br/>

<img src="//img.oradba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/02-database-software-installation/database-software-installation_13.png" border="0" alt="Oracle DataBase 12.2 SoftWare installation"><br/><br/>
