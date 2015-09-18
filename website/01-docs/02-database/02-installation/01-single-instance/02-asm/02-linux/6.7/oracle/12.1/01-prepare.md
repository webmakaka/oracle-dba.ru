---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Установка hostname и hosts
permalink: /database/installation/single/asm/linux/6.7/oracle/12.1/prepare/
---

# <a href="/database/installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Установка hostname и hosts

<br/>


	# vi /etc/hosts

<br/>

	## Localdomain and Localhost

	127.0.0.1 localhost.localdomain localhost


	## DataBases

	192.168.1.11 moscow.localdomain moscow



 Устанавливаю значение hostname для сервера

    # vi /etc/sysconfig/network

<br/>

    NETWORKING=yes
    HOSTNAME=moscow.localdomain


**После переименования, лучше перезагрузить сервер или каким-то способом применить изменения, или иначе в конфигах будет прописано что-то не то и придется их потом еще и править**
