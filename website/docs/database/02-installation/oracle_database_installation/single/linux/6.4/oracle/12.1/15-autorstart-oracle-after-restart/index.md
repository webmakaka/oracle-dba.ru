---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /oracle_database_installation/linux/6.4/oracle/12.1/autorstart-oracle-after-restart/
---

# <a href="/oracle_database_installation/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Настройка автозапуска Oracle после перезагрузки



	$ vi /etc/oratab


<br/>

	orcl:/u01/oracle/database/12.1:N


заменить на


	# orcl:/u01/oracle/database/12.1:N
	orcl:/u01/oracle/database/12.1:Y


<br/>

### Создание скрипта, стартующего и останавливающего базу данных при старте и перезапуске операционной системы


Скрипт следующего содержания мы добавим в автозагрузку (выполнив команды после данного скрипта):


<script src="http://gist-it.appspot.com/https://github.com/oradev/oracle-dba-scripts/blob/master/oracle_12R1_startup_and_shutdown_script">
</script>


<br/><br/>

	# cd /tmp
	# wget -O startupOracleDatabase12R1 https://github.com/oradev/oracle-dba-scripts/raw/master/oracle_12R1_startup_and_shutdown_script
	# mv startupOracleDatabase12R1 /etc/rc.d/init.d/
	# chmod +x /etc/rc.d/init.d/startupOracleDatabase12R1
	# chkconfig --add startupOracleDatabase12R1
	# chkconfig --level 345 startupOracleDatabase12R1 on
