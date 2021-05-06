---
layout: page
title: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Инсталляция ASMLIB на узлах кластера
description: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Инсталляция ASMLIB на узлах кластера
keywords: Oracle DataBase 12.1, Oracle Linux 6.7, RAC, (ISCSI + ASM), ASMLIB
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/asmlib-installation/
---

# [Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM)]: Инсталляция ASMLIB на узлах кластера

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>

В Oracle Linux 6 oracleasm kernel driver встроены в ядро UEK и как следствиет не требует инсталляции.

Необходимо с сайта Oracle:

http://www.oracle.com/technetwork/server-storage/linux/asmlib/rhel6-1940776.html

Скачать: oracleasmlib-\*.x86_64.rpm

    # cd /tmp
    # wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.4-1.el6.x86_64.rpm

<br/>

    # yum install -y \
    oracleasm \
    oracleasm-support \
    oracleasmlib-2.0.4-1.el6.x86_64.rpm

<br/>

Проверяем инсталлированные пакеты:

    # rpm -qa | grep oracleasm
    oracleasm-support-2.1.8-1.el6.x86_64
    oracleasmlib-2.0.4-1.el6.x86_64

Если используется Centos, RedHat а не OEL, нужно еще установить:.

    # yum install -y \
    kmod-oracleasm.x86_64
