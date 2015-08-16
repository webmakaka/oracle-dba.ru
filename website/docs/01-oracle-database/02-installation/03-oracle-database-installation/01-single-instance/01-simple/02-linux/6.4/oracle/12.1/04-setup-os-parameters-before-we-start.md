---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/setup-os-parameters-before-we-start/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Установка параметров ОС перед стартом


Некоторые комментарии к следующей команде. Создаю резервную копию файла /etc/selinux/config, и меняю значение парамета SELINUX с enforcing на disabled


    # sed -i.bkp -e "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config


Далее, делаю резервную копию и меняю значение timeout с 5 на 0, чтобы при старте операционная система не ждала лишние 5 секунд.

    # sed -i.bkp -e "s/timeout=5/timeout=0/g" /boot/grub/grub.conf


Выключаю firewall

    # service iptables stop


Запрещаю firewall запускаться при старте операционной системы

    # chkconfig iptables off
