---
layout: page
title: Настройка сети (Настройка слушивающего процесса Listener)
permalink: /docs/architecture/networking/
---


<h2>Настройка сети (Настройка слушивающего процесса Listener)</h2><br/>

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
            (ADDRESS = (PROTOCOL = TCP)(HOST = hostname.domain.com)(PORT = &lt;port_number&gt;))
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
          (ADDRESS = (PROTOCOL = TCP)(HOST = hostname.domain.com)(PORT = &lt;port_number&gt;))
        )
        (CONNECT_DATA =
          (SERVER = DEDICATED)
          (SERVICE_NAME = SID1)
        )
      )

    SID2 =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = hostname.domain.com)(PORT = &lt;port_number&gt;))
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
<h3>Основные команды службы слушателя (Listener):</h3>

    lsnrctl status
    lsnrctl stop
    lsnrctl start
    lsnrctl restart
