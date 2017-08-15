---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Копирование дистрибутивов базы данных на сервер
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/copy-oracle-distrib-on-server/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Копирование дистрибутивов базы данных на сервер (в каталог /tmp)


<br/>

Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle12


Скопируйте дистрибутивы во временный каталог /distrib/oracle/12.2/

	$ cd /distrib/oracle/12.2/

<br/>

	$ ls
	linuxx64_12201_database.zip

Разархивируем DataBase

	$ unzip linuxx64_12201_database.zip

Удаляю архив

	$ rm linuxx64_12201_database.zip

<br/>

### OFFTOPIC

Самый простой способ скопировать файлы в linux - подключиться к серверу по протоколу sftp://192.168.56.101

Вы можете также воспользоваться утилитой scp. Например, следующей командой можно забрать дистрибутивы базы данных с другого сервера linux и положить их в каталог /tmp/oracle/12.2/:

	# scp marley@192.168.1.5:/oracle/linuxx64_12201_database.zip /tmp/oracle/12.2/

<br/>

Если Вы работаете под Windows, самый простой способ - воспользоваться winscp.

<br/>

Если нужно назначить владельцем скачанных архивов пользователя oracle12

	# chown -R oracle12:oinstall /tmp/linuxamd64_12c_database_*.zip
