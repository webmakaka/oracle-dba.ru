---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Контрольный backup (горячий backup)
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-final-hot-backup/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Контрольный backup (горячий backup):


<br/>

	$ mkdir -p /u02/oracle/oradata/12.2/${ORACLE_SID}/scripts

<br/>

	$ cd /u02/oracle/oradata/12.2/${ORACLE_SID}/scripts



<br/>

	$ vi rmanscript.rman


<br/>

	RUN {
	CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET;
	BACKUP FULL DATABASE TAG "FULL_DATABASE" PLUS ARCHIVELOG TAG "FULL_DATABASE_ARCHIVELOGS";
	BACKUP CURRENT CONTROLFILE TAG "FULL_DATABASE_CONTROLFILE";
	BACKUP SPFILE TAG "FULL_DATABASE_SPFILE";
	}

Проверка синтаксиса созданного файла сценария


	$ rman CHECKSYNTAX @rmanscript.rman

Выполнение скрипта резервного копирования


	$ rman target / @rmanscript.rman



<br/>

### Посмотреть список бекапов

	RMAN> rman target /


<br/>

	RMAN> list backup of database summary;

<br/>

Следующей командой я сообщаю, что все бекапы кроме последного, следует поменить как obsolete.


	RMAN> CONFIGURE RETENTION POLICY TO REDUNDANCY 1;


Теперь говорю RMAN удалить устаревшие бекапы (без подтверждения).


	RMAN> delete noprompt obsolete;

<br/>

	RMAN> list backup of database summary;

    List of Backups
    ===============
    Key     TY LV S Device Type Completion Time     #Pieces #Copies Compressed Tag
    ------- -- -- - ----------- ------------------- ------- ------- ---------- ---
    1       B  F  A DISK        14/08/2017 14:31:28 1       1       NO         FULL_DATABASE_DATAFILES
    8       B  F  A DISK        14/08/2017 15:15:39 1       1       YES        FULL_DATABASE


<br/>

	RMAN>  quit
