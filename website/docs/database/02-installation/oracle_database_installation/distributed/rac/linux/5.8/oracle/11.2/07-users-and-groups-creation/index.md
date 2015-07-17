---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /oracle_database_installation/rac/linux/5.8/oracle/11.2/users-and-groups-creation/
---

# <a href="/oracle_database_installation/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Создание пользователя oracle11 и групп

<br/>


Настройка параметров системы (выполняется на обоих узлах кластера)


Перед тем как вносить изменения в конфигурационные скрипты, следует предварительно создать их резервные копии:

	# {
	cp /etc/sysctl.conf /etc/sysctl.conf.bkp
	cp /etc/security/limits.conf /etc/security/limits.conf.bkp
	cp /etc/pam.d/login /etc/pam.d/login.bkp
	cp /etc/profile /etc/profile.bkp
	}

Создаем группы:

	# groupadd -g 1000 oinstall
	# groupadd -g 1001 dba
	# groupadd -g 1002 oper


Создаем пользователя oracle11, сообщаем, что он будет членом групп dba и oinstall и домашним каталогом у него будет /home/oracle11

	# useradd -g oinstall -G dba -d /home/oracle11 oracle11

Устанавливаем пароль для пользователе oracle11

	# passwd oracle11




==============

P.S.

Видел как на однром из сайтов создают следующих пользователей и групп. Наверное это более правильно.


	groupadd -g 1020 asmadmin
	groupadd -g 1021 asmdba
	useradd -u 1100 -g oinstall -G asmadmin,asmdba grid
	useradd -u 1101 -g oinstall -G dba,asmdba oracle11
