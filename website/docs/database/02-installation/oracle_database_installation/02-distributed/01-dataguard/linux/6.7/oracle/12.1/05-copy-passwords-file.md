---
layout: page
title: Копирование файла паролей с primary на standby
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/copy-passwords-file/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Копирование файла паролей с primary на standby



### На Primary


**Passwordfile**

	SQL> show parameter remote_login_passwordfile

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	remote_login_passwordfile	     string	 EXCLUSIVE


<br/>

	SQL> exit


<br/>

	$ chmod 4640 $ORACLE_HOME/dbs/orapworcl

<br/>


// Файл паролей можно создать следующей командой. Entries - ограничить максимальное количество подключений к базе (если ничего не путаю). Я не создавал новый файл паролей.

	$ orapwd fiel=orapwdorcl password=oracle12 entries=5



Копирую файл паролей

	$ scp $ORACLE_HOME/dbs/orapworcl oracle12@piter:$ORACLE_HOME/dbs/orapworcl

<br/>

### Standby

	$ chmod 4640 /u01/oracle/database/12.1/dbs/orapworcl
