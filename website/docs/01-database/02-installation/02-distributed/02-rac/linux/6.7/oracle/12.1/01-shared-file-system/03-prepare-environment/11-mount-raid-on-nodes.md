---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Монтирование RAID на узлах кластера
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/mount-raid-on-nodes/
---


# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Монтирование RAID на узлах кластера


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>



    # mkdir /u02

<br/>

    # vi /etc/fstab

    storage:/raid /u02 nfs rw,bg,hard,nointr,tcp,vers=3,timeo=600,rsize=32768,wsize=32768,actimeo=0 0 0

<br/>

    # chkconfig --level 345 rpcbind on
    # service  rpcbind restart

    # chkconfig --level 345 nfs on
    # service nfs restart

<br/>

    # mount /u02

<br/>

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
