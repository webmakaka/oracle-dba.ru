---
layout: page
title: Repository Creation Utility (RCU)
permalink: /middleware/rcu/
---

# Repository Creation Utility (RCU)


<br/>

**Устанавливаю 27.11.2017**

<br/>

Ранее база данных была установлена по этому документу:

<ul>
    <li><a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4</a></li>
</ul>


<br/>
<br/>

Скачиваю отсюда:  
http://www.oracle.com/technetwork/middleware/data-integrator/downloads/index.html

Repository Creation Utility (RCU) (11.1.1.9.0) для Linux (x64)


<br/>

Скопировал ofm_rcu_linux_11.1.1.9.0_64_disk1_1of1.zip на сервер.


    $ ssh oracle12@192.168.56.101
    $ cd "distrib_folder"
    $ unzip ofm_rcu_linux_11.1.1.9.0_64_disk1_1of1.zip


<br/>

Чтобы избежать ошибки "ORA-28040: No matching authentication protocol"

Делаю следующее:

    $ cd /u01/oracle/database/12.2/network/admin/sqlnet.ora


    -- создал файл и добавил в него следующие строки
    $ vi sqlnet.ora


{% highlight shell %}

SQLNET.ALLOWED_LOGON_VERSION_CLIENT=8
SQLNET.ALLOWED_LOGON_VERSION_SERVER=8

{% endhighlight %}


<br/>

### Поехали устанавливать

    -- 192.168.1.5 - хостовая машина
    $ xclock -display 192.168.1.5:0


    $ export DISPLAY=192.168.1.5:0.0

    $ cd /tmp/rcuHome/bin
    $ ./rcu


<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic01.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic02.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic03.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic04.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic05.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic06.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic07.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic08.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic09.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic10.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic11.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic12.png" border="0" alt="RCU Installation">
<br/><br/><img src="http://img.oradba.net/03-middleware/rcu/pic13.png" border="0" alt="RCU Installation">





<br/>
<br/>

**Возможно будет полезно:**


<br/>

<ul>
    <li><a href="/docs/business-intelligence/repository-creation-utility/">Создание схемы в базе данных для приложения OBIEE с помощью Repository Creation Utility (RCU)</a></li>
</ul>
