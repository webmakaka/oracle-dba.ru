---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Предварительные настройки
description: Oracle RAC 12.1 SHARED FILE SYSTEM - Предварительные настройки
keywords: Oracle DataBase 12.1, Oracle Linux 6.7, RAC, SHARED FILE SYSTEM
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/setup-os-parameters-before-begin/
---

# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Предварительные настройки

<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2, storage, dnsserv</strong></span></td>
</tr>

</table>

<br/>

Некоторые комментарии к следующим 2 командам - 1 создает резервную копию файла /etc/selinux/config, а вторая заменяет значение парамета SELINUX с enforcing на disabled

    # cp /etc/selinux/config /etc/selinux/config.bkp
    # sed -i.gres "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config

Следующие 2 команды - 1 создает резервную копию файла, меняет значение timeout с 5 на 0

    # cp /etc/grub.conf /etc/grub.conf.bkp
    # sed -i.gres "s/timeout=5/timeout=0/g" /etc/grub.conf

Выключаю firewall

    # service iptables stop

Запрещаю firewall запускаться при старте операционной системы

    # chkconfig iptables off
