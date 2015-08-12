---
layout: page
title: Экземпляр базы данных Oracle (Oracle DataBase Instance)
permalink: /docs/architecture/instance/
---

# Экземпляр базы данных Oracle (Oracle DataBase Instance)


<br/>
Когда вы инсталлируете базу данных Oracle. Вы сначала устанавливаете программное обеспечение СУБД (Систему Управления Базой Данных, DataBase Software). Помимо СУБД, необходима также сама база данных. Одна система управления базой данных, может работать сразу с несколькими базами данных на одном сервере. Каждая такая база данных в терминологии Oracle называется экземпляром базы данных (DataBase Instance). Каждый запущенный экземпляр активно использует ресурсы процессора, оперативной и дисковой памяти.


Далее, мы постепенно разберем что у нас хранится на дисках (основные файлы), какие процессы за что отвечают и собственно, что хранится в оперативной памяти.



<strong>Oracle Database = Oracle DataBase Software + Oracle DataBase Instance (s)</strong>

<br/>

<div align="center">
<img src="http://img.oradba.net/architecture/OracleDatabaseFiles.jpg" border="0" alt="Oracle Instance"><br/>
</div>



Для того, чтобы узнать текущее состояние экземпляра базы данных,
можно выполнить следующую процедуру:

<br/>
<br/>
1) убедиться, что подключаетесь к базе с правильным параметром ORACLE_SID.<br/>
Поменять SID можно, командой <strong>export</strong>

    $ export ORACLE_SID=ora112

<br/>

    $ echo $ORACLE_SID
    ora112

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> select status from v$instance;

<br/>

    STATUS
    ------------
    OPEN

<br/><br/>

В данном случае, все хорошо.
