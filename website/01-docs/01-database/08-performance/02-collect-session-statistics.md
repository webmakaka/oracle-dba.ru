---
layout: page
title: Собрать статистику пользовательской сессии
description: Собрать статистику пользовательской сессии
keywords: Oracle Database, Собрать статистику пользовательской сессии
permalink: /database/performance/collect-session-statistics/
---

# Собрать статистику пользовательской сессии:

Т.е. получить максимально полный отчет по тому, какие действия проводились пользователем и каким образом на эти действия реагировала база.

Показать текущие сессии

```sql
select t.SID, t.SERIAL#, t.osuser as "User", t.MACHINE as "Computer", t.PROGRAM as "Program"
from v$session t
--where (NLS_LOWER(t.PROGRAM) = 'myprogram.exe') -- посмотреть сессии от программы myprogram.exe
--where status='ACTIVE' and osuser!='SYSTEM' -- посмотреть пользовательские сессии
order by 4 asc;
```

Включить трассировку

```sql
begin
dbms_system.set_sql_trace_in_session(sid => 139 , serial# => 40063, sql_trace => true);
end;
```

Выключить трассировку

```sql
begin
dbms_system.set_sql_trace_in_session(sid => 139 , serial# => 40063, sql_trace => false);
end;
```

Преобразовать трассировочный файл в понятный для человека вид.

```sql
CMD> tkprof filename.trc filename.txt
```
