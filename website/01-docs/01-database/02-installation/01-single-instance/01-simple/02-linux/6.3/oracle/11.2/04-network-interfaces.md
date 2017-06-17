---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/network-interface/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Настройка сетевых интерфейсов


Необходимо выбрать подходящее имя для сервера, которое бы отражало его роль и назначение в сети.


Для этого, с помощью редактора (например, vi) отредактируйте файл /etc/sysconfig/network


Задайте параметры, согласно характеристикам Вашей сети.


Не рекомендуется в hostname использовать знак нижнего подчеркивания (_). (Enterprise Manager и другие web приложения не смогут подключиться к базе по http/https)


    # vi /etc/sysconfig/network

<br/>


    NETWORKING=yes
    NETWORKING_IPV6=no
    HOSTNAME=oracle112.localdomain


<br/>

    # vi /etc/sysconfig/network-scripts/ifcfg-eth0

<br/>

    DEVICE="eth0"
    ONBOOT="yes"
    BOOTPROTO="static"
    IPADDR=192.168.1.10
    NETMASK=255.255.255.0
    GATEWAY=192.168.1.1


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
    192.168.1.10 oracle112.localdomain oracle112


Перестартовать сетевые интерфейсы, можно с помощью следующей команды:

<br/>

    # service network restart



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
