---
layout: page
title: BACKUPы на DataGuard
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/dataguard/linux/6.7/oracle/12.1/backups/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: BACKUPы на DataGuard


Смысл в том, что:

1) Бекапы всеравно нужно делать.  
2) FRA может заполниться архивлогами. Если не предпринять меры, то сервер остановится.  


Следующим образом предлагает делать бекапы автор курса [Udemy] easy way to set oracle active dataguard.



<br/>

    SQL> show parameter recovery

    NAME				     TYPE	 VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest		     string	 +ARCH
    db_recovery_file_dest_size	     big integer 40000M
    recovery_parallelism		     integer	 0


<br/>

### ALL DB:

    RMAN> CONFIGURE CONTROLFILE AUTOBACKUP FORMAT FOR DEVICE TYPE DISK CLEAR;

    RMAN> CONFIGURE CHANNEL DEVICE TYPE DISK FORMAT '+ARCH/%d_DB_%u_%s_%p';


<br/>

### PRIMARY database:

    RMAN> CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 7 DAYS;

    RMAN> CONFIGURE DEFAULT DEVICE TYPE TO DISK;

    RMAN> CONFIGURE CONTROLFILE AUTOBACKUP ON;

<br/>

### STANDBY database:

    RMAN> CONFIGURE BACKUP OPTIMIZATION ON;

    RMAN> CONFIGURE ARCHIVELOG DELETION POLICY TO NONE;


<br/>

### Backups FULL

    RMAN> RUN {
        CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET PARALLELISM 1;
        BACKUP CHECK LOGICAL INCREMENTAL LEVEL 0 FILESPERSET 10 FORMAT '+ARCH/FULL0_%D_%U'
        (DATABASE INCLUDE CURRENT CONTROLFILE);
        BACKUP NOT BACKED UP 1 TIMES FILESPERSET 10
        (ARCHIVELOG ALL DELETE INPUT FORMAT '+ARCH/%d_DB_%u_%s_%p');
        BACKUP (CURRENT CONTROLFILE FORMAT '+ARCH');
    }

<br/>

    RMAN> RUN {
        COPY CURRENT CONTROLFILE TO '/backups/oracle/12.1/orcl12/controlfiles/CTL_STANDBY.CTL';
    }

<br/>

### Backup Archives

    RMAN> RUN {
       CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET PARALLELISM 2;
       BACKUP ARCHIVELOG ALL FORMAT '+ARCH/ARCH0_%D_%u' DELETE ALL INPUT;
    }


<br/>

    RMAN> RUN {
        COPY CURRENT CONTROLFILE TO '/backups/oracle/12.1/orcl12/controlfiles/CTL_STANDBY.CTL';
    }
