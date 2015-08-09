---
layout: page
title: Инсталляция GRID
permalink: /oracle-database-installation/asm/linux/6.7/oracle/12.1/grid-installation/
---


# <a href="/oracle-database-installation/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Инсталляция GRID




Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle12


Копирую дистрибутивы во временный каталог /tmp/oracle/12.1/

	$ cd /tmp/oracle/12.1/

<br/>

	$ ls
	linuxamd64_12102_database_1of2.zip  linuxamd64_12102_grid_1of2.zip
	linuxamd64_12102_database_2of2.zip  linuxamd64_12102_grid_2of2.zip


<br/>

	$ unzip linuxamd64_12102_grid_1of2.zip; unzip linuxamd64_12102_grid_2of2.zip
	$ unzip linuxamd64_12102_database_1of2.zip; unzip linuxamd64_12102_database_2of2.zip

<br/>

	$ cd ~

	$ . asm.sh

Проверка:

	$ echo $ORACLE_SID
	+ASM

<br/>

	$ cd /tmp/oracle/12.1/grid


Определите системную переменную DISPLAY следующим образом.

	$ export DISPLAY=192.168.1.5:0.0

В данном случае 192.168.1.5 - ip адрес компьютера, с которого происходит процесс управления установкой.

	$ ./runInstaller


<br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_01.png" border="0" alt="Grid installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_02.png" border="0" alt="Grid installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_03.png" border="0" alt="Grid installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_04.png" border="0" alt="Grid installation"><br/><br/>



> INS-30011: The string password entered does not conform to the Oracle recommended standards.

> Cause: Oracle recommends that the password entered should be at least string characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].

> Action: Provide a password that conforms to the Oracle recommended standards.



<br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_05.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_06.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_07.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_08.png" border="0" alt="Grid installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_09.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_10.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_11.png" border="0" alt="Grid installation"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_12.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_13.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_14.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_15.png" border="0" alt="Grid installation"><br/><br/>

<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/01-grid-installation/grid-installation_16.png" border="0" alt="Grid installation"><br/><br/>




<br/>

### Проверка работы служб crsctl


	$ crsctl check has
	CRS-4638: Oracle High Availability Services is online


<br/>


	$ crsctl check css
	CRS-4529: Cluster Synchronization Services is online

<br/>



	$ crsctl stat res
	NAME=ora.DATA.dg
	TYPE=ora.diskgroup.type
	TARGET=ONLINE
	STATE=ONLINE on localhost

	NAME=ora.LISTENER.lsnr
	TYPE=ora.listener.type
	TARGET=ONLINE
	STATE=ONLINE on localhost

	NAME=ora.asm
	TYPE=ora.asm.type
	TARGET=ONLINE
	STATE=ONLINE on localhost

	NAME=ora.cssd
	TYPE=ora.cssd.type
	TARGET=ONLINE
	STATE=ONLINE on localhost

	NAME=ora.diskmon
	TYPE=ora.diskmon.type
	TARGET=OFFLINE
	STATE=OFFLINE

	NAME=ora.evmd
	TYPE=ora.evm.type
	TARGET=ONLINE
	STATE=ONLINE on localhost

	NAME=ora.ons
	TYPE=ora.ons.type
	TARGET=OFFLINE
	STATE=OFFLINE

	NAME=ora.ora121.db
	TYPE=ora.database.type
	TARGET=ONLINE
	STATE=ONLINE on localhost


<br/>

	$ ps -fea | grep asm_
	oracle12  1914     1  0 10:17 ?        00:00:00 asm_pmon_+ASM
	oracle12  1916     1  0 10:17 ?        00:00:00 asm_psp0_+ASM
	oracle12  1918     1 10 10:17 ?        00:04:16 asm_vktm_+ASM
	oracle12  1922     1  0 10:17 ?        00:00:02 asm_gen0_+ASM
	oracle12  1924     1  0 10:17 ?        00:00:00 asm_mman_+ASM
	oracle12  1928     1  0 10:17 ?        00:00:00 asm_diag_+ASM
	oracle12  1930     1  0 10:17 ?        00:00:00 asm_dia0_+ASM
	oracle12  1932     1  0 10:17 ?        00:00:00 asm_dbw0_+ASM
	oracle12  1934     1  0 10:17 ?        00:00:00 asm_lgwr_+ASM
	oracle12  1936     1  0 10:17 ?        00:00:00 asm_ckpt_+ASM
	oracle12  1938     1  0 10:17 ?        00:00:00 asm_smon_+ASM
	oracle12  1940     1  0 10:17 ?        00:00:00 asm_lreg_+ASM
	oracle12  1942     1  0 10:17 ?        00:00:00 asm_pxmn_+ASM
	oracle12  1944     1  0 10:17 ?        00:00:00 asm_rbal_+ASM
	oracle12  1946     1  0 10:17 ?        00:00:00 asm_gmon_+ASM
	oracle12  1948     1  0 10:17 ?        00:00:00 asm_mmon_+ASM
	oracle12  1950     1  0 10:17 ?        00:00:00 asm_mmnl_+ASM
	oracle12  7312     1  0 10:50 ?        00:00:00 asm_asmb_+ASM
	oracle12  7765 29253  0 10:57 pts/0    00:00:00 grep asm_



<br/>

	$ sqlplus / as sysdba

	SQL> set linesize 200;
	SQL> set pagesize 0;
	SQL>  col  name format a20;
	SQL>  col  name state a20;

<br/>

	SQL>  select name, state from v$asm_diskgroup;


<br/>

	column path format a30

<br/>

	SQL> select name, path from v$asm_disk;


Для запуска консоли для работы с ASM дисками, выполните команду (если нужно)

	$ asmca
