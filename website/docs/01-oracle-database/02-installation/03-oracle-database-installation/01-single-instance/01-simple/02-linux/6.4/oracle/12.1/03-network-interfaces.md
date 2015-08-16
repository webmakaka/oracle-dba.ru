---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/network-interfaces/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Настройка сетевых интерфейсов



### Настраиваем сетевые интерфейсы и параметры работы сетевых служб.

<br/>

    # vi /etc/sysconfig/network-scripts/ifcfg-eth0

<br/>

    DEVICE="eth0"
    ONBOOT="yes"
    BOOTPROTO="static"
    IPADDR=192.168.1.10
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

    $ ssh root@192.168.1.10






<br/><br/>
<h3>Продолжаем настраивать параметры сетевого окружения</h3>
<br/>

Необходимо выбрать подходящее имя для сервера, которое бы отражало его роль и назначение в сети.


Для этого, с помощью редактора (например, vi) отредактируйте файл /etc/sysconfig/network

<br/><br/>

Не рекомендуется в hostname использовать знак нижнего подчеркивания (_).(Enterprise Manager и другие web приложения не смогут подключиться к базе по http/https)


    # vi /etc/sysconfig/network

<br/>

    NETWORKING=yes
    NETWORKING_IPV6=no
    HOSTNAME=oracleserv.localdomain


<br/>

    # vi /etc/resolv.conf

<br/>


    nameserver 192.168.1.1
    nameserver 127.0.0.1
    search localdomain

    options attempts: 2
    options timeout: 1


<br/>

    # vi /etc/hosts

<br/>


    ## Localdomain and Localhost (hosts file, DNS)
    127.0.0.1 localhost.localdomain localhost
    ::1            localhost6.localdomain6 localhost6

    ## IPs Public Network (hosts file, DNS)
    192.168.1.10 oracleserv.localdomain oracleserv



Проверяем правильно ли все работает.

    # ping ya.ru
