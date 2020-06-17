---
layout: page
title: Инсталляция Oracle DataBase 11.2.0.3.2 в Oracle Linux 6.3 - Создание резервной копии созданной базы данных (холодный backup)
description: Инсталляция Oracle DataBase 11.2.0.3.2 в операционной системе Oracle Linux 6.3 - Создание резервной копии созданной базы данных (холодный backup)
keywords: Oracle DataBase 11.2, Oracle Linux 6.3, Холодный backup, Cold Backup
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-cold-backup/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Создание резервной копии созданной базы данных (холодный backup):

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> alter system set db_recovery_file_dest_size = 25G;

<br/>

    SQL> alter system set db_recovery_file_dest="/u03/orabackups/";

<br/>

    SQL> shutdown immediate;
    SQL> startup mount;
    SQL> quit

<br/>

    $ rman target /

<br/>

    RMAN> backup full database noexclude include current controlfile spfile TAG "FULL_COLD_BACKUP";

<br/>

    RMAN> sql 'alter database open';

<br/>

    // Посмотреть, какие бекапы имеются
    RMAN> list backup summary;

<br/>

    RMAN> quit

<br/><br/>
<br/><br/>

<div style="padding:10px; border:thin solid black;">

    <h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
