---
layout: page
title: Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/
---

# В разработке!  
# В разработке!  
## Помогайте, кому нечем заняться!  
# В разработке!  
# В разработке!  



В случае обнаружения ошибок, неточностей, опечаток или вам известны лучшие способы, пишите мне на адрес эл. почты:


<div>
	<img src="http://img.fotografii.org/a3333333mail.gif" border="0">
</div>


<br/>
<br/>


<div style="padding:10px; border:thin solid black;">

Для информации:

db_name - должно быть одинаковое на узлах  
db_unique_name - должно быть разными на узлах  

</div>



<br/>

## Подготовка виртуальных машин:


<ul>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/info-about-env/">Описание системы, которое будет настраиваться</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/prepare-env/">Предварительные шаги по настройке environment</a></li>

</ul>



<br/>


## Подготовка дупликата:


<ul>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/setup-oracle-network-services/">Настройка сетевых служб Oracle для создания standby дупликата</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/copy-passwords-file/">Копирование файла паролей с primary на standby</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/startup-instance-on-standby/">Стартую instance на standby</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/check-duplicate-env/">Проверяем, что файловая система схожа на 2-х серверах</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-connection-check/">Проверка подключения RMAN к обоим Instance</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-script-for-duplicate-instance/">Создание rman скрипта для дупликата и его выполнение</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-script-for-duplicate-instance/">Создание rman скрипта для дупликата и его выполнение</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps/">Шаги, выполняемые после создания дупликата</a></li>

</ul>
