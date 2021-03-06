---
layout: page
title: Инсталляция Oracle DataBase 11.2.0.3.2 в Oracle Linux 6.3 - Мультиплексирование redologs
description: Инсталляция Oracle DataBase 11.2.0.3.2 в операционной системе Oracle Linux 6.3 - Мультиплексирование redologs
keywords: Oracle DataBase 11.2, Oracle Linux 6.3, Мультиплексирование redologs
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-multiplex-redologs/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Мультиплексирование redologs

<br/>

    $ mkdir -p /u02/oradata/${ORACLE_SID}/redologs
    $ mkdir -p /u03/oradata/${ORACLE_SID}/redologs

<br/>

    $ sqlplus / as sysdba

Блок команд, чтобы удобнее представить на экране результаты выполнения запросов.

    SQL> set linesize 250;
    SQL> set pagesize 0;
    SQL> col  GROUP# format 99;
    SQL> col  MEMBER format a40;
    SQL> col  STATUS format a10;
    SQL> col  MB format 999;

<br/>

```sql
SQL> select a.group#, member, a.status, bytes/1024/1024 as "MB"
from v$log a, v$logfile b
where a.group# = b.group#
order by 1;
```

<br/>

    1 /u02/oradata/ora112/redo01.log           INACTIVE                         50
    2 /u02/oradata/ora112/redo02.log           INACTIVE                         50
    3 /u02/oradata/ora112/redo03.log           CURRENT                         50

Удалить можно только файлы неактивной группы. Группы можно переключать, что будет показано ниже.

Удаляем файлы группы в состоянии INACTIVE

1. Нужно пересоздать группу 1 и файлы данной группы.

Удаляем файлы группы 1

    SQL> alter database drop logfile group 1;

<br/>

    SQL> quit

<br/>

    $ rm /u02/oradata/ora112/redo01.log

<br/>

    $ sqlplus / as sysdba

Добавляем новую группу, перечисляем файлы новой группы и определяем их размер.

<br/>

```sql
SQL> alter database add logfile group 1 ('/u02/oradata/ora112/redologs/redo01.log' , '/u03/oradata/ora112/redologs/redo01.log') size 100M;
```

<br/>

2. Нужно пересоздать группу 2 и файлы данной группы.

Удаляем файлы группы 2

    SQL> alter database drop logfile group 2;

<br/>

    SQL> quit

<br/>

    $ rm /u02/oradata/ora112/redo02.log

<br/>

    $ sqlplus / as sysdba

<br/>

```sql
SQL> alter database add logfile group 2 ('/u02/oradata/ora112/redologs/redo02.log' , '/u03/oradata/ora112/redologs/redo02.log ') size 100M;
```

<br/>

3. Нужно пересоздать группу 3 и файлы данной группы.

Так как группа активна, необходимо переключиться на следующую группу файлов, сделав группу 2 INACTIVE.

Для переключения, достаточно выполнить команды:

    SQL> alter system checkpoint;
    SQL> alter system switch logfile;

Удаляем файлы группы 3

    SQL> alter database drop logfile group 3;

<br/>

    SQL> quit

<br/>

    $ rm /u02/oradata/ora112/redo03.log

<br/>

    $ sqlplus / as sysdba

<br/>

```sql
SQL> alter database add logfile group 3 ('/u02/oradata/ora112/redologs/redo03.log', '/u03/oradata/ora112/redologs/redo03.log ') size 100M;
```

<br/>

    SQL> set linesize 250;
    SQL> set pagesize 0;
    SQL> col  GROUP# format 99;
    SQL> col  MEMBER format a40;
    SQL> col  STATUS format a10;
    SQL> col  MB format 999;

<br/>

```sql
SQL> select a.group#, member, a.status, bytes/1024/1024 as "MB"
from v$log a, v$logfile b
where a.group# = b.group#
order by 1,2;
```

<br/>

     1 /u02/oradata/ora112/redologs/redo01.log  CURRENT     100
     1 /u03/oradata/ora112/redologs/redo01.log  CURRENT     100
     2 /u02/oradata/ora112/redologs/redo02.log  UNUSED      100
     2 /u03/oradata/ora112/redologs/redo02.log  UNUSED      100
     3 /u02/oradata/ora112/redologs/redo03.log  UNUSED      100
     3 /u03/oradata/ora112/redologs/redo03.log  UNUSED      100

<br/>

    SQL> quit

<br/><br/>
<br/><br/>

<div style="padding:10px; border:thin solid black;">

    <h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
