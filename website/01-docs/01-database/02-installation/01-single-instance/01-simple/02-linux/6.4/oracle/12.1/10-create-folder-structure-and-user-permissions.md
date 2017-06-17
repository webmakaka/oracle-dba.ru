---
layout: page
title: Oracle DataBase 12c - Linux - Создание структуры каталогов и назначение необходимых прав
permalink: /database/installation/single-instance/simple/linux/6.4/oracle/12.1/create-folder-structure-and-user-permissions/
---

# <a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Создание структуры каталогов и назначение необходимых прав


	# mkdir -p /u01/oracle/database/12.1
	# chown -R oracle:dba /u01/oracle
	# chmod -R 775 /u01/oracle/database/12.1


	# mkdir -p /u01/oraInventory
	# chown -R oracle:oinstall /u01/oraInventory
	# chmod -R 775 /u01/oraInventory


	# mkdir -p /u02/oracle/oradata
	# chown -R oracle:dba /u02/oracle/oradata
	# chmod -R 775 /u02/oracle/oradata

	# mkdir -p /u03/oracle/oradata
	# chown -R oracle:dba /u03/oracle/oradata
	# chmod -R 775 /u03/oracle/oradata

	# mkdir -p /u03/oracle/oradata/orcl/backups
	# chown -R oracle:dba /u03/oracle/oradata
	# chmod -R 775 /u03/oracle/oradata



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
