---
layout: page
title: Настройка сети (Настройка слушивающего процесса Listener)
permalink: /docs/architecture/networking/
---


## Настройка сети (Настройка слушивающего процесса Listener)


2 конфигурационных файла отвечают за подключение к Oracle.<br/>
Один обязательный (listener.ora) и один скорее для удобства, но для работы некоторых программ, он также может быть обязательным
(tnsnames.ora).<br/>


По умолчанию файлы хранятся:

<br/>
/u01/app/oracle/product/11.2/network/admin

<br/><br/>
<strong>listener.ora</strong>
<br/>


    LISTENER =
      (DESCRIPTION_LIST =
        (DESCRIPTION =
          (ADDRESS_LIST =
            (ADDRESS = (PROTOCOL = TCP)(HOST = hostname.domain.com)(PORT = "port_number"))
          )
        )
      )

    SID_LIST_LISTENER =
      (SID_LIST =
      (SID_DESC =
          (GLOBAL_DBNAME = SID1)
          (ORACLE_HOME = /u01/app/oracle/product/11.2)
          (SID_NAME = SID1)
        )
      (SID_DESC =
          (GLOBAL_DBNAME = SID2)
          (ORACLE_HOME = /u01/app/oracle/product/11.2)
          (SID_NAME = SID2)
        )

      )


  <br/>
  <strong>tnsnames.ora</strong><br/>
  <br/>

  В данном файле описываются подробности подключения к базе данных. Т.о, становится возможным явно не указывать некоторые параметры. (Например, хост, порт и др.).
  И сразу обращаться по имени.


    SID1 =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = hostname.domain.com)(PORT = "port_number"))
        )
        (CONNECT_DATA =
          (SERVER = DEDICATED)
          (SERVICE_NAME = SID1)
        )
      )

    SID2 =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = hostname.domain.com)(PORT = "port_number"))
        )
        (CONNECT_DATA =
          (SERVER = DEDICATED)
          (SERVICE_NAME = SID2)
        )
      )



  В следующем примере, происходит подключение к базе данных с использованием записи с именем orcl в файле tnsnames.ora.

  Т.е. для подключения к базе, не приходится дополнительно вводить host, port, sid

  <br/><br/>

  <img src="http://img.fotografii.org/images/odba/oracleInstallation/_Windows/Oracle_Database_10g_Release_2_Installation/Oracle_Database_10g_Release_2_Installation_114.png" border="0" alt="tnsnames.ora">





<br/>

### Основные команды службы слушателя (Listener):

    lsnrctl status
    lsnrctl stop
    lsnrctl start
    lsnrctl restart


<br/>

### Информация о Listener из командной строки:

    $ ps -edf | grep tns
	root        13     2  0 Aug09 ?        00:00:00 [netns]
	oracle12  6604     1  0 Aug09 ?        00:00:02 /u01/oracle/grid/12.1/bin/tnslsnr LISTENER -no_crs_notify -inherit
	oracle12 16991 14456  0 09:26 pts/1    00:00:00 grep tns

<br/>

    $ lsnrctl services

    LSNRCTL for Linux: Version 12.1.0.2.0 - Production on 15-AUG-2015 15:09:04

    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    Services Summary...
    Service "+ASM" has 1 instance(s).
      Instance "+ASM", status READY, has 1 handler(s) for this service...
        Handler(s):
          "DEDICATED" established:0 refused:0 state:ready
             LOCAL SERVER
    Service "orcl12XDB" has 1 instance(s).
      Instance "orcl12", status READY, has 1 handler(s) for this service...
        Handler(s):
          "D000" established:0 refused:0 current:0 max:1022 state:ready
             DISPATCHER <machine: piter.localdomain, pid: 8805>
             (ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=60254))
    Service "slave" has 1 instance(s).
      Instance "orcl12", status READY, has 1 handler(s) for this service...
        Handler(s):
          "DEDICATED" established:0 refused:0 state:ready
             LOCAL SERVER
    Service "slave_DGB" has 1 instance(s).
      Instance "orcl12", status READY, has 1 handler(s) for this service...
        Handler(s):
          "DEDICATED" established:0 refused:0 state:ready
             LOCAL SERVER
    The command completed successfully



<br/>

### Информация о Listener из консоли sqlplus:

<br/>

    SQL> show parameter local_listener;

    NAME				     TYPE	 VALUE
    ------------------------------------ ----------- ------------------------------
    local_listener			     string	 LISTENER_ORCL12


<br/>

    SQL> show parameter listener

	NAME				     TYPE
	------------------------------------ ---------------------------------
	VALUE
	------------------------------
	listener_networks		     string

	local_listener			     string

	remote_listener 		     string


<br/>

    SQL> alter system set local_listener='(DESCRIPTION =(ADDRESS = (PROTOCOL = TCP)(HOST = moscow.localdomain)(PORT = 1521)))' scope=both;



 <br/>

 ### OFFTOPIC Listener для grid


    $ srvctl status listener
    Listener LISTENER is enabled
    Listener LISTENER is running on node(s): piter


 <br/>

    $ srvctl config listener
    Name: LISTENER
    Type: Database Listener
    Home: /u01/oracle/grid/12.1
    End points: TCP:1521
    Listener is enabled.
