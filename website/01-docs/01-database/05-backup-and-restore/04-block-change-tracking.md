---
layout: page
title: Enable block change tracking
description: Enable block change tracking
keywords: Oracle Database, Enable block change tracking
permalink: /database/backup-and-restore/block-change-tracking/
---

# Enable block change tracking

    SQL> alter database enable block change tracking using file '/home/oracle/block_tracki/block_change_traning.trc';

// Отключить если не нужно

    SQL> alter database disable block change tracking;

<br/>

    SQL> select * from v$block_change_tracking;
