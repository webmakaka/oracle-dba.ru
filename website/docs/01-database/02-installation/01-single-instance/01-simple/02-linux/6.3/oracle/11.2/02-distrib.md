---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 Дистрибутивы и дополнительное ПО
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.3/oracle/11.2//distrib/
---


# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Дистрибутивы и дополнительное ПО

Последние версии БД Oracle и пакеты критических исправлений доступны коммерческим подписчикам  с активным контрактом на техническую поддержку. Если у вас есть контракт на техподдержку, вы можете скачать дистрибутивы базы данных непосредственно с сайта support.oracle.com.


Если контракта у вас нет, простой регистрации на сайте Oracle будет недостаточно, чтобы скачать последние версии даже для изучения.

Каких-либо ключей для активации нет. Для разработки (development) дистрибутивы можно использовать бесплатно, но для использования по основному их назначению (production), требуется приобрести лицензию.

<br/><br/>


<strong>VirtualBox:</strong><br/>
hxxp://www.virtualbox.org/wiki/Downloads



<strong>Дистрибутивы операционной системы Oracle Linux Server 6 Update 3 (x86_x64):</strong><br/>
hxxp://rutracker.org/forum/viewtopic.php?t=4112274




<strong>upd: Oracle Linux Server 6 Update 4 (x86_x64):</strong><br/>
hxxp://rutracker.org/forum/viewtopic.php?t=4407896



<strong>Дистрибутивы базы данных Oracle (11.2.0.3) Linux x64:</strong><br/>
hxxp://rutracker.org/forum/viewtopic.php?t=3749965


<strong>upd: Oracle (11.2.0.4) Linux x64:</strong><br/>
hxxp://rutracker.org/forum/viewtopic.php?t=4522137


<br/><br/>

<strong>Содержимое архивов:</strong>

<pre>
// Oracle Database (includes Oracle Database and Oracle RAC)
p10098816_112020_Linux-x86-64_1of7.zip
p10098816_112020_Linux-x86-64_2of7.zip

// Oracle Grid Infrastructure (includes Oracle ASM, Oracle Clusterware, and Oracle Restart)
p10098816_112020_Linux-x86-64_3of7.zip

// Oracle Database Client
p10098816_112020_Linux-x86-64_4of7.zip

// Oracle Gateways
p10098816_112020_Linux-x86-64_5of7.zip

// Oracle Examples
p10098816_112020_Linux-x86-64_6of7.zip

// Deinstall
p10098816_112020_Linux-x86-64_7of7.zip
</pre>

Для инсталляции Oracle в описываемой инструкции, достаточно первых 2х архивов.

<br/>

<strong>Putty:</strong><br/>
http://www.putty.org/


<strong>winscp:</strong><br/>
http://winscp.net/eng/download.php



<strong>XMing</strong> (необходимо установить XMing, дополнительные шрифты и рекомендую перезагрузить компьютер):<br/>
http://sourceforge.net/projects/xming/<br/>
http://sourceforge.net/projects/xming/files/Xming-fonts/


Далее, необходимо настроить правила доступа.<br/>
В самом простом варианте, правой кнопкой мыши по ярлыку xming. Зайти в свойства и в target дописать -ac (т.е. без контроля доступа)


<img src="http://img.oradba.net/img/oracle/database/simple/12.1/XMing.png" border="0" alt="XMing">
