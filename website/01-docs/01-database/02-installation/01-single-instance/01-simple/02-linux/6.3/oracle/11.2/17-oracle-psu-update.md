---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-psu-update/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Обновление базы патчами, рекомендованными Oracle:


<pre>

Если у вас имеется активный контракд для доступа на support.oracle.com, вы можете
скачать последние обновления для продуктов Oracle и при необходимости сделать запрос в тех поддержку, в т.ч.
на выпуск каких-нибудь заплаток. Особенно актуально это было в период, когда менялись часовые пояся из за
распоряжения Президента.

На одной из закладок, Oracle показывает, какие патчи он рекомендует применить.

</pre>

<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/simple/11.2/OraclePatches_01.PNG" border="0" alt="Oracle Patches"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/OraclePatches_02.PNG" border="0" alt="Oracle Patches"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/OraclePatches_03.PNG" border="0" alt="Oracle Patches"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/OraclePatches_04.PNG" border="0" alt="Oracle Patches"><br/><br/>



<br/><br/>

<pre>

Перед примененением, рекомендуется обновить саму систему обновления патчей, которая называется OPatch.
Сам OPatch имеет свой внутренний код 6880880 и доступен для скачивания:

https://updates.oracle.com/ARULink/PatchDetails/process_form?patch_num=6880880
</pre>

<br/><br/>


<img src="http://img.oradba.net/img/oracle/database/simple/11.2/OraclePatches_05.PNG" border="0" alt="Oracle Patches"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/OraclePatches_06.PNG" border="0" alt="Oracle Patches"><br/><br/>


<br/><br/>

### Обновление OPatch


	$ rm -rf /u01/oracle/database/11.2/OPatch/
	$ unzip p6880880_112000_Linux-x86-64.zip
	$ mv OPatch/ /u01/oracle/database/11.2
	$ cd /u01/oracle/database/11.2/OPatch


<br/>

	$ ./opatch version



<br/>

	OPatch Version: 11.2.0.3.0
	OPatch succeeded.



### 2) Применение патча 1


	$ sqlplus / as sysdba
	SQL> shutdown immediate;
	SQL> quit



<br/>

	$ cd /tmp

<br/>

	$ export PATH=$PATH:/u01/oracle/database/11.2/OPatch
	$ unzip p13632717_112030_Linux-x86-64.zip
	$ cd 13632717/
	$ opatch napply -skip_subset -skip_duplicate



<br/>

	....
	OPatch succeeded.


<br/>

	cd $ORACLE_HOME/rdbms/admin
	$ sqlplus / as sysdba

<br/>

	SQL> startup
	SQL> @catbundle.sql cpu apply
	SQL> QUIT


<br/>


### 3) Применение патча 2

	$ sqlplus / as sysdba
	SQL> shutdown immediate;
	SQL> quit

<br/>

	$ cd /tmp

<br/>

	$ unzip p13696216_112030_Linux-x86-64.zip
	$ cd 13696216
	$ opatch prereq CheckConflictAgainstOHWithDetail -ph ./


<br/>

	$ opatch apply

<br/>

	***
	OPatch completed with warnings.

<br/>

	$ cd $ORACLE_HOME/rdbms/admin
	$ sqlplus / as sysdba
	SQL> startup
	SQL> @catbundle.sql psu apply
	SQL> QUIT



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
