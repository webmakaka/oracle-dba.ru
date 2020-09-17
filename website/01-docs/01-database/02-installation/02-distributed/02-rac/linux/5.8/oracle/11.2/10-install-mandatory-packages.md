---
layout: page
title: Oracle RAC 11.2 ISCSI + ASM - Инсталляция необходимых пакетов
permalink: /database/installation/distributed/rac/linux/5.8/oracle/11.2/install-mandatory-packages/
---

# <a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Инсталляция необходимых пакетов

<br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Добавляем репозиторий для инсталляции пакетов</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2, storage</strong></span></td>
</tr>

</table>

    # vi /etc/yum.repos.d/oracleLinuxRepoINTERNET.repo

<br/>

    [OEL_INTERNET]
    name=Oracle Enterprise Linux $releasever - $basearch
    baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL5/latest/x86_64/
    gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-el5
    gpgcheck=1
    enabled=1

<br/>

    # yum repolist

<br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Инсталляция необходимых пакетов</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2 и storage</strong></span></td>
</tr>

</table>

    # yum install -y \
    mc \
    nano \
    gcc \
    make \
    openssh-clients \
    wget \
    xinetd \
    screen \
    vsftpd \
    gamin \
    unzip \
    ntp \
    net-snmp \
    ntsysv

### Инсталляция обязательных пакетов:

Следующие пакеты или более поздние должны быть установлены в OEL 5.x:

    binutils-2.17.50.0.6
    compat-libstdc++-33-3.2.3
    compat-libstdc++-33-3.2.3 (32 bit)
    elfutils-libelf-0.125
    elfutils-libelf-devel-0.125
    gcc-4.1.2
    gcc-c++-4.1.2
    glibc-2.5-24
    glibc-2.5-24 (32 bit)
    glibc-common-2.5
    glibc-devel-2.5
    glibc-devel-2.5 (32 bit)
    glibc-headers-2.5
    ksh-20060214
    libaio-0.3.106
    libaio-0.3.106 (32 bit)
    libaio-devel-0.3.106
    libaio-devel-0.3.106 (32 bit)
    libgcc-4.1.2
    libgcc-4.1.2 (32 bit)
    libstdc++-4.1.2
    libstdc++-4.1.2 (32 bit)
    libstdc++-devel 4.1.2
    make-3.81
    sysstat-7.0.2

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


    WARNING:
    PRVF-7584 : Multiple versions of package "elfutils-libelf-devel" found on node node2: elfutils-libelf-devel(x86_64)-0.137-3.el5,elfutils-libelf-devel(i386)-0.137-3.el5

<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2</strong></span></td>
</tr>

</table>

Я ставлю:

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
    readline-devel.x86_64

И вот эти пакеты:

    # yum install -y \
    unixODBC.i386 \
    unixODBC.x86_64 \
    unixODBC-devel.i386 \
    unixODBC-devel.x86_64

rlwrap - пакет, который позволяет хранить историю команд в SQL\*PLUS и RMAN в Linux (его необходимо прописывать отдельной строкой в bash профиле). Установив данный пакет, вы сможете использовать кнопки вверх, вниз для просмотра истории введенных команд, правильную работу команды backspace и др.

    # cd /tmp
    # wget http://utopia.knoware.nl/~hlub/uck/rlwrap/rlwrap-0.37.tar.gz

<br/>

Если не работает вышеуказанный сайт, исходники можно взять здесь:

    https://github.com/hanslub42/rlwrap

<br/>

    # tar zxvf rlwrap-0.37.tar.gz
    # cd rlwrap-0.37
    # ./configure
    # make
    # make check
    # make install
