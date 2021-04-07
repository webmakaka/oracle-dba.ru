---
layout: page
title: Инсталляция Oracle DataBase 12.2 в Oracle Linux 7.4 - Настройка сервисов отвечающих за синхронизацию времени
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Настройка сервисов отвечающих за синхронизацию времени
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, Синхронизация времени
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/setup-actual-time/
---

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Настройка сервисов отвечающих за синхронизацию времени

<br/>

    # systemctl start ntpd
    # systemctl enable ntpd
    # systemctl status ntpd

<br/>

При необходимости разрешить на фаерволе

    # firewall-cmd --add-service=ntp --permanent
    # firewall-cmd --reload

<br/>

Проверка

    # ntpq -p
    # date -R
