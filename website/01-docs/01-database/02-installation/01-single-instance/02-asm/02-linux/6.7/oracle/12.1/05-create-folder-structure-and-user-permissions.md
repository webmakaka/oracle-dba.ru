---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Создание структуры каталогов и назначение необходимых прав
description: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Создание структуры каталогов и назначение необходимых прав
keywords: Oracle DataBase 12.1, Centos 6.7, ASM, GRID
permalink: /database/installation/single/asm/linux/6.7/oracle/12.1/create-folder-structure-and-user-permissions/
---

# <a href="/database/installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Создание структуры каталогов и назначение необходимых прав

    # mkdir -p /u01/oracle/database/12.1
    # mkdir -p /u01/oracle/grid/12.1

    # chown -R oracle12:oinstall /u01/oracle
    # chmod -R 775 /u01/oracle

    # mkdir -p /u01/oraInventory
    # chown -R oracle12:oinstall /u01/oraInventory
    # chmod -R 775 /u01/oraInventory
