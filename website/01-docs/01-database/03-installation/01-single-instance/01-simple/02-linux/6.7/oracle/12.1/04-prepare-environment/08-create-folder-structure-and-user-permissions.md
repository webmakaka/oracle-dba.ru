---
layout: page
title: Инсталляция Oracle DataBase 12c в Oracle Linux 6.7 - Создание структуры каталогов и назначение необходимых прав
description: Инсталляция Oracle DataBase 12c в операционной системе Oracle Linux 6.7 - Создание структуры каталогов и назначение необходимых прав
keywords: Oracle DataBase 12c, Oracle Linux 6.7, Создание структуры каталогов и назначение необходимых прав
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/create-folder-structure-and-user-permissions/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Создание структуры каталогов и назначение необходимых прав

    # mkdir -p /u01/oracle/database/12.1
    # chown -R oracle12:dba /u01/oracle
    # chmod -R 775 /u01/oracle/database/12.1

    # mkdir -p /u01/oraInventory
    # chown -R oracle12:oinstall /u01/oraInventory
    # chmod -R 775 /u01/oraInventory

    # mkdir -p /u02/oracle/oradata/12.1
    # chown -R oracle12:dba /u02/oracle/oradata/12.1
    # chmod -R 775 /u02/oracle/oradata/12.1

    # mkdir -p /u03/oracle/oradata/12.1/orcl12/backups
    # chown -R oracle12:dba /u03/oracle/oradata/12.1/orcl12/
    # chmod -R 775 /u03/oracle/oradata/12.1/orcl12/
