---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - После инсталляции
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/post-installation-tasks/
---

# [Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM)]: После инсталляции

<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>

    $ vi /etc/oratab

Заменить:

    +ASM1:/u01/app/grid/12.1:N
    -MGMTDB:/u01/app/grid/12.1:N
    rac12:/u01/app/oracle/product/rac/12.1:N

на

    +ASM1:/u01/app/grid/12.1:Y
    -MGMTDB:/u01/app/grid/12.1:Y
    rac12:/u01/app/oracle/product/rac/12.1:Y

Правда я пока не знаю каким боком здесь ASM и что за MGMTDB.
