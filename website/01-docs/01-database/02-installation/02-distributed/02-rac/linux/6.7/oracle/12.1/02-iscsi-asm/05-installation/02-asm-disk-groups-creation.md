---
layout: page
title: Создание дисковых групп ASM
permalink: /database/installation/single/asm/linux/6.7/oracle/12.1/asm-disk-groups-creation/
---

# [Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM)]: Создание ASM дисковых групп

Для запуска консоли для работы с ASM дисками, выполните команду (если нужно)

    $ asmca

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/02-asm-disks-group-creation/asm-disks-group-creation_01.png" border="0" alt="Создание дисковых групп ASM"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/02-asm-disks-group-creation/asm-disks-group-creation_02.png" border="0" alt="Создание дисковых групп ASM"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/02-asm-disks-group-creation/asm-disks-group-creation_03.png" border="0" alt="Создание дисковых групп ASM"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/02-asm-disks-group-creation/asm-disks-group-creation_04.png" border="0" alt="Создание дисковых групп ASM"><br/><br/>

Да я согласен, что для OCR выделнно слишком уж много ресурсов. Реально нужно что-то приблизительно 3 по 300 MB.

Просто получить какую-то информацию о дисковых группах

    $ asmcmd

    ASMCMD> ls
