---
layout: page
title: Инсталляция Oracle DataBase 12.2 в Oracle Linux 7.4 - Создание экземпляра базы данных (Instance)
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Создание экземпляра базы данных (Instance)
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, Создание Instance
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-instance-creation/
---

<br/>

<div style="padding:10px; border:thin solid black;">

    <h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>:: Создание экземпляра базы данных (Instance)

<br/>

Выполните команду:

    $ dbca

<br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_01.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_02.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_03.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_04.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_05.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_06.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_07.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_08.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_09.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_10.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_11.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_12.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_13.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_14.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_15.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_16.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_17.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_18.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_19.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_20.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<br/><br/>

### Подключение к Express Manager (раньше назвался Enterprise Manager)

<br/>

1. Сервер по http не принимает обращения. Работает только по https <br/>
   https://192.168.56.101:5500/em

2. Сейчас консолька требует flash player. Хром больше не поддерживает flash (по крайней мере официально). Пришлось подключаться с помощью Firefox.

<br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_21.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_22.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_23.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_24.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<img src="//img.oracledba.net/01-database/02-installation/01-single-instance/01-simple/02-linux/7.4/oracle/12.2/04-instance-creation/instance-creation_25.png" border="0" alt="Oracle 12.2 Instance Creation"><br/><br/>

<br/><br/>

    $ sqlplus / as sysdba

<br/>

    SQL> select status from v$instance;

    STATUS
    ------------
    OPEN
