---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-instance-creation/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Создание экземпляра базы данных (Instance)


Выполните команду:

	$ dbca


<br/><br/>

<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_01.PNG" border="0" alt="Oracle Instance creation"><br/><br/>


<pre>

<strong>Step1: Operations</strong>

</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_02.PNG" border="0" alt="Oracle Instance creation"><br/><br/>

<pre>

<strong>Step2: Database Templates</strong>

</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_03.PNG" border="0" alt="Oracle Instance creation"><br/><br/>

<pre>

Oracle предлагает создать экземпляр базы данных на основе одного из подготовленных шаблонов.

1. Система обработки транзакций (OLTP) - когда необходимо оптимизировать ввод данных в базу данных. Преимущественно операции по добавлению и изменению данных.
2. База данных общего назначения (custom database) - вам предлагается самостоятельно выбрать системные параметры базы данных. (самый оптимальный вариант).
3. Хранилище данных (warehouse) - когда необходимо оптимизировать работу с данными в базе данных. Преимущество операции чтения данных и подстроения аналитических отчетов.

При необходимости, данные параметры можно будет изменить в pfile или spfile.

</pre>




<pre>

<strong>Step3: Database Identification</strong>

</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_04.PNG" border="0" alt="Oracle Instance creation"><br/><br/>


<pre>


Oracle предлагает задать имя для создаваемого экземпляра базы данных.


</pre>









<pre>
<strong>Step4: Management Options</strong>
</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_05.PNG" border="0" alt="Oracle Instance creation"><br/><br/>
<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_06.PNG" border="0" alt="Oracle Instance creation"><br/><br/>





<pre>
<strong>Step 5: Database Credentials</strong>
</pre>

<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_07.PNG" border="0" alt="Oracle Instance creation"><br/><br/>

<pre>

Вы можете для каждого из создаваемых системных паользователей задать индивидуальный пароль, либо указать 1 пароль
сразу для всех пользователей, перечисленных в таблице.


Пароль после можно поменять.
</pre>







<pre>
<strong>Step 6: Database File Locations</strong>
</pre>

<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_08.PNG" border="0" alt="Oracle Instance creation"><br/><br/>

<pre>
Далее необходимо указать место, где база данных будет хранить файлы базы данных - т.е. те файлы в которых собственно и будут храниться данные.

/u02/oradata
</pre>



<pre>
<strong>Step 7: Recovery Configuration</strong>
</pre>

<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_09.PNG" border="0" alt="Oracle Instance creation"><br/><br/>


<pre>
Fast Recovery Area (FRA) - определить нахождение и размер области на диске, где будут храниться резервные копии данных (и архивлоги, если предполагается их использовать и хранить в FRA).
Enable Archiving - включить режим работы базы данных Archivelog.

Данные параметры будут настроены уже после завершения установки базы данных.

</pre>



<pre>
<strong>Step 8: Database Content</strong>
</pre>

<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_10.PNG" border="0" alt="Oracle Instance creation"><br/><br/>
<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_11.PNG" border="0" alt="Oracle Instance creation"><br/><br/>
<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_12.PNG" border="0" alt="Oracle Instance creation"><br/><br/>


<pre>

Предлагается выбрать дополнительные компоненты. Если не предполагается их использовать, то скорее всего их и не следует устанавливать.

Oracle Text  - обеспечивает индексирование слов и поиск
http://docs.oracle.com/cd/B10501_01/text.920/a96517/cdefault.htm

Oracle OLAP - многомерный анализ данных, для аналитических приложений.
http://www.oracle.com/technetwork/documentation/olap-101824.html

Oracle Spatial -  для Geographic Information System (GIS) (Наверное, что-то вроде карт google maps)
http://docs.oracle.com/html/A88805_01/sdo_intr.htm

Oracle Multimedia - нужна в случае, если предполагается хранить в базе картинки, аудио, видео.
http://docs.oracle.com/cd/E11882_01/appdev.112/e10777/ch_intr.htm#i610845

Oracle JVM - нужна если нужно вызывать программы (процедуры, функции и т.д.), написанные на java непосредственно внутри базы данных.

Application Express -  приложение, с помощью которого можно достаточно просто с помощью "вайзардов" создавать приложения, работающие с базой данных. Имеет смысл оставить, только если предполагается с ним работать.

</pre>






<pre>
<strong>Step 9: Initialization Parameters: Memory</strong>
</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_13.PNG" border="0" alt="Oracle Instance creation"><br/><br/>

<pre>

Если не планируется на сервере создавать еще один экземпляр базы данных, имеет смысл выделить для сервера побольше памяти.  (> 90%).

(на картинке изображена установка с большим количеством оперативной памяти, чем прилагается в документе по созданию виртуальной машины)

Вы также можете самостоятельно задать системные параметры создаваемой базы данных.


</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_14.PNG" border="0" alt="Oracle Instance creation"><br/><br/>

<pre>
<strong>Step 9: Initialization Parameters: Character sets</strong>
</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_15.PNG" border="0" alt="Oracle Instance creation"><br/><br/>

<pre>
Если в базе будут использоваться русские буквы, рекомендуется выбрать кодировку, которая поддерживает данную возможность. Unicode, где каждый символ кодируется 2 байтами, вполне подходит для этой задачи.

</pre>



<pre>
<strong>Step 9: Initialization Parameters: Connection Mode</strong>
</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_16.PNG" border="0" alt="Oracle Instance creation"><br/><br/>


<ul>
	<li>Dedicated Server Mode - для каждого соединения создается отдельный сервис. </li>
	<li>Shared Server Mode - создается пул соединений, и все клиенты подключаются к базе данных через этот пул. Имеет смысл использовать только в случае нехватки ресурсов сервера на создание выделенных сервисов.</li>
</ul>


<pre>
<strong>Step 10: Initialization Parameters: DataBase Storage</strong>
</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_17.PNG" border="0" alt="Oracle Instance creation"><br/><br/>



<pre>
С помощью этого окна можно добавлять табличные пространства, щелкая по кнопке Add (Добавить). Некоторые табличные пространства создаются автоматически, и, раскрывая пункты навигационного окна слева и выбирая в нем элементы, вы можете изменять размеры и характеристики этих табличных пространств.
</pre>



<pre>
<strong>Step 11: Creation Options</strong>
</pre>

<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_18.PNG" border="0" alt="Oracle Instance creation"><br/><br/>


<pre>

Вы можете создать базу данных, записать данную конфигурацию в качестве шаблона для последующего использования и, по желанию, создать скрипт для создания базы данных, например, если нужно создать базу данных позже.

</pre>

<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_19.PNG" border="0" alt="Oracle Instance creation"><br/><br/>
<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_20.PNG" border="0" alt="Oracle Instance creation"><br/><br/>
<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_21.PNG" border="0" alt="Oracle Instance creation"><br/><br/>


<pre>
Можно подключиться к Enterprise Manager по адресу:
https://192.168.1.10:1158/em

</pre>


<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_22.PNG" border="0" alt="Oracle Instance creation"><br/><br/>
<img src="https://img.oracledba.net/img/oracle/database/simple/11.2/oracle11_database_instance_creation_23.PNG" border="0" alt="Oracle Instance creation"><br/><br/>


<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
