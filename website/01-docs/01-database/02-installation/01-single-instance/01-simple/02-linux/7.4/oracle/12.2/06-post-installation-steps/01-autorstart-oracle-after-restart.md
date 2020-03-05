---
layout: page
title: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Настройка автозапуска Oracle после перезагрузки
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Настройка автозапуска Oracle после перезагрузки
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, автозапуск Oracle
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/autorstart-oracle-after-restart/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Настройка автозапуска Oracle после перезагрузки


<br/>

	$ vi /etc/oratab


<br/>

	orcl12:/u01/oracle/database/12.2:N


заменить на


	# orcl12:/u01/oracle/database/12.2:N
	orcl12:/u01/oracle/database/12.2:Y


<br/>

### Создание скрипта, стартующего и останавливающего базу данных при старте и перезапуске операционной системы


<!-- Скрипт следующего содержания мы добавим в автозагрузку (выполнив команды после данного скрипта):


<script src="http://gist-it.appspot.com/https://github.com/oradev/oracle-dba-scripts/blob/master/oracle_12R1_startup_and_shutdown_script">
</script> -->


	# cd /tmp

    # vi oracle_12.2_startup_and_shutdown_script

https://bitbucket.org/oracle-dba/oracle-dba-startup-and-shutdown-scripts/src/14797e3bf31c47d9b70b98539e8f248650666a97/oracle_12.2_startup_and_shutdown_script?at=master&fileviewer=file-view-default

<!-- # wget -O startupOracleDatabase12R1 https://github.com/oradev/oracle-dba-scripts/raw/master/oracle_12R1_startup_and_shutdown_script -->

	# mv oracle_12.2_startup_and_shutdown_script /etc/rc.d/init.d/
	# chmod +x /etc/rc.d/init.d/oracle_12.2_startup_and_shutdown_script
	# chkconfig --add oracle_12.2_startup_and_shutdown_script
	# chkconfig --level 345 oracle_12.2_startup_and_shutdown_script on
