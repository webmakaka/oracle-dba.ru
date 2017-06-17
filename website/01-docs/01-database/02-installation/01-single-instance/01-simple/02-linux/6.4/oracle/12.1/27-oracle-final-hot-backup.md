---
layout: page
title: Oracle DataBase 12c - Linux - Контрольный backup (горячий backup)
permalink: /database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-final-hot-backup/
---

# <a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Контрольный backup (горячий backup):



	$ mkdir -p /u02/oracle/oradata/${ORACLE_SID}/scripts

<br/>

	$ cd /u02/oracle/oradata/${ORACLE_SID}/scripts



<br/>

	$ vi rmanscript.rman


<br/>

	RUN {
	CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET;
	BACKUP FULL DATABASE TAG "FULL_DATABASE" PLUS ARCHIVELOG TAG "FULL_DATABASE_ARCHIVELOGS";
	}



Проверка синтаксиса созданного файла сценария


	$ rman CHECKSYNTAX @rmanscript.rman

Выполнение скрипта резервного копирования


	$ rman target / @rmanscript.rman



<h3>Посмотреть список бекапов</h3>



	RMAN> rman target /



<br/>

	RMAN> list backup of database summary;


<br/>


	List of Backups
	===============
	Key     TY LV S Device Type Completion Time     #Pieces #Copies Compressed Tag
	------- -- -- - ----------- ------------------- ------- ------- ---------- ---
	1       B  F  A DISK        06.09.2013 06:12:23 1       1       NO         TAG20130906T061141
	5       B  F  A DISK        06.09.2013 07:35:00 1       1       YES        FULL_DATABASE



Следующей командой я сообщаю, что все бекапы кроме последного, следует поменить как obsolete.


	RMAN> CONFIGURE RETENTION POLICY TO REDUNDANCY 1;


Теперь прошу RMAN удалить устаревшие бекапы (без подтверждения).


	RMAN> delete noprompt obsolete;

<br/>

	RMAN> list backup of database summary;


<br/>

	List of Backups
	===============
	Key     TY LV S Device Type Completion Time     #Pieces #Copies Compressed Tag
	------- -- -- - ----------- ------------------- ------- ------- ---------- ---
	5       B  F  A DISK        06.09.2013 07:35:00 1       1       YES        FULL_DATABASE

<br/>


	RMAN>  quit




<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
