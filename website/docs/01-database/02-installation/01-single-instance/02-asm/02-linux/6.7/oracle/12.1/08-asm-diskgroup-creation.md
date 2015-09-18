---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Создание дисковых групп ASM
permalink: /database/installation/single/asm/linux/6.7/oracle/12.1/asm-diskgroup-creation/
---


# <a href="/database/installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Инсталляция GRID





Для запуска консоли для работы с ASM дисками, выполните команду (если нужно)

	$ asmca


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/02-asm-diskgroup/asm-diskgroup_01.png" border="0" alt="ASM DISKGROUPS"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/02-asm-diskgroup/asm-diskgroup_02.png" border="0" alt="ASM DISKGROUPS"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/02-asm-diskgroup/asm-diskgroup_03.png" border="0" alt="ASM DISKGROUPS"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/02-asm-diskgroup/asm-diskgroup_04.png" border="0" alt="ASM DISKGROUPS"><br/><br/>


<img src="http://img.oradba.net/oracle-database-installation/asm/linux/6.7/oracle/12.1/02-asm-diskgroup/asm-diskgroup_05.png" border="0" alt="ASM DISKGROUPS"><br/><br/>



Просто получить какую-то информацию о дисковых группах

	$ asmcmd

	ASMCMD> ls
	ARCH/
	DATA/


	ASMCMD> lsdg
	State    Type    Rebal  Sector  Block       AU  Total_MB  Free_MB  Req_mir_free_MB  Usable_file_MB  Offline_disks  Voting_files  Name
	MOUNTED  NORMAL  N         512   4096  1048576     81918    81810                0           40905              0             N  ARCH/
	MOUNTED  NORMAL  N         512   4096  1048576    163836   163645            40959           61343              0             N  DATA/


	ASMCMD> exit
