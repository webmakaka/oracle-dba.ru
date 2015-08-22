---
layout: page
title: Удаление объектов RMAN (Recovery Manager)
permalink: /docs/oracle-database/backup-and-restore/rman/oracle-rman-delete/
---


<h2>Удаление объектов RMAN (Recovery Manager)</h2>


// Удалить устаревшие бэкапы с подтверждением удаления

    RMAN> delete obsolete;

// Удалить устаревшие бэкапы без подтверждения удаления

    RMAN> delete noprompt obsolete;

<br/>

    RMAN> DELETE EXPIRED BACKUP;
    RMAN> DELETE EXPIRED COPY;

// Удалить copy

    RMAN> delete copy;

// Удалить backupset с определенным ID

    RMAN> delete backupset 20;


// Удалить все архивные журналы.

    RMAN> delete archivelog all;
