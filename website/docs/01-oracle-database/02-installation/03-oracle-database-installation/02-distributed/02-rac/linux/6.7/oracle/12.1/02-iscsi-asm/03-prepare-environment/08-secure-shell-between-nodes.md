---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Настройка Secure Shell между узлами кластера
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/secure-shell-between-nodes/
---

# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Настройка Secure Shell между узлами кластера


<br/>

Необходимо, чтобы узлы кластера могли обмениваться между собой по протоколу ssh.
Когда устанавливается Oracle RAC, он устанавливается только на первую ноду,
на все стальные он просто копируется.


### Настраиваем secure shell (ssh)


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">


<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
</tr>

</table>

	# su - oracle12

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

	$ ssh rac2 mkdir /home/oracle12/.ssh/

<br/>

	$ scp authorized_keys rac2:/home/oracle12/.ssh

<br/>

	$ ssh rac2

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

	$ scp authorized_keys rac1:/home/oracle12/.ssh

<br/>

	$ ssh rac1

<br/>

	$ exec /usr/bin/ssh-agent $SHELL
	$ /usr/bin/ssh-add


Проверяем, что все работает нормально. Необходимо постараться пройти все возможные варианты подключений между узлами без ввода учетных записей.

	$ ssh rac1 date
	$ ssh rac2 date

<br/>

	$ ssh rac1.localdomain date
	$ ssh rac2.localdomain date

<br/>

	$ ssh rac2

<br/>

	$ ssh rac1 date
	$ ssh rac2 date

<br/>

	$ ssh rac1.localdomain date
	$ ssh rac2.localdomain date

<br/>

	$ ssh rac1
