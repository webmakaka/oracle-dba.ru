---
layout: page
title: Инсталляция Oracle DataBase 12.2 в Oracle Linux 7.4 - Запретить удаленное подключение к серверу баз данных пользователем root
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Запретить удаленное подключение к серверу баз данных пользователем root
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, запрет root
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-restrict-root-access/
---

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Запретить удаленное подключение к серверу баз данных пользователем root

<br/>

Запрет входа root по SSH

    # vi /etc/ssh/sshd_config

Нужно

    #PermitRootLogin yes

заменить на

    PermitRootLogin no

<br/>

    # /bin/systemctl restart sshd.service
