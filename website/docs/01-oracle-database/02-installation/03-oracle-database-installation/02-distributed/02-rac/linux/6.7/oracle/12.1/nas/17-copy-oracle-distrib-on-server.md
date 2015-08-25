---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/copy-oracle-distrib-on-server/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Копирование дистрибутивов базы данных на сервер


<br/>


Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle12


Копирую дистрибутивы во временный каталог /tmp/oracle/12.1/

	$ cd /tmp/oracle/12.1/

<br/>

	$ ls
	linuxamd64_12102_database_1of2.zip  linuxamd64_12102_grid_1of2.zip
	linuxamd64_12102_database_2of2.zip  linuxamd64_12102_grid_2of2.zip


<br/>

	$ unzip linuxamd64_12102_grid_1of2.zip; unzip linuxamd64_12102_grid_2of2.zip
	$ unzip linuxamd64_12102_database_1of2.zip; unzip linuxamd64_12102_database_2of2.zip
