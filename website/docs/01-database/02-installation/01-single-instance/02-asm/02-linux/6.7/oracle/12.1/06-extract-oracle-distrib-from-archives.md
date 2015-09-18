---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Извлечение дистрибутивов базы Oracle из архивов
permalink: /docs/oracle-database/installation/oracle-database-installation/single/asm/linux/6.7/oracle/12.1/extract-oracle-distrib-from-archives/
---


# <a href="/docs/oracle-database/installation/oracle-database-installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>:  Извлечение дистрибутивов базы Oracle из архивов




Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle12


Скопируйте дистрибутивы во временный каталог /tmp/oracle/12.1/

	$ cd /tmp/oracle/12.1/

<br/>

	$ ls
	linuxamd64_12102_database_1of2.zip  linuxamd64_12102_grid_1of2.zip
	linuxamd64_12102_database_2of2.zip  linuxamd64_12102_grid_2of2.zip


<br/>

	$ unzip linuxamd64_12102_grid_1of2.zip; unzip linuxamd64_12102_grid_2of2.zip
	$ unzip linuxamd64_12102_database_1of2.zip; unzip linuxamd64_12102_database_2of2.zip
