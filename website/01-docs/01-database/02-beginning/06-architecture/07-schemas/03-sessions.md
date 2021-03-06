---
layout: page
title: Сессии к базе данных Oracle
description: Сессии к базе данных Oracle
keywords: Oracle Database, Sessions
permalink: /docs/architecture/schemas/sessions/
---

# Сессии к базе данных Oracle

<h3>Список:</h3>

<ul>
    <li><a href="#sessions1">Посмотреть текущие сессии к базе данных</a></li>
    <li><a href="#sessions2">Найти блокирующую сессию</a></li>
    <li><a href="#sessions3">Убить сессию</a></li>
    <li><a href="#sessions4">Убийство всех сессий к одной схеме</a></li>
    <li><a href="#sessions5">Отследить, какой запрос выполняет приложение</a></li>
</ul>

<h3><a name="sessions1">Посмотреть текущие сессии к базе данных</a></h3>

```sql
    SELECT t.SID, t.SERIAL#, t.osuser as "User", t.MACHINE as "PC", t.PROGRAM as "Program"
    FROM v$session t
    --WHERE (NLS_LOWER(t.PROGRAM) = 'cash.exe') -- посмотреть сессии от программы cash.exe
    --WHERE status='ACTIVE' and osuser!='SYSTEM' -- посмотреть пользовательские сессии
    --WHERE username = 'схема' -- посмотреть сессии к схеме (пользователь)
    ORDER BY 4 ASC;
```

<br/>
<h3><a name="sessions2">Найти блокирующую сессию</a></h3>

```sql
SELECT status, SECONDS_IN_WAIT, BLOCKING_SESSION, SEQ#
FROM v$session
WHERE username=upper('scott');
```

<br/>
<h3><a name="sessions3">Убить сессию</a></h3>

    ALTER SYSTEM KILL SESSION 'SID,Serial#' IMMEDIATE;

Заменить 'SID' и 'Serial#' на текущие значения сессии.

<br/>
<h3><a name="sessions4">Убийство всех сессий к определенной схеме</a></h3>

```sql
define USERNAME = "USER_NAME"

begin
    for i in (select SID, SERIAL# from V$SESSION where USERNAME = upper('&&USERNAME')) loop
    execute immediate 'alter system kill session '''||i.SID||','||i.SERIAL#||''' immediate';
    end loop;
end;
/
```

<br/>
<h3><a name="sessions5">Отследить, какой запрос выполняет приложение</a></h3>

```sql
SELECT PROCESS pid, sess.process, sess.status, sess.username, sess.schemaname, sql.sql_text
FROM v$session sess, v$sql sql
WHERE sql.sql_id(+) = sess.sql_id AND sess.type = 'USER';
```
