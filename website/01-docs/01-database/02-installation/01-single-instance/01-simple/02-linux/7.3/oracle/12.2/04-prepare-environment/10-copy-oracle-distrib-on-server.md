---
layout: page
title: Oracle DataBase 12c - Linux - Копирование дистрибутивов базы данных на сервер
permalink: /database/installation/single-instance/simple/linux/7.3/oracle/12.2/copy-oracle-distrib-on-server/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Копирование дистрибутивов базы данных на сервер (в каталог /tmp)




Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle12


Скопируйте дистрибутивы во временный каталог /tmp/oracle/12.1/

	$ cd /tmp/oracle/12.1/

<br/>

	$ ls
	linuxamd64_12102_database_1of2.zip  linuxamd64_12102_database_2of2.zip

Разархивируем DataBase

	$ unzip linuxamd64_12102_database_1of2.zip; unzip linuxamd64_12102_database_2of2.zip




<br/>

### OFFTOPIC

Самый простой способ скопировать файлы в linux - подключиться к серверу по протоколу sftp://192.168.1.11

Вы можете также воспользоваться утилитой scp. Например, следующей командой можно забрать дистрибутивы базы данных с другого сервера linux и положить их в каталог /tmp/oracle/12.1/:

	# scp marley@192.168.1.5:/oracle/linuxamd64_12c_database_*.zip /tmp/oracle/12.1/


<br/>

Если Вы работаете под Windows, самый простой способ - воспользоваться winscp.

Если нужно назначить владельцем скачанных архивов пользователя oracle12

	# chown -R oracle12:oinstall /tmp/linuxamd64_12c_database_*.zip
