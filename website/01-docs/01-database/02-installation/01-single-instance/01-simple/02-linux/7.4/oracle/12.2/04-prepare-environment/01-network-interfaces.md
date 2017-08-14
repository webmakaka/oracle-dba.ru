---
layout: page
title: Oracle DataBase 12c - Linux - Настройка сетевых интерфейсов
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/network-interfaces/
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
    # cp ifcfg-enp0s3 ifcfg-enp0s3.orig
    # cp ifcfg-enp0s8 ifcfg-enp0s8.orig


в

    # vi ifcfg-enp0s3
    # vi ifcfg-enp0s8

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

    # yum install -y net-tools

<br/>

    # ifconfig enp0s3
    возвращает, что IP у меня 192.168.56.101

<br/>


Далее подключаюсь уже к серверу по SSH и работаю с ним удаленно:

    $ ssh root@192.168.56.101


















-------------------------------------------------------------------------



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


    # hostnamectl set-hostname oracle12serv.localdomain

Проверка:

    # hostnamectl


<!-- <br/>

    # vi /etc/resolv.conf

<br/>

добавить:

    nameserver 192.168.56.1 -->


<br/>

    # vi /etc/hosts

<br/>

Добавляю:

    ## Localdomain and Localhost (hosts file, DNS)
    127.0.0.1 localhost.localdomain localhost

    ## IPs Public Network (hosts file, DNS)
    192.168.56.101 oracle12serv.localdomain oracle12serv



<br/>

### Разрешаю подключиться к портам

    # firewall-cmd --permanent --add-port=1521/tcp
    # firewall-cmd --permanent --add-port=5500/tcp
    # firewall-cmd --reload