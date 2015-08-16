---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/setup-os-parameters-before-begin/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Предварительные настройки

<br/>

Следующие команды выполняются на всех виртаульных машинах

Некоторые комментарии к следующим 2 командам - 1 создает резервную копию файла /etc/selinux/config, а вторая заменяет значение парамета SELINUX с enforcing на disabled

    # cp /etc/selinux/config /etc/selinux/config.bkp
    # sed -i.gres "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config

Следующие 2 команды -  1 создает резервную копию файла, меняет значение timeout с 5 на 0

    # cp /etc/grub.conf /etc/grub.conf.bkp
    # sed -i.gres "s/timeout=5/timeout=0/g" /etc/grub.conf


Выключаю firewall

    # service iptables stop

Запрещаю firewall запускаться при старте операционной системы

    # chkconfig iptables off
