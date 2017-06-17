---
layout: page
title: Oracle DataBase 12c - Linux - Создание резервной копии созданной базы данных (холодный бекап)
permalink: /database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-cold-backup/
---

# <a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Создание резервной копии созданной базы данных (холодный бекап)



Выполните следующие команды:

	$ sqlplus / as sysdba

<br/>

	SQL> shutdown immediate;
	SQL> startup mount;
	SQL> quit


<br/>

	$ rman target /



<br/>


	RMAN> backup full database noexclude include current controlfile spfile TAG "FULL_COLD_BACKUP";


<br/>

	****
	channel ORA_DISK_1: backup set complete, elapsed time: 00:00:01
	Finished backup at 06.09.2013 06:12:32


<br/>


	RMAN> sql 'alter database open';


<br/>

	RMAN> quit

<br/>

	$ sqlplus / as sysdba



Получить информацию о использовании FRA


	SQL> SELECT
	    TO_CHAR(SPACE_USED, '999,999,999,999') AS "Used",
	    TO_CHAR(SPACE_LIMIT - SPACE_USED + SPACE_RECLAIMABLE, '999,999,999,999')
	       AS "Free",
	    ROUND((SPACE_USED - SPACE_RECLAIMABLE)/SPACE_LIMIT * 100, 1)
	       AS "Used %"
	    FROM V$RECOVERY_FILE_DEST;


<br/>

	Used		 Free		      Used %
	---------------- ---------------- ----------
	     440,131,584   21,034,704,896	   2


<br/>

	SQL> quit



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
