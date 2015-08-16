---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/secure-shell-between-nodes/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Настройка Secure Shell между узлами кластера


<br/>

Необходимо, чтобы узлы кластера могли обмениваться между собой по протоколу ssh.
Когда устанавливается Oracle RAC, он устанавливается только на первую ноду,
на все стальные он просто копируется.


### Настраиваем secure shell (ssh)

node1

	# su - oracle11

<br/>

	$ mkdir ~/.ssh
	$ chmod 700 ~/.ssh



Создаем RSA-type public и private encryption keys. (На все вопросы просто жмем Enter)

	$ /usr/bin/ssh-keygen -t rsa

Создаем DSA-type public и private encryption keys.  (На все вопросы жмем Enter)

	$ /usr/bin/ssh-keygen -t dsa

<br/>

	$ cd .ssh/


Добавляем полученные ключи в файл authorized key.

	$ cat id_rsa.pub >>authorized_keys
	$ cat id_dsa.pub >>authorized_keys

<br/>

	$ ssh node2 mkdir /home/oracle11/.ssh/

<br/>

	$ scp authorized_keys node2:/home/oracle11/.ssh

<br/>

	$ ssh node2

Повторяем процедуру генерации

	$ /usr/bin/ssh-keygen -t rsa
	$ /usr/bin/ssh-keygen -t dsa

<br/>


	$ cd ~/.ssh
	$ cat id_rsa.pub >> authorized_keys
	$ cat id_dsa.pub >> authorized_keys

<br/>

	$ chmod 644 authorized_keys

<br/>

	$ scp authorized_keys node1:/home/oracle11/.ssh

<br/>

	$ ssh node1

<br/>

	$ exec /usr/bin/ssh-agent $SHELL
	$ /usr/bin/ssh-add


Проверяем, что все работает нормально. Необходимо постараться пройти все возможные варианты подключений между узлами без ввода учетных записей.

	$ ssh node1 date
	$ ssh node2 date

<br/>

	$ ssh node1.localdomain date
	$ ssh node2.localdomain date

<br/>

	$ ssh node2

<br/>

	$ ssh node1 date
	$ ssh node2 date

<br/>

	$ ssh node1.localdomain date
	$ ssh node2.localdomain date
