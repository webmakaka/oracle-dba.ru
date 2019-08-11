---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/
---

### Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64



<div style="padding:10px; border:thin solid black;">

<strong>Предупреждение</strong> Из-за перевода времени нашим "Руководством". Время на сервере может работать по-старому. В некоторых случаях из-за этого неправильно работает Enterprise Manager. Все это исправляется патчами, которые могут скачать счастливые обладатели доступа к support oracle. У меня сейчас нет такой возможности. Если кто скинет, прикреплю патчи к теме. На момент написания статьи такой проблемы не было и на момент написания у меня самого был доступ к support oracle. Проблема патчится патчем с кодовым названием DST v23.

</div>

<br/>

В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Oracle Linux.

Использовать его следует, если вы только приступаете к изучению основ администрирования баз данных Oracle. В случае необходимости использования в промышленной среде, необходимо обязательно обеспечить резервное копирование, мультиплексирование критичных для работы базы данных файлов и правильно настроить системные параметры.

В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, пишите мне адрес эл. почты:

<div>
	<img src="http:///img/a3333333mail.gif" alt="Marley" border="0">
</div>


<strong>Самые последние версии (на момент написания):</strong>

<ul>
	<li>Oracle Linux - 6.3 (лучше ставьте 6.7)</li>
	<li>Oracle DataBase - 11.2.0.3 (лучше ставьте 11.2.0.4)</li>
</ul>

<br/>

Инсталляция происходит на удаленный сервер без GUI.

Управление процессом установки и настройки происходит с рабочей станции под управлением Windows, на которой установлены putty и xming.

При помощью консоли putty на сервере выполняются команды. Xming нужен для получения графических изображений.



<br/><br/>
<h2>Документация:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/docs/">Официальная документация</a><br/></li>
</ul>



<br/><br/>

<h2>Дистрибутивы:</h2>


<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/distrib/">Дистрибутивы баз данных и дополнительное программное обеспечение</a><br/></li>
</ul>

<br/><br/>

<h2>Подготовка операционной системы Linux к инсталляции базы данных Oracle:</h2>


<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/setup-os-parameters-before-we-start/">Настройка некоторых параметров операционной системы</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/network-interface/">Настройка сетевых интерфейсов</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/install-mandatory-packages/">Инсталляция обязательных пакетов</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/setup-actual-time/">Настройка актуального времени</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/prepare-hdd-to-install-oracle/">Подготовка дисков к инсталляции базы данных</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/prepare-kernel-parameters-and-user-environments/">Конфигурирование системных пользователей, настройка параметров системы</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/autostart-only-packages-what-needed/">Автозапуск только выбранных программ</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/create-folder-structure-and-user-permissions/">Создание структуры каталогов и назначение необходимых прав</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/copy-oracle-distrib-on-server/">Копирование дистрибутивов базы данных на сервер</a></li>
</ul>


<br/><br/>

<h2>Инсталляция базы данных:</h2>
<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-database-software-installation/">Инсталляция СУБД Oracle (DataBase SoftWare)</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-listener-creation/">Создание службы удаленного подключения к серверу (Listener)</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-instance-creation/">Создание экземпляра базы данных (Instance)</a></li>
</ul>

<br/><br/>

<h2>После инсталляции:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/autorstart-oracle-after-restart/">Настройка автозапуска Oracle после перезагрузки</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-cold-backup/">Создание резервной копии созданной базы данных (холодный backup)</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-psu-update/">Обновление базы патчами, рекомендованными Oracle</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-restrict-root-access/">Запретить удаленное подключение к серверу баз данных пользователем root</a></li>
</ul>

<br/><br/>

<h2>Обеспечение дополнительной отказоустойчивости и надежности:</h2>

<ul>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-multiplex-controlfiles/">Мультиплексирование controlfiles</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-multiplex-redologs/">Мультиплексирование redologs</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/enable-archivelog-mod/">Включить режим работы ARCHIVELOG</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-multiplex-archivelogs/">Мультиплексирование archivelog</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-additionals-datafiles/">Расширение табличных пространств (создание дополнительных файлов для табличных пространств)</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/enable-flashback-mod/">Включить режим работы FLASH BACK</a></li>
	<li><a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-final-hot-backup/">Контрольный backup (горячий backup)</a></li>
</ul>


<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
