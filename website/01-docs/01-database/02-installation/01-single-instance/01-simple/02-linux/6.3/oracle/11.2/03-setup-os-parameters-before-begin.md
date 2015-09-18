---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/12.1/setup-os-parameters-before-we-start/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/12.1/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Установка параметров ОС перед стартом



Некоторые комментарии к следующей команде. Создаем резервную копию файла /etc/selinux/config, и меняем значение парамета SELINUX с enforcing на disabled


	# sed -i.bkp -e "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config


А здесь, мы делаем резервную копию и меняем значение timeout с 5 на 0


	# sed -i.bkp -e "s/timeout=5/timeout=0/g" /boot/grub/grub.conf

Выключаю firewall

	# service iptables stop

Запрещаю firewall запускаться при старте операционной системы

	# chkconfig iptables off
