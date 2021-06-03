---
layout: page
title: Инсталляция Oracle DataBase 12c в Oracle Linux 6.7 - Дистрибутивы и дополнительное ПО
description: Инсталляция Oracle DataBase 12c в операционной системе Oracle Linux 6.7 - Дистрибутивы и дополнительное ПО
keywords: Oracle DataBase 12c, Oracle Linux 6.7, Дистрибутивы и дополнительное ПО
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/distrib/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Дистрибутивы и дополнительное ПО

Последние версии БД Oracle и пакеты критических исправлений доступны коммерческим подписчикам с активным контрактом на техническую поддержку. Если у вас есть контракт на техподдержку, вы можете скачать дистрибутивы базы данных непосредственно с сайта support.oracle.com.

Если контракта у вас нет, простой регистрации на сайте Oracle будет недостаточно, чтобы скачать последние версии даже для изучения.

Каких-либо ключей для активации нет. Для разработки (development) дистрибутивы можно использовать бесплатно, но для использования по основному их назначению (production), требуется приобрести лицензию.

<br/>

### Программное обеспечение:

<strong>VirtualBox:</strong><br/>
http://www.virtualbox.org/wiki/Downloads

<br/>

<strong>Дистрибутивы операционной системы Oracle Linux Server 6 Update 7 (x86_x64):</strong><br/>
http://linux.oracle.com

<strong>Резервный источники для скачивания:</strong><br/>
hxxp://rutracker.org/forum/viewtopic.php?t=4603407

<br/>

<strong>Дистрибутивы базы данных Oracle (12.1) Linux x64:</strong><br/>
http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html

<strong>Резервный источники для скачивания:</strong><br/>
hxxp://rutracker.org/forum/viewtopic.php?p=65149195#65149195

Для инсталляции достаточно:<br/>

linuxamd64_12c_database_1of2.zip<br/>
linuxamd64_12c_database_2of2.zip

<br/>

### Если компьютер с которого происходит управление инсталляцией под Windows:

<strong>Putty (SSH Клиент):</strong><br/>
http://www.putty.org/

<br/>

<strong>XMing (Для отображения графических окон в процессе инсталляции)</strong> (необходимо установить XMing, дополнительные шрифты и перезагрузить компьютер):<br/>
http://sourceforge.net/projects/xming/<br/>
http://sourceforge.net/projects/xming/files/Xming-fonts/

<br/><br/>

<p>Далее, необходимо настроить правила доступа.<br />
В самом простом варианте, правой кнопкой мыши по ярлыку xming. Зайти в свойства и в target дописать -ac (т.е. без контроля доступа)</p>

<p><img src="https://img.oracledba.net/img/oracle/database/simple/12.1/XMing.png" border="0" alt="XMing" /></p>

<br/><br/>

<strong>winscp (Для копирования файлов на сервер):</strong><br/>
http://winscp.net/eng/download.php

<br/>

### Если компьютер с которого происходит управление инсталляцией под Linux:

Все уже есть