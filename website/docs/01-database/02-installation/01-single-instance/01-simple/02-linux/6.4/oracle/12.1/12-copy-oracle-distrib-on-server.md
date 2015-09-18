---
layout: page
title: Oracle DataBase 12c - Linux - Копирование дистрибутивов базы данных на сервер 
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/copy-oracle-distrib-on-server/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Копирование дистрибутивов базы данных на сервер (в каталог /tmp)



Необходимо скопировать архивы на сервер в каталог /tmp:<br/>

Самый простой способ скопировать файлы - подключиться к серверу по протоколу sftp://192.168.1.10
<br/><br/>
Вы можете также воспользоваться утилитой scp.
<br/>
Например, следующей командой можно забрать дистрибутивы базы данных с другого сервера linux и положить их в каталог /tmp:
<br/><br/>


	# scp marley@192.168.1.5:/oracle/linuxamd64_12c_database_*.zip /tmp/

Если Вы работаете под Windows, самый простой способ - воспользоваться winscp.


Далее нужно назначить владельцем скачанных архивов пользователя oracle12

	# chown -R oracle12:oinstall /tmp/linuxamd64_12c_database_*.zip
