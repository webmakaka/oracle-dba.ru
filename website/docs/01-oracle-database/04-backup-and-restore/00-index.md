---
layout: page
title: Backup и Restore Oracle DataBase
permalink: /docs/oracle-database/backup-and-restore/
---


### Backup и Restore Oracle DataBase


Бла, бла, бла. Всегда нужно делать бекапы, иначе будет как на картинке "Он дропнул базу и не делал бэкапы".

Бекапы должны выполняться автоматически, согласно установленным правилам. Администратор должен вмешиваться, если что-то пошло не так, а не каждый раз, когда понадобился бекап.

Рекомендуется время от времени восстанавливать копию базы данных из бекапов, чтобы убедиться, что все в актуальном состоянии, да и вообще всегда нужно иметь подготовленную инструкцию по восстановлению.


Бекапы следует хранить на другом сервере, желательно не в том же самом помещении. Если такой возможности нет, то следует хранить на каком-нибудь другом диске, отличном от того, где хранятся файлы базы данных.



Резервное копирование баз данных Oracle подразумевает создание резервных копий файлов данных, управляющих файлов и файлов архивных журналов.
Вдобавок в состав запасного набора могут включать файлы spfile, init.ora, listener.ora и tnsnames.ora


Резервное копирование выполняеся:

<ul>
<li>Средствами операционной системы. </li>
<li>Средствами RMAN (Recovery Manager). </li>
</ul>


Для центролизованного хранения бекапов большого количества баз данных, Oracle предлагает использовать Oracle Catalog - еще одна база, созданная специально для бекапов (Что в ней хранится пока сказать не могу. Не использовал никогда). Почему-то я думал, что в ней хранятся бекапы. Но чего-то стал сомневаться в этом.


Помимо бекапов, можно делать экспорт нужной схемы в файл. После при желании ее можно также импортировать. При этом не нужны никакие другие файлы, кроме самого файла дампа.



<br/>

### Базовые знания о бекапах в Oracle

<ul>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/oracle-database-backup/">Вводная информация о резервном копировании баз данных Oracle</a>
    </li>
</ul>


<br/>

### Oracle Recomery Manager (Rman)

<ul>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/rman/fra/">Fast Recovery Area (FRA)</a>
    </li>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/rman/about-oracle-rman/">Утилита RMAN (Recovery Manager)</a>
    </li>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/rman/oracle-rman-backup/">Создание резервных копий с помощью утилиты RMAN (Recovery Manager)</a>
    </li>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/rman/oracle-rman-restore-and-recover/">Восстановление из резервой копий с помощью утилиты RMAN (Recovery Manager)</a>
    </li>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/rman/oracle-rman-delete/">Удаление объектов RMAN (Recovery Manager)</a>
    </li>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/rman/rman-catalog-installation/">Создание RMAN Catalog (Для хранение бекапов баз в специальной базе для бекапов)</a>
    </li>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/rman/rman-incarnations-sample/">Пример с инкарнациями</a>
    </li>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/rman/change-db-unique-name-in-catalog/">Поменять db_unique_name в RMAN каталоге</a>
    </li>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/low-space-in-fra/">Недостаточно свободного места в Fast Recovery Area</a>
    </li>


</ul>


<br/>

### Oracle Data Pump (Export / Import схем) (с 11 версии Oracle)

До 11 версии использовались похожие утилиты - IMP/EXP.

<ul>
    <li>
        <a href="/docs/oracle-database/backup-and-restore/oracle-data-pump/">Утилиты экспорта и импорта данных Data Pump (Резервное копирование объектов схемы)</a>
    </li>
    <li>
        <a href="http://odba.ru/showthread.php?t=28">Утилиты exp и imp</a>
    </li>
</ul>




<br/>

### Другое:

<ul>

    <li>
        <a href="/docs/oracle-database/backup-and-restore/oracle-11-transportable-tablespaces/">[Habrahabr] Транспортируемые табличные пространства в Oracle 11g</a>
    </li>
</ul>
