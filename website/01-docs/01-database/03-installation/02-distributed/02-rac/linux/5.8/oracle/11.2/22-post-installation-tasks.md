---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 (ISCSI + ASM) - После инсталляции
description: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 (ISCSI + ASM) - После инсталляции
keywords: database, installation, distributed, rac, linux, 5.8, oracle, 11.2, После инсталляции
permalink: /database/installation/distributed/rac/linux/5.8/oracle/11.2/post-installation-tasks/
---

# <a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: После инсталляции

<br/>

1.

node1

    $ vi /etc/oratab

Заменить:

+ASM1:/u01/app/grid/11.2:N
racnode:/u01/app/oracle/product/database/11.2:N

на

+ASM1:/u01/app/grid/11.2:Y
racnode:/u01/app/oracle/product/database/11.2:Y

<br/>

node2

    $ vi /etc/oratab

Заменить:

+ASM2:/u01/app/grid/11.2:N
racnode:/u01/app/oracle/product/database/11.2:N

на

+ASM2:/u01/app/grid/11.2:Y
racnode:/u01/app/oracle/product/database/11.2:Y

2. Убедитесь, что удается подключиться к узлам кластера командой sqlplus
   Если нет,

Покажет какие процессы запущены.

    ps -eaf | grep ora*

Из этого можно будет понять какое имя у экземпляра.

Откорректируйте

    vi /home/oracle11/.bash_profile

<br/>

    export ORACLE_SID=racnode1
    export ORACLE_UNQNAME=racnode1
