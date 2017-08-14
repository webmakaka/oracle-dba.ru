---
layout: page
title: Oracle DataBase 12c - Linux - Настройка автозапуска Oracle после перезагрузки
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/autorstart-oracle-after-restart/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Настройка автозапуска Oracle после перезагрузки



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

    # vi startupOracleDatabase12.2

https://bitbucket.org/oracle-dba/oracle-dba-startup-and-shutdown-scripts/raw/b6be770160490abcc906953237985ddcfa2c7224/oracle_12R1_startup_and_shutdown_script

<!-- # wget -O startupOracleDatabase12R1 https://github.com/oradev/oracle-dba-scripts/raw/master/oracle_12R1_startup_and_shutdown_script -->

	# mv startupOracleDatabase12.2 /etc/rc.d/init.d/
	# chmod +x /etc/rc.d/init.d/startupOracleDatabase12.2
	# chkconfig --add startupOracleDatabase12.2
	# chkconfig --level 345 startupOracleDatabase12.2 on