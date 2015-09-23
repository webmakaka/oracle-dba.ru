---
layout: page
title: Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server
permalink: /database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-final-hot-backup/
---

# <a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/">[Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server]</a>:  Контрольный backup (горячий backup)

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
		BACKUP CURRENT CONTROLFILE TAG "FULL_DATABASE_CONTROLFILE";
		BACKUP SPFILE TAG "FULL_DATABASE_SPFILE";
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

Следующей командой я сообщаю, что все бекапы кроме последного, следует поменить как obsolete.


	RMAN> CONFIGURE RETENTION POLICY TO REDUNDANCY 1;

Теперь прошу RMAN удалить устаревшие бекапы (без подтверждения).


	RMAN> delete noprompt obsolete;

<br/>

	RMAN> list backup of database summary;


<br/>

	RMAN>  quit
