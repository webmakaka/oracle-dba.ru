---
layout: page
title:  Настройка параметров Instance после создания дупликата на standby
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-on-standby/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Настройка параметров Instance после создания дупликата на standby




### STANDBY


    SQL> alter system set LOG_ARCHIVE_CONFIG="DG_CONFIG=(master, slave)" scope=both;


Сам я хрен знает сколько времени сидел из-за того, что неправильно указывал SERVICE. Вообщем значение SERVICE из tnanames.ora. Я же ставил в поле SERVICE - db_unique_name.

    SQL> alter system set log_archive_dest_2="SERVICE=primary LGWR SYNC VALID_FOR=(ONLINE_LOGFILES,PRIMARY_ROLE) db_unique_name=master" scope=both;

<br/>

    SQL> alter system set log_archive_dest_state_2="enable" scope=both;

<br/>

    SQL> alter system set standby_file_management= AUTO scope=both;

<br/>

    SQL> alter system set FAL_SERVER="master" scope=both;
    SQL> alter system set FAL_CLIENT="slave" scope=both;
