---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-final-hot-backup/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Контрольный backup (горячий backup):


<br/>

	$ cd /u03/orabackups

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


Посмотреть список бекапов:


	RMAN> rman target /

<br/>

	RMAN> list backup of database summary;

<br/>

	List of Backups
	===============
	Key     TY LV S Device Type Completion Time     #Pieces #Copies Compressed Tag
	------- -- -- - ----------- ------------------- ------- ------- ---------- ---
	1       B  F  A DISK        10.06.2012 22:05:45 1       1       NO         TAG20120610T220429
	6       B  F  A DISK        10.06.2012 22:12:46 1       1       NO         TAG20120610T221132
	10      B  F  A DISK        10.06.2012 23:21:10 1       1       YES        FULL_DATABASE



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
	10      B  F  A DISK        10.06.2012 23:21:10 1       1       YES        FULL_DATABASE


<br/>

	RMAN>  quit
