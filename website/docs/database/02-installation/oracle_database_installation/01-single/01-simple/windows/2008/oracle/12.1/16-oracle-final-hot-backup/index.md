---
layout: page
title: Инсталляция Oracle Database 12g Release 1 в Microsoft Windows 2008 Server
permalink: /oracle-database-installation/windows/2008/oracle/12.1/oracle-final-hot-backup/
---

# <a href="/oracle-database-installation/windows/2008/oracle/12.1/">[Инсталляция Oracle Database 12g Release 1 в Microsoft Windows 2008 Server]</a>:  Контрольный backup (горячий backup)

<br/>

	CMD>
	CMD> e:
	CMD> md  E:\app\oracle\oradata\ora121\scripts
	CMD> cd E:\app\oracle\oradata\ora121\scripts

<br/>

	$ Создаем файл с именем rmanscript.rman

<br/>

	RUN {
	CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET;
	BACKUP FULL DATABASE TAG "FULL_DATABASE" PLUS ARCHIVELOG TAG "FULL_DATABASE_ARCHIVELOGS";
	}


Проверка синтаксиса созданного файла сценария

	rman CHECKSYNTAX @rmanscript.rman


Выполнение скрипта резервного копирования

	rman target / @rmanscript.rman


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



<br/>

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
