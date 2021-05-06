---
layout: page
title: Инсталляция Oracle DataBase 11.2.0.3.2 в Oracle Linux 6.3 - Копирование дистрибутивов на сервер
description: Инсталляция Oracle DataBase 11.2.0.3.2 в операционной системе Oracle Linux 6.3 - Копирование дистрибутивов на сервер
keywords: Oracle DataBase 11.2, Oracle Linux 6.3, Копирование дистрибутивов на сервер
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/copy-oracle-distrib-on-server/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Копирование дистрибутивов базы данных на сервер (в каталог /tmp)

Необходимо скопировать следующие архивы на сервер в каталог /tmp:

    p10404530_112030_Linux-x86-64_1of7.zip
    p10404530_112030_Linux-x86-64_2of7.zip

Для инсталляции базы данных достаточно первых 2-х архивов из 7.

Если архивы, лежат на сервере с операционной системой linux, можно воспользоваться утилитой scp.

Например, следующей командой можно забрать дистрибутивы базы данных с другого сервера linux и положить их в каталог /tmp:

    # scp marley@192.168.1.5:/oracle/p10404530_112030_Linux-x86-64_{1..2}of7.zip /tmp/

Если Вы работаете под Windows, самый простой способ - воспользоваться winscp.

Далее нужно назначить владельцем скачанных архивов пользователя oracle11

    # chown -R oracle11:oinstall /tmp/p10404530_112030_Linux-x86-64_*

<br/><br/>
<br/><br/>

<div style="padding:10px; border:thin solid black;">

    <h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
