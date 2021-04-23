---
layout: page
title: Некоторые запросы к базе данных Oracle
description: Некоторые запросы к базе данных Oracle
keywords: Oracle Database, Некоторые запросы к базе данных Oracle
permalink: /docs/architecture/queries/query/
---

# Некоторые запросы к базе данных Oracle:

<br/>

// Какие компоненты установлены:

    SQL> select comp_id, comp_name, version, status from dba_registry;

<br/>

// Tracking Oracle Option Usage (Какие опции Oracle DataBase использовались):

    select samp.dbid, fu.name, samp.version, detected_usages, total_samples,
      decode(to_char(last_usage_date, 'MM/DD/YYYY, HH:MI:SS'),
             NULL, 'FALSE',
             to_char(last_sample_date, 'MM/DD/YYYY, HH:MI:SS'), 'TRUE',
             'FALSE')
      currently_used, first_usage_date, last_usage_date, aux_count,
      feature_info, last_sample_date, last_sample_period,
      sample_interval, mt.description
     from wri$_dbu_usage_sample samp, wri$_dbu_feature_usage fu,
          wri$_dbu_feature_metadata mt
     where
      samp.dbid    = fu.dbid and
      samp.version = fu.version and
      fu.name      = mt.name and
      fu.name not like '_DBFUS_TEST%' and  /* filter out test features */
      bitand(mt.usg_det_method, 4) != 4    /* filter out disabled features */
    /

http://www.remote-dba.net/oracle_10g_tuning/t_tracking_auditing_option_usage.htm

<br/>

Отключение корзины

    SQL> alter system set RECYCLEBIN=off scope=BOTH;

<br/>

Найти невалидные объекты

    SQL> select object_name, object_type from DBA_OBJECTS
    WHERE status = 'INVALID';

<br/>

Задать каталог где будут создаваться фийлы

    SQL> alter system set db_create_file_dest="/u01/datafiles";

<br/>

Посмотреть параметры

    SQL> show parameter db_create_file_dest

<br/>

Выявление пользоавтелей, наиболее интенсивно эксплуатирующих ресурсы ЦП

    SQL> SELECT n.username, s.sid, s.value
    FROM v$sesstat s, v$statname t, v$session n
    WHERE s.statistic# = t.statistic#
    AND n.sid = s.sid
    AND t.name='CPU used by this session'
    ORDER BY s.value desc;

<br/>

Создание и использование последовательностей (sequence)

    create sequence dept_seq start with 200 increment by 10;
    insert into departments valuse (dept_seq.netxval, .......)

<br/>

Показать залоченные объекты

    select * from source_locked l
    where l.object_name = 'PRINT'

<!--

//
select sa.sql_text,ss.username
from v$session ss, v$sqlarea sa
where sa.hash_value = ss.prev_hash_value;




/*
This script produces a summary of all blocking locks in the database:
blocking and waiting session summary, locked objects, and lock details
for all blocking locks in the database

Submitted by:
Last edited by: Evgeny Agafonov, 03/12/2008
*/

select
  to_char(bs.username||' ('||bs.sid||', '||bs.serial#||')') as "Blocking User (SID, Serial#)",
  to_char(ws.username||' ('||ws.sid||', '||ws.serial#||')') as "Waiting User (SID, Serial#)",
  to_char(bs.osuser||', '||bs.module||', '||bs.process) as "Blocking OS User, Program, PID",
  to_char(ws.osuser||', '||ws.module||', '||ws.process) as "Waiting OS User, Program, PID",
  bo.object_name, bo.object_type,
  decode(wl.type,
    'TX', 'Transaction',
    'TM', 'DML',
    'UL', 'User Defined',
    'System') as "LOCK_TYPE",
  decode(bl.lmode,
    0, 'None',
    1, 'Null',
    2, 'Row Shared',
    3, 'Row Exclusive',
    4, 'Share',
    5, 'Share Row Excl',
    6, 'Exclusive') as "LOCKED_MODE",
  decode(wl.request,
    0, 'None',
    1, 'Null',
    2, 'Row Shared',
    3, 'Row Exclusive',
    4, 'Share',
    5, 'Share Row Excl',
    6, 'Exclusive') as "REQUESTED_MODE"
from v$lock bl, v$session bs, v$lock wl, v$session ws,
  v$locked_object blo, dba_objects bo
where bl.sid=bs.sid and bl.sid = blo.session_id and blo.object_id = bo.object_id
  and wl.sid=ws.sid and bl.block = 1 and wl.request > 0
  and wl.id1 = bl.id1 and wl.id2 = bl.id2
order by "Blocking User (SID, Serial#)", "Waiting User (SID, Serial#)";


-->
