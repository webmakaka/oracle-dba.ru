---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Установка параметров ОС перед стартом
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/setup-os-parameters-before-we-start/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>


# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Установка параметров ОС перед стартом


Некоторые комментарии к следующей команде. Создаю резервную копию файла /etc/selinux/config, и меняю значение парамета SELINUX с enforcing на disabled


    # sed -i.bkp.$(date +%Y-%m-%d) -e "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config


<!-- Далее, делаю резервную копию и меняю значение timeout с 5 на 0, чтобы при старте операционная система не ждала лишние 5 секунд.

    # sed -i.bkp.$(date +%Y-%m-%d) -e "s/timeout=5/timeout=0/g" /boot/grub/grub.conf -->



<!-- Выключаю firewall (по умолчанию )

    # service iptables stop


Запрещаю firewall запускаться при старте операционной системы

    # chkconfig iptables off -->
