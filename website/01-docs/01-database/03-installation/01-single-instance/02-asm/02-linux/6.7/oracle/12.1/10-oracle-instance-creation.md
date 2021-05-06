---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Создание экземпляра базы данных (Instance)
description: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Создание экземпляра базы данных (Instance)
keywords: Oracle DataBase 12.1, Centos 6.7, ASM, GRID
permalink: /database/installation/single/asm/linux/6.7/oracle/12.1/oracle-instance-creation/
---

# <a href="/database/installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Создание экземпляра базы данных (Instance)

Определите системную переменную DISPLAY следующим образом (если она не поределена).

    $ export DISPLAY=192.168.1.5:0.0


    $ dbca

<img src="https://img.oracledba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_01.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="https://img.oracledba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_02.png" border="0" alt="oracle database software installation"><br/><br/>

<br/><br/>

В режиме Advanced, можно более оптимально настроить параметры. Исключить из установки лишнее. Например, JVM, Enterprise Manager, Multimedia. Можно выделить побольше ресурсов памяти и д.р.

<a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/oracle-instance-creation/">Посмотреть можно здесь</a>

<br/><br/>

<img src="https://img.oracledba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_03.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="https://img.oracledba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_04.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="https://img.oracledba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_05.png" border="0" alt="oracle database software installation"><br/><br/>

<img src="https://img.oracledba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/04-oracle-instance-creation/oracle-instance-creation_06.png" border="0" alt="oracle database software installation"><br/><br/>

<br/>
<br/>

Узнать порт подключения к EM:

    SQL> select dbms_xdb_config.gethttpsport() from dual;

    DBMS_XDB_CONFIG.GETHTTPSPORT()
    ------------------------------
    			  5500

Можно подключиться к EM:  
https://192.168.1.11:5500/em/

<br/>

### После инсталляционные шаги

    $ vi /etc/oratab

<br/>

    +ASM:/u01/oracle/grid/12.1:N
    orcl12:/u01/oracle/database/12.1:N

меняю на

    +ASM:/u01/oracle/grid/12.1:Y
    orcl12:/u01/oracle/database/12.1:Y

<br/>

    SQL> select name, total_mb, free_mb from v$asm_diskgroup;

    NAME				 TOTAL_MB    FREE_MB
    ------------------------------ ---------- ----------
    DATA				   163836     159704
    ARCH				    81918      81452
