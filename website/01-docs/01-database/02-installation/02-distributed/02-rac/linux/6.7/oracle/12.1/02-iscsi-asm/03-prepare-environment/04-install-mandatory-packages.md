---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Инсталляция обязательных пакетов
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/install-mandatory-packages/
---

# [Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM)]: Инсталляция обязательных пакетов

<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2, storage</strong></span></td>
</tr>

</table>

Если в каталоге /etc/yum.repos.d нет нет файлов с описанием репозиториев Oracle Linux.

    # vi /etc/yum.repos.d/OracleLinuxRepo.repo

<br/>

    [OEL6]
    name=Oracle Enterprise Linux $releasever - $basearch
    baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/latest/$basearch/
    gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
    gpgcheck=1
    enabled=1

<br/>

    # yum repolist

<br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Инсталляция пакетов для работы в ОС</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2 и storage</strong></span></td>
</tr>

</table>

    # yum update -y

<br/>

    # yum install -y \
    gcc \
    make \
    openssh-clients \
    wget \
    xinetd \
    screen \
    gamin \
    unzip \
    ntp \
    net-snmp \
    ntsysv \
    bind-utils

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Инсталляция обязательных пакетов для инсталляции Oracle</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>

Следующие пакеты или более поздние должны быть установлены в OEL 6.x:

    binutils-2.20.51.0.2-5.11.el6 (x86_64)
    compat-libcap1-1.10-1 (x86_64)
    compat-libstdc++-33-3.2.3-69.el6 (x86_64)
    compat-libstdc++-33-3.2.3-69.el6.i686
    gcc-4.4.4-13.el6 (x86_64)
    gcc-c++-4.4.4-13.el6 (x86_64)
    glibc-2.12-1.7.el6 (i686)
    glibc-2.12-1.7.el6 (x86_64)
    glibc-devel-2.12-1.7.el6 (x86_64)
    glibc-devel-2.12-1.7.el6.i686
    ksh
    libgcc-4.4.4-13.el6 (i686)
    libgcc-4.4.4-13.el6 (x86_64)
    libstdc++-4.4.4-13.el6 (x86_64)
    libstdc++-4.4.4-13.el6.i686
    libstdc++-devel-4.4.4-13.el6 (x86_64)
    libstdc++-devel-4.4.4-13.el6.i686
    libaio-0.3.107-10.el6 (x86_64)
    libaio-0.3.107-10.el6.i686
    libaio-devel-0.3.107-10.el6 (x86_64)
    libaio-devel-0.3.107-10.el6.i686
    make-3.81-19.el6
    sysstat-9.0.4-11.el6 (x86_64)

<br/>

    # yum install -y \
    binutils \
    compat-libstdc++*33* \
    elfutils-libelf \
    elfutils-libelf-devel \
    elfutils-libelf-devel-static \
    gcc \
    gcc-c++ \
    glibc \
    glibc-common \
    glibc-devel \
    glibc-headers \
    kernel-headers \
    libaio \
    libaio-devel \
    libgcc \
    libgomp \
    libstdc++ \
    libstdc++-devel \
    make \
    numactl-devel \
    sysstat \
    libXext.x86_64 \
    compat-libstdc++* \
    ksh \
    compat-libcap1

И вот эти пакеты:

    # yum install -y \
    unixODBC.x86_64 \
    unixODBC-devel.x86_64

Для отображения окон на клиентской машине:

    # yum install -y \
    xdpyinfo \
    xclock

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2, storage</strong></span></td>
</tr>

</table>

    # yum install -y \
    nfs-utils-lib.x86_64

<br/>

### rlwrap

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>

rlwrap - пакет, который позволяет хранить историю команд в SQL\*PLUS и RMAN в Linux (его необходимо прописывать отдельной строкой в bash профиле). Установив данный пакет, вы сможете использовать кнопки вверх, вниз для просмотра истории введенных команд, правильную работу команды backspace и др.

    # yum install -y \
    readline-devel.x86_64

<br/>

    # cd /tmp
    # wget http://utopia.knoware.nl/~hlub/uck/rlwrap/rlwrap-0.37.tar.gz

    # tar zxvf rlwrap-0.37.tar.gz
    # cd rlwrap-0.37
    # ./configure
    # make
    # make check
    # make install
