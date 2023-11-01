---
layout: page
title: Некоторые запросы к базе данных Oracle
description: Некоторые запросы к базе данных Oracle
keywords: Oracle Database, Некоторые запросы к базе данных Oracle
permalink: /docs/architecture/queries/query/
---

# Некоторые запросы к базе данных Oracle:

<br/>

```sql
-- какой сегмент попадает на битые блоки
SELECT e.owner, e.segment_type, e.segment_name, e.partition_name, c.file#
     , greatest(e.block_id, c.block#) corr_start_block#
     , least(e.block_id+e.blocks-1, c.block#+c.blocks-1) corr_end_block#
     , least(e.block_id+e.blocks-1, c.block#+c.blocks-1)
       - greatest(e.block_id, c.block#) + 1 blocks_corrupted
     , null description
  FROM dba_extents e, v$database_block_corruption c
 WHERE e.file_id = c.file#
   AND e.block_id <= c.block# + c.blocks - 1
   AND e.block_id + e.blocks - 1 >= c.block#
UNION
SELECT s.owner, s.segment_type, s.segment_name, s.partition_name, c.file#
     , header_block corr_start_block#
     , header_block corr_end_block#
     , 1 blocks_corrupted
     , 'Segment Header' description
  FROM dba_segments s, v$database_block_corruption c
 WHERE s.header_file = c.file#
   AND s.header_block between c.block# and c.block# + c.blocks - 1
UNION
SELECT null owner, null segment_type, null segment_name, null partition_name, c.file#
     , greatest(f.block_id, c.block#) corr_start_block#
     , least(f.block_id+f.blocks-1, c.block#+c.blocks-1) corr_end_block#
     , least(f.block_id+f.blocks-1, c.block#+c.blocks-1)
       - greatest(f.block_id, c.block#) + 1 blocks_corrupted
     , 'Free Block' description
  FROM dba_free_space f, v$database_block_corruption c
 WHERE f.file_id = c.file#
   AND f.block_id <= c.block# + c.blocks - 1
   AND f.block_id + f.blocks - 1 >= c.block#
order by file#, corr_start_block#;
```

<br/>

https://t.me/oracle_dba_ru/49323

<br/>

```sql
-- Какие компоненты установлены
SQL> select comp_id, comp_name, version, status from dba_registry;
```

<br/>

// Какие компоненты установлены:

```sql
--  Версия БД с учетом установленных PSU.
-- 12 и 21+ версий
declare
  l_rel int;
  l_ver varchar2(30);
begin
  select  to_number(substr(version,1,instr(version,'.')-1)) into l_rel from v$instance;
  $IF DBMS_DB_VERSION.version = 11 $THEN
    select version into l_ver from v$instance;
  $ELSIF DBMS_DB_VERSION.version = 12 $THEN
    select full_ver
    into l_ver
    from (SELECT t.version||'.'||bundle_id full_ver,t.description
          FROM   dba_registry_sqlpatch t
          where  flags = 'NB'
          order by action_time desc)
    where rownum=1;
  $ELSIF DBMS_DB_VERSION.version > 12 $THEN
    select version_full into l_ver from v$instance;
  $END
  DBMS_OUTPUT.PUT_LINE( l_ver);
end;
/
```

https://t.me/oracle_dba_ru/39524

<br/>

```sql
-- Tracking Oracle Option Usage (Какие опции Oracle DataBase использовались):
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
```

http://www.remote-dba.net/oracle_10g_tuning/t_tracking_auditing_option_usage.htm

<br/>

```sql
-- Отключение корзины
SQL> alter system set RECYCLEBIN=off scope=BOTH;
```

<br/>

```sql
-- Найти невалидные объекты
SQL> select object_name, object_type from DBA_OBJECTS
WHERE status = 'INVALID';
```

<br/>

```sql
-- Задать каталог где будут создаваться файлы
SQL> alter system set db_create_file_dest="/u01/datafiles";
```

<br/>

```sql
-- Посмотреть параметры
SQL> show parameter db_create_file_dest
```

<br/>

```sql
-- Выявление пользователей, наиболее интенсивно эксплуатирующих ресурсы ЦП
SQL> SELECT n.username, s.sid, s.value
FROM v$sesstat s, v$statname t, v$session n
WHERE s.statistic# = t.statistic#
AND n.sid = s.sid
AND t.name='CPU used by this session'
ORDER BY s.value desc;
```

<br/>

```sql
-- Создание и использование последовательностей (sequence)
create sequence dept_seq start with 200 increment by 10;
insert into departments valuse (dept_seq.netxval, .......)
```

<br/>

```sql
-- Показать залоченные объекты
select * from source_locked l
where l.object_name = 'PRINT'
```

<br/>

```sql
-- Топ 10 таблиц, выросших больше всего за месяц
select *
from (select c.TABLESPACE_NAME,
c.segment_name "Object Name",
b.object_type,
sum(space_used_delta) / 1024 / 1024 "Growth(MB)"
from dba_hist_snapshot sn,
dba_hist_seg_stat a,
dba_objects b,
dba_segments c
where begin_interval_time > trunc(sysdate) - 30
and sn.snap_id = a.snap_id
and b.object_id = a.obj#
and b.owner = c.owner
and b.object_name = c.segment_name
—and c.owner = user
group by c.TABLESPACE_NAME, c.segment_name, b.object_type)
order by 4 desc;
```

<br/>

https://t.me/oracle_dba_ru/26798

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
