---
layout: page
title: Собрать статистику пользовательской сессии
permalink: /docs/architecture/performance/session_statistic/
---



<h2>Собрать статистику пользовательской сессии:</h2>


Т.е. получить максимально полный отчет по тому, какие действия проводились пользователем и каким образом на эти действия реагировала база.


Показать текущие сессии

    select t.SID, t.SERIAL#, t.osuser as "User", t.MACHINE as "Computer", t.PROGRAM as "Program"
    from v$session t
    --where (NLS_LOWER(t.PROGRAM) = 'myprogram.exe') -- посмотреть сессии от программы myprogram.exe
    --where status='ACTIVE' and osuser!='SYSTEM' -- посмотреть пользовательские сессии
    order by 4 asc;


Включить трассировку

    begin
    dbms_system.set_sql_trace_in_session(sid => 139 , serial# => 40063, sql_trace => true);
    end;


Выключить трассировку

    begin
    dbms_system.set_sql_trace_in_session(sid => 139 , serial# => 40063, sql_trace => false);
    end;



Преобразовать трассировочный файл в понятный для человека вид.

    CMD> tkprof filename.trc filename.txt
