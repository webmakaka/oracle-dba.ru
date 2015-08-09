---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /oracle-database-installation/linux/6.3/oracle/11.2/install-mandatory-packages/
---

# <a href="/oracle-database-installation/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>:  Инсталляция обязательных пакетов




База данных Oracle, требует, чтобы в системе были обязательно установлены некоторые компоненты. Пакеты можно скачать с публичного репозитория (из интернет) или взять с диска, на котором и располагается дистрибутив операционной системы.

<br/>

**Вариант 1: Инсталляция пакетов с DVD диска Oracle Linux (Не рекомендуется):**

	# mkdir /mnt/cdrom
	# mount -t iso9660 -o ro /dev/cdrom /mnt/cdrom

<br/>

	# vi /etc/yum.repos.d/oracleLinuxRepoDVD.repo

<br/>

    [OEL63_DVD]
    name=Oracle Enterprise Linux DVD
    baseurl=file:///mnt/cdrom/Server/
    gpgcheck=0
    enabled=1


<br/>

**Вариант 2: Инсталляция пакетов из репозитория Oracle Linux в интернете:**

	# vi /etc/yum.repos.d/oracleLinuxRepoINTERNET.repo

<br/>

    [OEL_INTERNET]
    name=Oracle Enterprise Linux $releasever - $basearch
    baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/latest/$basearch/
    gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
    gpgcheck=1
    enabled=1


<br/>

	# yum repolist
	# yum update -y

<br/>


======================================<br/><br/>

Offtopic: (Рекомендуется пропустить! Просто для информации)<br/><br/>

Вы можете выполнить следующую команду и пропустить большую часть шагов по установке необходимых пакетов и правильной настройке окружения для инсталляции Oracle.<br/><br/>

    # yum install -y oracle-validated <br/><br/>

Выполнив данную команду, Oracle сам инсталлирует все необходимые пакеты, создаст необходимых пользователей, внесет изменения в конфигурационные файлы.

Имеется только один минус, возможно, что он сделает не все так как вы хотите. Т.е. будет выполнена подготовка окружения “по умолчанию”.

======================================<br/><br/>

Следующие пакеты должны быть установлены: <br/><br/>

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

Следующий пакет нужен для старта графической консоли

    # yum install -y xdpyinfo

<br/>

Дополнительные пакеты:


	# yum install -y \
		mc \
		nano \
		vim \
		emacs \
		wget \
		xinetd \
		screen \
		ntp \
		unzip

rlwrap - пакет, который позволяет хранить историю команд в SQL*PLUS и RMAN в Linux (его необходимо прописывать отдельной строкой в bash профиле). Установив данный пакет, вы сможете использовать кнопки вверх, вниз для просмотра истории введенных команд, правильную работу команды backspace и др.


    # yum install -y \
	readline-devel.x86_64

<br/>

	# cd /tmp
	# wget http://utopia.knoware.nl/~hlub/uck/rlwrap/rlwrap-0.37.tar.gz

<br/>


	# tar zxvf rlwrap-0.37.tar.gz
	# cd rlwrap-0.37
	# ./configure
	# make
	# make check
	# make instal
