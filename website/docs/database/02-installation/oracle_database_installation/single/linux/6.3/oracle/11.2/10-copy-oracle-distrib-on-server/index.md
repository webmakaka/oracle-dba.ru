---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /oracle_database_installation/linux/6.3/oracle/11.2/copy-oracle-distrib-on-server/
---

# <a href="/oracle_database_installation/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>:  Копирование дистрибутивов базы данных на сервер (в каталог /tmp)


Необходимо скопировать следующие архивы на сервер в каталог /tmp:

	p10404530_112030_Linux-x86-64_1of7.zip
	p10404530_112030_Linux-x86-64_2of7.zip

Для инсталляции базы данных достаточно первых 2-х архивов из 7.

Если архивы, лежат на сервере с операционной системой linux, можно воспользоваться утилитой  scp.

Например, следующей командой можно забрать дистрибутивы базы данных с другого сервера linux и положить их в каталог /tmp:

	# scp marley@192.168.1.5:/oracle/p10404530_112030_Linux-x86-64_{1..2}of7.zip /tmp/

Если Вы работаете под Windows, самый простой способ - воспользоваться winscp.


Далее нужно назначить владельцем скачанных архивов пользователя oracle11

	# chown -R oracle11:oinstall /tmp/p10404530_112030_Linux-x86-64_*
