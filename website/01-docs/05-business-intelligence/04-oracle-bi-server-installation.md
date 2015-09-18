---
layout: page
title: Инсталляция Oracle BI EE (OBIEE)
permalink: /docs/business-intelligence/oracle-bi-server-installation/
---



<h2>Инсталляция Oracle BI EE (OBIEE)</h2>

	# mkdir -p /u01/app/oracle/oraclebi/11.1
	# mkdir -p /u01/app/oracle/oraclebi/oraInventory
	# chown -R oraclebi:oraclebi /u01/app/oracle/oraclebi
	# chmod -R 775 /u01/app/oracle/oraclebi

<br/>

	# mkdir -p /u02/oracle_bi_domains/bifoundation_domain
	# chown -R oraclebi:oraclebi  /u02/oracle_bi_domains



Следующие пакеты должны быть установлены на OEL6:


	# yum install -y \
	binutils.x86_64 \
	compat-libcap1 \
	list compat-libstdc++-33 \
	gcc \
	gcc-c++ \
	glibc \
	glibc-devel \
	libaio \
	libaio-devel \
	libgcc \
	libstdc++ \
	libstdc++-devel \
	libXext.i686 \
	libXtst.i686 \
	openmotif.x86_64 \
	redhat-lsb-core.x86_64 \
	openmotif-2.2.3.x86_64 \
	openmotif22.x86_64 \
	sysstat

<br/>

	# yum list binutils


-- uln-internal-setup - Не нашел в стандартном репозитории, в остальных искать не стал.



Копирую на сервер в каталог /tmp/_oralce_bi


	bi_linux_x86_111170_64_disk1_1of2.zip
	bi_linux_x86_111170_64_disk1_2of2.zip
	bi_linux_x86_111170_64_disk2_1of2.zip
	bi_linux_x86_111170_64_disk2_2of2.zip
	bi_linux_x86_111170_64_disk3.zip


и разархивирую


	$ unzip bi_linux_x86_111170_64_disk1_1of2.zip; \
	bi_linux_x86_111170_64_disk1_2of2.zip; \
	bi_linux_x86_111170_64_disk2_1of2.zip; \
	bi_linux_x86_111170_64_disk2_2of2.zip; \
	bi_linux_x86_111170_64_disk3.zip


Если не разархивировать все архивы, в процессе инсталляции появится сообщение с предложением указать источник нахождения нужных для инсталляции файлов.

<br/><br/>

<img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation-next-disk.png" alt="oracle bi installation"><br/><br/>



	$ cd bishiphome/Disk1/



<br/>

	$ export DISPLAY=192.168.1.5:0.0

<br/>

	$ ./runInstaller


<br/><br/>


<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_01.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_02.png" alt="oracle bi installation"><br/><br/>


	# cd /u01/app/oracle/oraclebi/oraInventory/
	# ./createCentralInventory.sh



Данные которые я вводил:<br/><br/>

Oracle Middleware Home: /u01/app/oracle/oraclebi/11.1<br/>
Domai Home Location: /u02/oracle_bi_domains/bifoundation_domain<br/>
Oracle Instance Location: /u01/app/oracle/oraclebi/11.1/instance1<br/>
Oracle Instance Name: Instance1<br/><br/>


Connect String: oracle112:1521:ora112.localdomain<br/>
BIPLATFORM Schema Username: dev_biplatform<br/><br/>

MD5 Schema Username: dev_MDS

<br/><br/>


<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_03.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_04.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_05.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_06.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_07.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_08.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_09.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_10.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_11.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_12.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_13.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_14.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_15.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_16.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_17.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_18.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_19.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_20.png" alt="oracle bi installation"><br/><br/>

<br/><br/>

<pre>

Type: Enterprise Install - Create New BI System
        Installation Details
                Middleware Home: /u01/app/oracle/oraclebi/11.1
                BI Oracle Home: /u01/app/oracle/oraclebi/11.1/Oracle_BI1
                WebLogic Server Home: /u01/app/oracle/oraclebi/11.1/wlserver_10.3
                BI Domain Home: /u02/oracle_bi_domains/bifoundation_domain
                BI Domain Name: bifoundation_domain
                Instance Home: /u01/app/oracle/oraclebi/11.1/instance1
                Instance Name: instance1
        Configure Components
                WebLogic Console
                        http://oraclebi.localdomain:7001/console
                Oracle Enterprise Manager
                        http://oraclebi.localdomain:7001/em
                Business Intelligence Enterprise Edition
                        http://oraclebi.localdomain:9704/analytics
                Business Intelligence Publisher
                        http://oraclebi.localdomain:9704/xmlpserver
                Real-Time Decisions
                        http://oraclebi.localdomain:9704/ui
                Calculation Manager
                        http://oraclebi.localdomain:9704/workspace
                Financial Reports
                        http://oraclebi.localdomain:9704/workspace
                Workspace
                        http://oraclebi.localdomain:9704/workspace
                Essbase Suite
                APS
                        http://oraclebi.localdomain:9704/aps
                Essbase Server
                Essbase Studio
                        oraclebi.localdomain
                Essbase Administration Services
                        oraclebi.localdomain:9704



</pre>



<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_21.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_22.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_23.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_24.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_25.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_26.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_27.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_28.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_29.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_30.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_31.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_32.png" alt="oracle bi installation"><br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/oracle-bi-installation/oracle-bi-installation_33.png" alt="oracle bi installation"><br/><br/>
