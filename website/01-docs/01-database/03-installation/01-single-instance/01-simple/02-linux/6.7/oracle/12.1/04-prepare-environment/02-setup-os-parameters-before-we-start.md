---
layout: page
title: Инсталляция Oracle DataBase 12c в Oracle Linux 6.7 - Установка параметров ОС перед стартом
description: Инсталляция Oracle DataBase 12c в операционной системе Oracle Linux 6.7 - Установка параметров ОС перед стартом
keywords: Oracle DataBase 12c, Oracle Linux 6.7, Установка параметров ОС перед стартом
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/setup-os-parameters-before-we-start/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Установка параметров ОС перед стартом

Некоторые комментарии к следующей команде. Создаю резервную копию файла /etc/selinux/config, и меняю значение парамета SELINUX с enforcing на disabled

    # sed -i.bkp.$(date +%Y-%m-%d) -e "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config

Далее, делаю резервную копию и меняю значение timeout с 5 на 0, чтобы при старте операционная система не ждала лишние 5 секунд.

    # sed -i.bkp.$(date +%Y-%m-%d) -e "s/timeout=5/timeout=0/g" /boot/grub/grub.conf

Выключаю firewall

    # service iptables stop

Запрещаю firewall запускаться при старте операционной системы

    # chkconfig iptables off
