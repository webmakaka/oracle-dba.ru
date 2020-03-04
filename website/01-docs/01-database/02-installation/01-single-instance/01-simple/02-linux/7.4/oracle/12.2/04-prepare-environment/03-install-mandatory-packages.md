---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Инсталляция обязательных пакетов
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/install-mandatory-packages/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>:: Инсталляция обязательных пакетов


<br/>

База данных Oracle, требует, чтобы в системе были обязательно установлены некоторые компоненты. Пакеты можно скачать с публичного репозитория (из интернет) или взять с диска, на котором и располагается дистрибутив операционной системы.

<strong>Должен отметить, что на самом деле, сервер не должен иметь возможность выхода в интернет!</strong> Для установки пакетов, нужно поднимать локальный репозиторий и уже с него получать нужные пакеты. Более того, по хорошему, на сервере не должно быть никаких ненужных пакетов.


<br/>

**Инсталляция пакетов из репозитория Oracle Linux в интернете:**

Шаг следует выполнять, если в файловой системе нет файла с описанием, где Oracle Linux должен брать нужные пакеты. При установке от и до по этой инструкции, его выполнять не нужно.

	# vi /etc/yum.repos.d/oracleLinuxRepoINTERNET.repo

<br/>

    [OEL_INTERNET]
    name=Oracle Enterprise Linux $releasever - $basearch
    baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/latest/$basearch/
    gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol7
    gpgcheck=1
    enabled=1

<br/>

	# yum repolist


<br/>

### Обновление пакетов

	# yum update -y

<br/>


Следующие пакеты должны быть установлены:   (http://docs.oracle.com/cd/E16655_01/install.121/e17718/toc.htm#BABGGEBA)

binutils-2.20.51.0.2-5.11.el6 (x86_64)<br/>
compat-libcap1-1.10-1 (x86_64)<br/>
compat-libstdc++-33-3.2.3-69.el6 (x86_64)<br/>
compat-libstdc++-33-3.2.3-69.el6.i686<br/>
gcc-4.4.4-13.el6 (x86_64)<br/>
gcc-c++-4.4.4-13.el6 (x86_64)<br/>
glibc-2.12-1.7.el6 (i686)<br/>
glibc-2.12-1.7.el6 (x86_64)<br/>
glibc-devel-2.12-1.7.el6 (x86_64)<br/>
glibc-devel-2.12-1.7.el6.i686<br/>
ksh<br/>
libgcc-4.4.4-13.el6 (i686)<br/>
libgcc-4.4.4-13.el6 (x86_64)<br/>
libstdc++-4.4.4-13.el6 (x86_64)<br/>
libstdc++-4.4.4-13.el6.i686<br/>
libstdc++-devel-4.4.4-13.el6 (x86_64)<br/>
libstdc++-devel-4.4.4-13.el6.i686<br/>
libaio-0.3.107-10.el6 (x86_64)<br/>
libaio-0.3.107-10.el6.i686<br/>
libaio-devel-0.3.107-10.el6 (x86_64)<br/>
libaio-devel-0.3.107-10.el6.i686<br/>
make-3.81-19.el6<br/>
sysstat-9.0.4-11.el6 (x86_64)<br/>


<br/><br/>

Посмотреть пакеты в репозитории можно следующей командой:

	# yum search all binutils

<br/>

Инсталляция всех необходимых пакетов одной командой:

	# yum install -y \
	binutils.x86_64 \
	compat-libcap1.x86_64 \
	compat-libstdc++-33.i686 \
	compat-libstdc++-33.x86_64 \
	gcc.x86_64 \
	gcc-c++.x86_64 \
	glibc.i686 \
	glibc.x86_64 \
	glibc-devel.i686 \
	glibc-devel.x86_64 \
	ksh.x86_64 \
	libgcc.i686 \
	libgcc.x86_64 \
	libstdc++.i686 \
	libstdc++.x86_64 \
	libstdc++-devel.i686 \
	libstdc++-devel.x86_64 \
	libaio.i686 \
	libaio.x86_64 \
	libaio-devel.i686 \
	libaio-devel.x86_64 \
	make.x86_64 \
	sysstat.x86_64

<br/>

Для версии 12.2 теперь также нужен следующий пакет:

    # yum install -y smartmontools


<br/>


Следующий пакет нужен для старта графической консоли

    # yum install -y \
	xdpyinfo

<br/>

Дополнительные пакеты, не являющиеся необходимыми для инсталляции базы данных:

    # yum install -y \
    vim \
    wget \
    xinetd \
    screen \
    ntp \
    unzip

<br/>

### Инсталляция rlwrap

rlwrap - пакет, который позволяет хранить историю команд в SQL*PLUS и RMAN в Linux (его необходимо прописывать отдельной строкой в bash профиле). Установив данный пакет, вы сможете использовать кнопки вверх, вниз для просмотра истории введенных команд, правильную работу команды backspace и др.

	# yum install -y \
	readline-devel.x86_64

<br/>

    # yum install -y git
    # cd /tmp
    # git clone --depth=1 https://github.com/hanslub42/rlwrap

    # cd rlwrap/

<br/>

	# yum install -y gcc
    # yum install -y automake
    # autoreconf --install
    # automake  --add-missing
    # ./configure
    # make && make check && make install
