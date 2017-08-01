---
layout: page
title: Oracle DataBase 12c - Linux - Настройка сетевых интерфейсов
permalink: /database/installation/single-instance/simple/linux/7.3/oracle/12.2/network-interfaces/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Настройка сетевых интерфейсов



### Настраиваем сетевые интерфейсы и параметры работы сетевых служб.


<br/>

    # cd /etc/sysconfig/network-scripts/
    # vi ifcfg-enp0s3

<br/>

В последней строке заменил

ONBOOT=no

на

ONBOOT="yes"

И перестартовал сетевой сервис

    # service network restart

<br/>

    # ping ya.ru (OK)

<br/>

Нет утилит для работы с сетью. Ставлю.

    # yum install -y iputils-ping net-tools

<br/>

    # cd /etc/sysconfig/network-scripts/
    # cp ifcfg-enp0s3 ifcfg-enp0s3.orig


<br/>

    # vi ifcfg-enp0s3

    DEVICE="eth0"
    ONBOOT="yes"
    BOOTPROTO="static"
    IPADDR=192.168.1.11
    NETMASK=255.255.255.0
    GATEWAY=192.168.1.1


<br/><br/>

Если вы подключились к серверу по RDP, я бы рекомендовал после ввода настроек сетевого интерфейса, перестартовать службу network и подключиться к серверу по ssh. И дальнейшие команды выполнять командами copy + paste.

<br/>

Перестартовать службы отвечающую за параметры сетевых интерфейсов, можно с помощью команды:


    # service network restart



<br/>
Подключиться к серверу можно командой
<br/>

    $ ssh root@192.168.1.11

<br/>

### Продолжаем настраивать параметры сетевого окружения

Необходимо выбрать подходящее имя для сервера, которое бы отражало его роль и назначение в сети.

Для этого, с помощью редактора (например, vi) отредактируйте файл /etc/sysconfig/network

<br/><br/>

Не рекомендуется в hostname использовать знак нижнего подчеркивания (_).(Enterprise Manager и другие web приложения не смогут подключиться к базе по http/https)


    # vi /etc/sysconfig/network

<br/>

    NETWORKING=yes
    NETWORKING_IPV6=no
    HOSTNAME=oracle12serv.localdomain


<br/>

    # vi /etc/resolv.conf

<br/>


    nameserver 192.168.1.1


<br/>

    # vi /etc/hosts

<br/>


    ## Localdomain and Localhost (hosts file, DNS)
    127.0.0.1 localhost.localdomain localhost

    ## IPs Public Network (hosts file, DNS)
    192.168.1.11 oracle12serv.localdomain oracle12serv


Проверяем правильно ли все работает.

    # ping google.com
