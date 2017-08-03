---
layout: page
title: Oracle DataBase 12c - Linux - Создание структуры каталогов и назначение необходимых прав
permalink: /database/installation/single-instance/simple/linux/7.3/oracle/12.2/create-folder-structure-and-user-permissions/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Создание структуры каталогов и назначение необходимых прав

	# mkdir -p /u01/oracle/database/12.2
	# chown -R oracle12:dba /u01/oracle
	# chmod -R 775 /u01/oracle/database/12.2

	# mkdir -p /u01/oraInventory
	# chown -R oracle12:oinstall /u01/oraInventory
	# chmod -R 775 /u01/oraInventory

	# mkdir -p /u02/oracle/oradata/12.2
	# chown -R oracle12:dba /u02/oracle/oradata/12.2
	# chmod -R 775 /u02/oracle/oradata/12.2

	# mkdir -p /u03/oracle/oradata/12.2/orcl12/backups
	# chown -R oracle12:dba /u03/oracle/oradata/12.2/orcl12/
	# chmod -R 775 /u03/oracle/oradata/12.2/orcl12/

    # mkdir -p /distrib/oracle/12.2/
    # chown -R oracle12:dba /distrib/oracle/12.2/
    # chmod -R 775 /distrib/oracle/12.2/
