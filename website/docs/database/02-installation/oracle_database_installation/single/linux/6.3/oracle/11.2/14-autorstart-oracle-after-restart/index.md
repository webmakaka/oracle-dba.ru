---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /oracle_database_installation/linux/6.3/oracle/11.2/autorstart-oracle-after-restart/
---

# <a href="/oracle_database_installation/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Настройка автозапуска Oracle после перезагрузки


<br/>

	$ vi /etc/oratab

<br/>

	ora112:/u01/oracle/database/11.2:N

заменить на

	# ora112:/u01/oracle/database/11.2:N
	ora112:/u01/oracle/database/11.2:Y


### Создание скрипта, стартующего и останавливающего базу данных при старте и перезапуске операционной системы:

Создайте скрипт для запуска базы данных следующего содержания.

	# vi /etc/rc.d/init.d/startupOracleDatabase11GR2


<script src="http://gist-it.appspot.com/https://github.com/oradev/oracle-dba-scripts/blob/master/oracle_11GR2_startup_and_shutdown_script">
</script>


	# chmod +x /etc/rc.d/init.d/startupOracleDatabase11GR2
	# chkconfig --add startupOracleDatabase11GR2
	# chkconfig --level 345 startupOracleDatabase11GR2 on
