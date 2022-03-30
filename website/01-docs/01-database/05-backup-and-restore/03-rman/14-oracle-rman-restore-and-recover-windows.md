---
layout: page
title: Восстановление из резервной копий с помощью утилиты RMAN (Recovery Manager) Пример с Windows из телеграм чата
description: Восстановление из резервной копий с помощью утилиты RMAN (Recovery Manager) Пример с Windows из телеграм чата
keywords: Oracle Database, RMAN, Restore, Пример с Windows из телеграм чата, Oracle 11, Windows Server
permalink: /database/backup-and-restore/rman/oracle-rman-restore-and-recover-windows/
---

# Восстановление из резервной копий с помощью утилиты RMAN (Recovery Manager) Пример с Windows из телеграм чата

<br/>

Oracle 11, Windows Server

<br/>

**Актуальность:**  
30.03.2022

<br/>

Да нужно разбираться, чтобы понять что да как.

<br/>

```
Попробую детально описать свои задачи, действия и проблемы.
Необходимо развернуть БД из определенных готовых бэкапов на новом сервере.
количество дисков и их наименование отличается от исходного сервера.

ОС Windows
на новом сервере установлен oracle 11g и создана база при установке. Она ничем не наполнена.
есть полный инкрементальный бэкап level 0,
 и один следующий за ним инкрементальный коммулятивный бэкап level 1
archive.log включены в бэкап
Восстановление самих бэкапов (2 папки с файлами бэкапов) на сервер происходило с ленты.
Был создан pfile из spfile исходной БД. Откорректирован в соответствии с новыми путями и именами.
На новом сервере был запущен ряд команд по развертыванию из бэкапа:

1. Startup nomount pfile -мой pfile

2. RESTORE CONTROLFILE FROM  - файл бэкапа с контрол файлом.

3. ALTER DATABASE MOUNT;

4. catalog start with '\мой backupset'

5. запускаю скрипт
run {
SET NEWNAME FOR DATABASE   TO  '\oradata\мой_сид\%b';
SET NEWNAME FOR tempfile  1 TO  '\oradata\мой_сид\%b';
restore database;
switch datafile all;
switch tempfile all;
}

Сегодня вижу, что restore прошел успешно.


Но, боюсь запускать следующий шаг
run {
set until sequence xxxxx thread 1;
recover database;
} alter database open resetlogs;
```

<br/>

https://t.me/oracle_dba_ru/16630

<br/>

См. предыдущие сообщения.
