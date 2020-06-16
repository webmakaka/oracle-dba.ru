---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID
description: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID
keywords: Oracle DataBase 12.1, Centos 6.7, ASM, GRID
permalink: /database/installation/single/asm/linux/6.7/oracle/12.1/
---

# [Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]

<br/>

В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Oracle Linux.

Использовать его следует, если вы только приступаете к изучению основ администрирования баз данных Oracle. В случае необходимости использования в промышленной среде, необходимо обязательно обеспечить резервное копирование, мультиплексирование критичных для работы базы данных файлов и правильно настроить системные параметры.

В случае обнаружения ошибок, неточностей, опечаток или вам известны лучшие способы, пишите мне на адрес эл. почты:

<div>
	<img src="/img/a3333333mail.gif" alt="Marley" border="0">
</div>

<br/>

**Предыдущая версия документа:**  
Инсталляция Oracle DataBase 11G R2 x86 64 bit в операционной системе Oracle Linux 5.7 x86 64 bit (ASM)  
https://docs.google.com/document/d/1iGmRtwwcC9FGESnlR7v5qrcLKOzGIoh1GNeU5N0Q5cQ/edit

<br/>

<strong>Самые последние версии (на момент написания):</strong>

<ul>
	<li>Oracle Linux - 6.7</li>
	<li>Oracle DataBase - 12.1</li>
</ul>

<br/><br/>

Инсталляция происходит на удаленный сервер без GUI.

Управление процессом установки и настройки происходит с рабочей станции под управлением Linux по SSH.

<br/>

Шаги без ссылок, предполагают, что делается тоже самое, что и в <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">инструкции без ASM и без GRID</a>. (дабы не писать лишнего)

<br/>

## Подготовка операционной системы Linux к инсталляции базы данных Oracle:

<ul>

    <li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/prepare/">Установка hostname и hosts</a></li>


    <li>Установка параметров ОС перед стартом</li>

    <li>Настройка актуального времени</li>

    <li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/asmlib-installation/">Инсталляция ASMLIB для работы ASM</a></li>

    <li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/prepare-kernel-parameters-and-user-environments/">Конфигурирование системных пользователей, настройка параметров системы</a></li>

    <li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/prepare-asm-disks/">Подготовка ASM дисков к инсталляции базы данных</a></li>

    <li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/create-folder-structure-and-user-permissions/">Создание структуры каталогов и назначение необходимых прав</a></li>

    <li>Автозапуск только выбранных программ</li>

    <li>Настройка Display Manger</li>

    <li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/extract-oracle-distrib-from-archives/">Извлечение дистрибутивов базы Oracle из архивов</a></li>

</ul>

<br/><br/>

## Инсталляция GRID:

<ul>
	<li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/grid-installation/">Инсталляция GRID</a></li>

</ul>

<br/><br/>

## Создание дисковых групп ASM:

<ul>
	<li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/asm-diskgroup-creation/">Создание дисковых групп ASM</a></li>

</ul>

<br/><br/>

## Инсталляция СУБД Oracle (DataBase SoftWare):

<ul>
    <li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/oracle-database-software-installation/">Инсталляция СУБД Oracle (DataBase SoftWare)</a></li>
</ul>

<br/><br/>

## Создание экземпляра базы данных (Instance):

<ul>
    <li><a href="/database/installation/single/asm/linux/6.7/oracle/12.1/oracle-instance-creation/">Создание экземпляра базы данных (Instance)</a></li>
</ul>
