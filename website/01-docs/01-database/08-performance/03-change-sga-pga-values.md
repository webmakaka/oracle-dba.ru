---
layout: page
title: Изменить параметы SGA и PGA
description: Изменить параметы SGA и PGA
keywords: Oracle Database, Изменить параметы SGA и PGA
permalink: /database/performance/change-sga-pga-values/
---

# Изменить параметы SGA и PGA (Oracle 11.2)

<br/>

Делалось в 2011

<br/>

1. Шаг

```
SQL> show paramteter sga;
SQL> show parameter pga;
```

Чтобы узнать, использовался при старте PFILE или SPFILE, выполните запрос:

<br/>

```sql
SELECT DECODE(value, NULL, 'PFILE', 'SPFILE') "Init File Type"
FROM sys.v_$parameter WHERE name = 'spfile';
```

<br/>

```sql
SQL> alter system set sga_target = 500m scope=both;
SQL> alter system set pga_aggregate_target = 150m scope=both;
SQL> shutdown immediate;
SQL> startup;
```

<br/>

2. Шаг

<br/>

Теперь мне нужно уменьшить размер sga,<br/>
При выполнении команд выше, размер остается прежним.

<br/>

Пробуем:

```sql
$ sqlplus / as sysdba
SQL> CREATE PFILE='/u02/oradata/ora112/pfile_myLastName_30_11_2011.ora' FROM SPFILE;
SQL> quit
```

<br/>

```
cp /u02/oradata/ora112/pfile_myLastName_30_11_2011.ora /u02/oradata/ora112/pfile_myLastName_30_11_2011.ora.bkp
vi /u02/oradata/ora112/pfile_myLastName_30_11_2011.ora
```

<br/>

```
ora112.__db_cache_size=276824064
ora112.__java_pool_size=4194304
ora112.__large_pool_size=4194304
ora112.__oracle_base='/u01/app/oracle'#ORACLE_BASE set from environment
ora112.__pga_aggregate_target=314572800
ora112.__sga_target=524288000
ora112.__shared_io_pool_size=0
ora112.__shared_pool_size=222298112
ora112.__streams_pool_size=8388608
*.audit_file_dest='/u01/app/oracle/admin/ora112/adump'
*.audit_trail='db'
*.compatible='11.2.0.0.0'
*.control_files='/u02/oradata/ora112/control01.ctl','/u02/oradata/ora112/control03.ctl','/u01/app/oracle/fast_recovery_area/ora112/control02.ctl'
*.db_block_size=8192
*.db_domain=''
*.db_name='ora112'
*.db_recovery_file_dest='/u01/app/oracle/fast_recovery_area'
*.db_recovery_file_dest_size=32212254720
*.diagnostic_dest='/u01/app/oracle'
*.dispatchers='(PROTOCOL=TCP) (SERVICE=ora112XDB)'
*.memory_target=838860800
*.open_cursors=300
*.pga_aggregate_target=157286400
*.processes=150
*.remote_login_passwordfile='EXCLUSIVE'
*.sga_target=524288000
*.star_transformation_enabled='TRUE'
*.undo_tablespace='UNDOTBS1'
```

<br/>

```
НЕ ПОМНЮ МОЖНО ТАК ДЕЛАТЬ ИЛИ НЕТ.
ДЕЛАЮ НА ТЕСТОВОЙ МАШИНЕ!!!
```

<br/>

```
*.audit_file_dest='/u01/app/oracle/admin/ora112/adump'
*.audit_trail='db'
*.compatible='11.2.0.0.0'
*.control_files='/u02/oradata/ora112/control01.ctl','/u02/oradata/ora112/control03.ctl','/u01/app/oracle/fast_recovery_area/ora112/control02.ctl'
*.db_block_size=8192
*.db_domain=''
*.db_name='ora112'
*.db_recovery_file_dest='/u01/app/oracle/fast_recovery_area'
*.db_recovery_file_dest_size=32212254720
*.diagnostic_dest='/u01/app/oracle'
*.dispatchers='(PROTOCOL=TCP) (SERVICE=ora112XDB)'
*.memory_target=500M
*.open_cursors=300
*.pga_aggregate_target=100M
*.processes=150
*.remote_login_passwordfile='EXCLUSIVE'
*.sga_target=400M
*.star_transformation_enabled='TRUE'
*.undo_tablespace='UNDOTBS1'
```

<br/>

```sql
$ sqlplus / as sysdba
SQL> shutdown immediate;
SQL> STARTUP PFILE=/u02/oradata/ora112/pfile_myLastName_30_11_2011.ora
SQL> create spfile from memory;
SQL> shutdown immediate;
SQL> startup
```
