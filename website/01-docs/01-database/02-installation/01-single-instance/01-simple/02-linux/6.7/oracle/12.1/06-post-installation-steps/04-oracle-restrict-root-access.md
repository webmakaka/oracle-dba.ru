---
layout: page
title: Инсталляция Oracle DataBase 12c в Oracle Linux 6.7 - Запретить удаленное подключение к серверу баз данных пользователем root
description: Инсталляция Oracle DataBase 12c в операционной системе Oracle Linux 6.7 - Запретить удаленное подключение к серверу баз данных пользователем root
keywords: Oracle DataBase 12c, Oracle Linux 6.7, Запретить удаленное подключение к серверу
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/oracle-restrict-root-access/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Запретить удаленное подключение к серверу баз данных пользователем root

Запрет входа root по SSH

    # vi /etc/ssh/sshd_config

Нужно

    #PermitRootLogin yes

заменить на

    PermitRootLogin no

<br/>

    # service sshd restart
