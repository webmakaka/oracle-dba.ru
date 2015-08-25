---
layout: page
title: Монтирование RAID на узлах кластера
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/mount-raid-on-nodes/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Подготовка сервера storage.


НА rac1, rac2



    # mkdir /u02

<br/>

    # vi /etc/fstab

    storage:/raid /u02 nfs rw,bg,hard,nointr,tcp,vers=3,timeo=600,rsize=32768,wsize=32768,actimeo=0 0 0

<br/>

    # service  rpcbind restart
    # chkconfig --level 345 rpcbind on

    # chkconfig --level 345 nfs on
    # service nfs restart

<br/>

    # mount /u02

    # df -h
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/VolGroup-lv_root
                           35G  1.9G   32G   6% /
    tmpfs                 1.9G     0  1.9G   0% /dev/shm
    /dev/sda1             477M  135M  314M  31% /boot
    /dev/sdb1              40G   48M   38G   1% /u01
    storage:/raid         118G   60M  112G   1% /u02

<br/>



    # chown -R oracle12:oinstall /u02
    # chmod -R 775 /u02
