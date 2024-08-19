---
layout: page
title: Подготовка отчета Automatic Database Diagnostic Monitor (ADDM) - Windows - Oracle 10.2
description: Подготовка отчета Automatic Database Diagnostic Monitor (ADDM) - Windows - Oracle 10.2
keywords: Oracle Database, Подготовка отчета Automatic Database Diagnostic Monitor (ADDM) - Windows - Oracle 10.2
permalink: /database/performance/addm/
---

# Подготовка отчета Automatic Database Diagnostic Monitor (ADDM) - Windows - Oracle 10.2

<br/>

Automatic Database Diagnostic Monitor (ADDM) - Монитор автоматической диагностики сервера базы данных

<br/>

Делалось в 2010

<br/>

Инструментальное средство Automatic Database Diagnostics Monitor ( ADDM монитор автоматической диагностики экземпляра сервера базы данных) в Oracle Database 10 g обнаруживает проблему прежде, чем она нанесет удар, и сообщает возможные пути ее разрешения.

Запустить ADDM можно через EM или способом описанным ниже:

<br/>

**1. Копируем файлы**

```
addmrpt.sql
addmrpti.sql
awrinpnm.sql
awrinput.sql
```

<br/>

из каталога на сервере C:\oracle\product\10.2.0\db_1\RDBMS\ADMIN на локальный диск клиента (Например в каталог C:\ADDM)

<br/>

**2. Создаем файл с именем connections.sql**

<br/>

```sql
conn system/master@10.32.11.95:1521/test;

@addmrpt.sql
```

<br/>

**3. Создаем файл с именем Run.bat**

<br/>

```
chcp 1251

sqlplus /nolog @connections.sql
exit;
```

<br/>

![Oracle DBA](/img/database/performance/addm/addm01.png 'Oracle Подготовка отчета ADDM'){: .center-image }

<br/>

**4. запускаем run.bat**

<br/>

![Oracle DBA](/img/database/performance/addm/addm02.png 'Oracle Подготовка отчета ADDM'){: .center-image }

<br/>

получаем результат.

```
DETAILED ADDM REPORT FOR TASK 'ЗАДАЧА_5154' WITH ID 5154
--------------------------------------------------------

Analysis Period: 20-МАР-2010 from 08:01:06 to 22:00:07
Database ID/Instance: 1998456309/1
Database/Instance Names: TEST/test
Host Name: 4TEST
Database Version: 10.2.0.1.0
Snapshot Range: from 2821 to 2835
Database Time: 637 seconds
Average Database Load: 0 active sessions

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~


FINDING 1: 100% impact (637 seconds)
------------------------------------
В операционной системе хоста обнаружена интенсивная подкачка данных из
виртуальной памяти.

RECOMMENDATION 1: Host Configuration, 100% benefit (637 seconds)
ACTION: В операционной системе хоста наблюдается интенсивная подкачка
данных, но определенного главного источника не выявлено. Изучите
выполняющиеся на хосте процессы, которые не принадлежат этому
экземпляру и которые потребляют значительный объем виртуальной
памяти. Рекомендуется также увеличить объем физической памяти хоста.
...


<br/>

Оперативку хочет !!!
```
