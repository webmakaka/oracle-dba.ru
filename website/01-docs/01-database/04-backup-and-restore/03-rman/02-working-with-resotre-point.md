---
layout: page
title: Работа с точками восстановления
description: Работа с точками восстановления
keywords: Oracle Database, Работа с точками восстановления
permalink: /database/backup-and-restore/rman/restore-points/
---

# Работа с точками восстановления

Чтобы не запоминать бездушный номар SCN, ему можно задать имя.
Например "Before_Upgrade". И в командах rman, можно также использовать понятные человеку слова исключительно для для удобства работы человека.

// Создание точки восстановления

    SQL> create restore point <pointName>;

// Создание точки восстановления с гарантией отката (при включенном flashback)

    SQL> create restore point <pointName> guarantee flashback database;

// Показать точки восстановления

    SQL> select * from v$restore_point;

// Удалить точку восстановления

    SQL> drop restore point <pointName>

// Откатиться на точку восстановления (при включенном flashback)

    SQL> shutdown immediate;
    SQL> startup mount exclusive;
    SQL> flashback database to restore point <pointName>;
    SQL> alter database open;
