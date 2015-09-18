---
layout: page
title: Настройка параметров instance на primary для работы в DataGuard конфигурации
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/dataguard/linux/6.7/oracle/12.1/setup-instance-parameters-to-work-in-dataguard/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Настройка параметров instance на primary для работы в DataGuard конфигурации


<br/>

	SQL> alter system set LOG_ARCHIVE_CONFIG="DG_CONFIG=(master, slave)" scope=both;

<br/>

	SQL> alter system set log_archive_dest_2="SERVICE=standby LGWR SYNC VALID_FOR=(ONLINE_LOGFILES,PRIMARY_ROLE) db_unique_name=slave" scope=both;

<br/>

	SQL> alter system set log_archive_dest_state_2="enable" scope=both;

<br/>


Можно использовать defer, чтобы в лог постоянно не писалось, что имеются проблеымы с коннектом к standby.

	-- SQL> alter system set log_archive_dest_state_2="defer" scope=both;

<br/>

	SQL> alter system set standby_file_management= AUTO scope=both;

<br/>


Следующие параметры будт использоваться (насколько я понял) в случае, если INSTANCE будет переключе в режим STANDBY

	SQL> alter system set FAL_SERVER="slave" scope=both;
	SQL> alter system set FAL_CLIENT="master" scope=both;



LOG_ARCHIVE_CONFIG - определяем имена экземпляров, между которыми будет происходить обмен журналами.

LOG_ARCHIVE_DEST_2 - место хранение архивлогов (т.е. то место где хранятся логи и еще вот сюда просим положить).


PRIMARY_ROLE - экземпляр является основной базой

LGWR - мы будем передавать архивные журналы на standby сервер с помощью процесса LGWR.

Параметр ASYNC указывает, что данные, сгенерированные транзакцией, не обязательно должны быть получены на standby до завершения транзакции – это не приведет к остановке основной базы, если нет связи со standby.

log_archive_dest_2 - куда будут передаваться архивлоги - файловой системе или сервису (если я все правильно понял конечно).

fal_client='master' – этот параметр определяет, что когда экземпляр перейдет в режим standby, он будет являться клиентом для приема архивных журналов (fetch archive log).


fal_server='slave' – определяет FAL (fetch archive log) сервер, с которого будет осуществляться передача архивных журналов. Параметры fal_client и fal_server работают только когда база запущена в standby режиме.

standby_file_management='AUTO' – задаем режим автоматического управления файлами в standby режиме. При таком значении параметра все создаваемые или удаляемые файлы основной базы будут автоматически создаваться или удаляться и на standby базе.


СМ:  

http://docs.oracle.com/cd/B19306_01/server.102/b14239/log_arch_dest_param.htm

<br/>

###	Посмотреть значения заданных параметров


	SQL> show parameter arch
	SQL> show parameter log_archive_dest_state_1
	SQL> show parameter log_archive_dest_state_2

<br/>

	SQL> SELECT DEST_NAME,STATUS,DESTINATION
	FROM V$ARCHIVE_DEST
	WHERE DESTINATION IS NOT NULL;

<br/>

	SQL> select name, value
	from v$parameter where name like 'fal%';

<br/>

	SQL>  show parameter fal;

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	fal_client			     string	 slave
	fal_server			     string	 master
