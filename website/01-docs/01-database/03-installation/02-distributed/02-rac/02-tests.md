---
layout: page
title: Некоторые запросы и команды к RAC
description: Некоторые запросы и команды к RAC
keywords: Некоторые запросы и команды к RAC
permalink: /database/installation/distributed/rac/tests/
---

# Некоторые запросы и команды к RAC

<br/>

```
$ crsctl stat res -t
--------------------------------------------------------------------------------
Name           Target  State        Server                   State details
--------------------------------------------------------------------------------
Local Resources
--------------------------------------------------------------------------------
ora.ASMNET1LSNR_ASM.lsnr
								ONLINE  ONLINE       rac1                     STABLE
								ONLINE  ONLINE       rac2                     STABLE
ora.DATA.dg
								ONLINE  ONLINE       rac1                     STABLE
								ONLINE  ONLINE       rac2                     STABLE
ora.FRA.dg
								ONLINE  ONLINE       rac1                     STABLE
								ONLINE  ONLINE       rac2                     STABLE
ora.LISTENER.lsnr
								ONLINE  ONLINE       rac1                     STABLE
								ONLINE  ONLINE       rac2                     STABLE
ora.OCR.dg
								ONLINE  ONLINE       rac1                     STABLE
								ONLINE  ONLINE       rac2                     STABLE
ora.net1.network
								ONLINE  ONLINE       rac1                     STABLE
								ONLINE  ONLINE       rac2                     STABLE
ora.ons
								ONLINE  ONLINE       rac1                     STABLE
								ONLINE  ONLINE       rac2                     STABLE
--------------------------------------------------------------------------------
Cluster Resources
--------------------------------------------------------------------------------
ora.LISTENER_SCAN1.lsnr
			1        ONLINE  ONLINE       rac2                     STABLE
ora.LISTENER_SCAN2.lsnr
			1        ONLINE  ONLINE       rac1                     STABLE
ora.LISTENER_SCAN3.lsnr
			1        ONLINE  ONLINE       rac1                     STABLE
ora.MGMTLSNR
			1        ONLINE  ONLINE       rac1                     169.254.32.178 192.1
																															68.2.11,STABLE
ora.asm
			1        ONLINE  ONLINE       rac1                     Started,STABLE
			2        ONLINE  ONLINE       rac2                     Started,STABLE
			3        OFFLINE OFFLINE                               STABLE
ora.cvu
			1        ONLINE  ONLINE       rac1                     STABLE
ora.mgmtdb
			1        ONLINE  ONLINE       rac1                     Open,STABLE
ora.oc4j
			1        ONLINE  ONLINE       rac1                     STABLE
ora.rac1.vip
			1        ONLINE  ONLINE       rac1                     STABLE
ora.rac12.db
			1        ONLINE  ONLINE       rac1                     Open,STABLE
			2        ONLINE  ONLINE       rac2                     Open,STABLE
ora.rac2.vip
			1        ONLINE  ONLINE       rac2                     STABLE
ora.scan1.vip
			1        ONLINE  ONLINE       rac2                     STABLE
ora.scan2.vip
			1        ONLINE  ONLINE       rac1                     STABLE
ora.scan3.vip
			1        ONLINE  ONLINE       rac1                     STABLE
--------------------------------------------------------------------------------
```

<br/>

    $ srvctl config database -d rac12
    Database unique name: rac12
    Database name: rac12
    Oracle home: /u01/app/oracle/product/rac/12.1
    Oracle user: oracle12
    Spfile: +DATA/RAC12/PARAMETERFILE/spfile.268.888906665
    Password file: +DATA/RAC12/PASSWORD/pwdrac12.256.888904179
    Domain:
    Start options: open
    Stop options: immediate
    Database role: PRIMARY
    Management policy: AUTOMATIC
    Server pools:
    Disk Groups: DATA,FRA
    Mount point paths:
    Services:
    Type: RAC
    Start concurrency:
    Stop concurrency:
    OSDBA group: dba
    OSOPER group: oper
    Database instances: rac121,rac122
    Configured nodes: rac1,rac2
    Database is administrator managed

<br/>

    $ srvctl config nodeapps -a -g -s
    PRKO-2207 : Warning:-gsdonly option has been deprecated and will be ignored.
    Network 1 exists
    Subnet IPv4: 192.168.1.0/255.255.255.0/eth0, static
    Subnet IPv6:
    Ping Targets:
    Network is enabled
    Network is individually enabled on nodes:
    Network is individually disabled on nodes:
    VIP exists: network number 1, hosting node rac1
    VIP Name: rac1-vip.localdomain
    VIP IPv4 Address: 192.168.1.21
    VIP IPv6 Address:
    VIP is enabled.
    VIP is individually enabled on nodes:
    VIP is individually disabled on nodes:
    VIP exists: network number 1, hosting node rac2
    VIP Name: rac2-vip.localdomain
    VIP IPv4 Address: 192.168.1.22
    VIP IPv6 Address:
    VIP is enabled.
    VIP is individually enabled on nodes:
    VIP is individually disabled on nodes:
    ONS exists: Local port 6100, remote port 6200, EM port 2016, Uses SSL false
    ONS is enabled
    ONS is individually enabled on nodes:
    ONS is individually disabled on nodes:

<br/>

    $ srvctl config listener -a -l LISTENER
    Name: LISTENER
    Type: Database Listener
    Network: 1, Owner: oracle12
    Home: <CRS home>
      /u01/app/grid/12.1 on node(s) rac2,rac1
    End points: TCP:1521
    Listener is enabled.
    Listener is individually enabled on nodes:
    Listener is individually disabled on nodes:

<br/>

    $ srvctl config scan -i 1
    SCAN name: rac12-scan, Network: 1
    Subnet IPv4: 192.168.1.0/255.255.255.0/eth0, static
    Subnet IPv6:
    SCAN 1 IPv4 VIP: 192.168.1.42
    SCAN VIP is enabled.
    SCAN VIP is individually enabled on nodes:
    SCAN VIP is individually disabled on nodes:

<br/>

    $ srvctl status scan
    SCAN VIP scan1 is enabled
    SCAN VIP scan1 is running on node rac2
    SCAN VIP scan2 is enabled
    SCAN VIP scan2 is running on node rac1
    SCAN VIP scan3 is enabled
    SCAN VIP scan3 is running on node rac1

<br/>

    $ srvctl config scan_listener
    SCAN Listener LISTENER_SCAN1 exists. Port: TCP:1521
    Registration invited nodes:
    Registration invited subnets:
    SCAN Listener is enabled.
    SCAN Listener is individually enabled on nodes:
    SCAN Listener is individually disabled on nodes:
    SCAN Listener LISTENER_SCAN2 exists. Port: TCP:1521
    Registration invited nodes:
    Registration invited subnets:
    SCAN Listener is enabled.
    SCAN Listener is individually enabled on nodes:
    SCAN Listener is individually disabled on nodes:
    SCAN Listener LISTENER_SCAN3 exists. Port: TCP:1521
    Registration invited nodes:
    Registration invited subnets:
    SCAN Listener is enabled.
    SCAN Listener is individually enabled on nodes:
    SCAN Listener is individually disabled on nodes:

<br/>

    $ srvctl stop instance -i rac121 -d rac12
    $ srvctl start instance -i rac121 -d rac12

<br/>

    $ srvctl status nodeapps

    VIP node1-vip is enabled
    VIP node1-vip is running on node: node1
    VIP node2-vip is enabled
    VIP node2-vip is running on node: node2
    Network is enabled
    Network is running on node: node1
    Network is running on node: node2
    GSD is disabled
    GSD is not running on node: node1
    GSD is not running on node: node2
    ONS is enabled
    ONS daemon is running on node: node1
    ONS daemon is running on node: node2

<br/>

    $ crs_stat -t

    Name           Type           Target    State     Host
    ------------------------------------------------------------
    ora.DATA.dg    ora....up.type ONLINE    ONLINE    node1
    ora....ER.lsnr ora....er.type ONLINE    ONLINE    node2
    ora....N1.lsnr ora....er.type ONLINE    ONLINE    node1
    ora....N2.lsnr ora....er.type ONLINE    ONLINE    node2
    ora....N3.lsnr ora....er.type ONLINE    ONLINE    node2
    ora.asm        ora.asm.type   ONLINE    ONLINE    node1
    ora.cvu        ora.cvu.type   ONLINE    ONLINE    node2
    ora.gsd        ora.gsd.type   OFFLINE   OFFLINE
    ora....network ora....rk.type ONLINE    ONLINE    node1
    ora....SM1.asm application    ONLINE    ONLINE    node1
    ora....E1.lsnr application    OFFLINE   OFFLINE
    ora.node1.gsd  application    OFFLINE   OFFLINE
    ora.node1.ons  application    ONLINE    ONLINE    node1
    ora.node1.vip  ora....t1.type ONLINE    ONLINE    node1
    ora....SM2.asm application    ONLINE    ONLINE    node2
    ora....E2.lsnr application    ONLINE    ONLINE    node2
    ora.node2.gsd  application    OFFLINE   OFFLINE
    ora.node2.ons  application    ONLINE    ONLINE    node2
    ora.node2.vip  ora....t1.type ONLINE    ONLINE    node2
    ora.oc4j       ora.oc4j.type  ONLINE    ONLINE    node2
    ora.ons        ora.ons.type   ONLINE    ONLINE    node1
    ora....ry.acfs ora....fs.type ONLINE    ONLINE    node1
    ora.scan1.vip  ora....ip.type ONLINE    ONLINE    node1
    ora.scan2.vip  ora....ip.type ONLINE    ONLINE    node2
    ora.scan3.vip  ora....ip.type ONLINE    ONLINE    node2

<br/>

    $ crsctl stat res ora.rac12.db -f
    NAME=ora.rac12.db
    TYPE=ora.database.type
    STATE=ONLINE
    TARGET=ONLINE
    ACL=owner:oracle12:rwx,pgrp:oinstall:r--,other::r--,group:dba:r-x,group:oper:r-x,user:oracle12:r-x
    ACTIONS=startoption,group:"oinstall",user:"oracle12",group:"dba",group:"oper"
    ACTION_SCRIPT=
    ACTION_START_OPTION=
    ACTION_TIMEOUT=600
    ACTIVE_PLACEMENT=0
    AGENT_FILENAME=%CRS_HOME%/bin/oraagent%CRS_EXE_SUFFIX%
    AUTO_START=restore
    CARDINALITY=2
    CARDINALITY_ID=0
    CHECK_INTERVAL=1
    CHECK_TIMEOUT=30
    CLEAN_TIMEOUT=60
    CLUSTER_DATABASE=true
    CONFIG_VERSION=1
    DATABASE_TYPE=RAC
    DB_UNIQUE_NAME=rac12
    DEGREE=1
    DELETE_TIMEOUT=60
    DESCRIPTION=Oracle Database resource
    ENABLED=1
    FAILOVER_DELAY=0
    FAILURE_INTERVAL=60
    FAILURE_THRESHOLD=1
    GEN_AUDIT_FILE_DEST=/u01/app/oracle/admin/rac12/adump
    GEN_START_OPTIONS=
    GEN_USR_ORA_INST_NAME=
    GEN_USR_ORA_INST_NAME@SERVERNAME(rac1)=rac121
    GEN_USR_ORA_INST_NAME@SERVERNAME(rac2)=rac122
    HOSTING_MEMBERS=
    ID=ora.rac12.db
    INSTANCE_COUNT=2
    INSTANCE_FAILOVER=0
    INTERMEDIATE_TIMEOUT=0
    LOAD=1
    LOGGING_LEVEL=1
    MANAGEMENT_POLICY=AUTOMATIC
    MODIFY_TIMEOUT=60
    NLS_LANG=
    OFFLINE_CHECK_INTERVAL=0
    ONLINE_RELOCATION_TIMEOUT=0
    ORACLE_HOME=/u01/app/oracle/product/rac/12.1
    ORACLE_HOME_OLD=
    PLACEMENT=restricted
    PWFILE=+DATA/RAC12/PASSWORD/pwdrac12.256.888904179
    RANK=0
    RELOCATE_ACTION=0
    RELOCATE_BY_DEPENDENCY=1
    RESTART_ATTEMPTS=2
    ROLE=PRIMARY
    SCRIPT_TIMEOUT=60
    SERVER_CATEGORY=
    SERVER_POOLS=ora.rac12
    SERVER_POOLS_PQ=
    SPFILE=+DATA/RAC12/PARAMETERFILE/spfile.268.888906665
    START_CONCURRENCY=0
    START_DEPENDENCIES=hard(global:uniform:ora.DATA.dg, global:uniform:ora.FRA.dg) pullup(global:ora.DATA.dg, global:ora.FRA.dg) weak(type:ora.listener.type,global:type:ora.scan_listener.type,uniform:ora.ons,global:ora.gns)
    START_TIMEOUT=600
    STOP_CONCURRENCY=0
    STOP_DEPENDENCIES=hard(global:intermediate:ora.asm,global:shutdown:ora.DATA.dg,global:shutdown:ora.FRA.dg)
    STOP_TIMEOUT=600
    TYPE_VERSION=3.3
    UPTIME_THRESHOLD=1h
    USER_WORKLOAD=yes
    USE_STICKINESS=0
    USR_ORA_DB_NAME=rac12
    USR_ORA_DOMAIN=
    USR_ORA_ENV=
    USR_ORA_FLAGS=
    USR_ORA_INST_NAME=
    USR_ORA_INST_NAME@SERVERNAME(rac1)=rac121
    USR_ORA_INST_NAME@SERVERNAME(rac2)=rac122
    USR_ORA_OPEN_MODE=open
    USR_ORA_OPI=false
    USR_ORA_STOP_MODE=immediate

<br/>

    $ crsctl query css votedisk
    ##  STATE    File Universal Id                File Name Disk group
    --  -----    -----------------                --------- ---------
    1. ONLINE   1f5590501e834f00bfffb717022f5746 (ORCL:ASMDISK1) [OCR]
    2. ONLINE   effa884850594f98bf43e29bd20fbb0b (ORCL:ASMDISK2) [OCR]
    3. ONLINE   e639ffd640c74ff2bf148cfe0d432463 (ORCL:ASMDISK3) [OCR]
    Located 3 voting disk(s).

<br/>

    $ olsnodes -n -i -s -t
    rac1	1	rac1-vip.localdomain	Active	Unpinned
    rac2	2	rac2-vip.localdomain	Active	Unpinned

<br/>

    $ oifcfg getif
    eth0  192.168.1.0  global  public
    eth1  192.168.2.0  global  cluster_interconnect,asm

<br/>

    $ ocrcheck
    Status of Oracle Cluster Registry is as follows :
    	 Version                  :          4
    	 Total space (kbytes)     :     409568
    	 Used space (kbytes)      :       1688
    	 Available space (kbytes) :     407880
    	 ID                       : 1367113341
    	 Device/File Name         :       +OCR
                                        Device/File integrity check succeeded

                                        Device/File not configured

                                        Device/File not configured

                                        Device/File not configured

                                        Device/File not configured

    	 Cluster registry integrity check succeeded

    	 Logical corruption check bypassed due to non-privileged user

<br/>

    $ ocrconfig -showbackup

    rac1     2015/08/28 20:40:20     /u01/app/grid/12.1/cdata/rac12/backup00.ocr     0

    rac1     2015/08/28 16:40:19     /u01/app/grid/12.1/cdata/rac12/backup01.ocr     0

    rac1     2015/08/28 12:40:19     /u01/app/grid/12.1/cdata/rac12/backup02.ocr     0

    rac1     2015/08/28 08:40:18     /u01/app/grid/12.1/cdata/rac12/day.ocr     0

    rac1     2015/08/28 08:40:18     /u01/app/grid/12.1/cdata/rac12/week.ocr     0
    PROT-25: Manual backups for the Oracle Cluster Registry are not available

<br/>

    $ cluvfy comp nodecon -n all

    Verifying node connectivity

    Checking node connectivity...

    Checking hosts config file...

    Verification of the hosts config file successful

    Node connectivity passed for subnet "192.168.1.0" with node(s) node2,node1
    TCP connectivity check passed for subnet "192.168.1.0"

    Node connectivity passed for subnet "192.168.2.0" with node(s) node2,node1
    TCP connectivity check passed for subnet "192.168.2.0"

    Node connectivity passed for subnet "169.254.0.0" with node(s) node2,node1
    TCP connectivity check passed for subnet "169.254.0.0"

    Node connectivity passed for subnet "192.168.3.0" with node(s) node2,node1
    TCP connectivity check passed for subnet "192.168.3.0"


    Interfaces found on subnet "192.168.1.0" that are likely candidates for VIP are:
    node2 eth0:192.168.1.12 eth0:192.168.1.22 eth0:192.168.1.33 eth0:192.168.1.31
    node1 eth0:192.168.1.11 eth0:192.168.1.21 eth0:192.168.1.32

    Interfaces found on subnet "169.254.0.0" that are likely candidates for VIP are:
    node2 eth1:169.254.128.142
    node1 eth1:169.254.214.68

    Interfaces found on subnet "192.168.2.0" that are likely candidates for a private interconnect are:
    node2 eth1:192.168.2.12
    node1 eth1:192.168.2.11

    Interfaces found on subnet "192.168.3.0" that are likely candidates for a private interconnect are:
    node2 eth2:192.168.3.12
    node1 eth2:192.168.3.11
    Checking subnet mask consistency...
    Subnet mask consistency check passed for subnet "192.168.1.0".
    Subnet mask consistency check passed for subnet "192.168.2.0".
    Subnet mask consistency check passed for subnet "169.254.0.0".
    Subnet mask consistency check passed for subnet "192.168.3.0".
    Subnet mask consistency check passed.

    Node connectivity check passed


    Verification of node connectivity was successful.

<br/>

    srvctl

    Usage: srvctl <command> <object> [<options>]
        command: enable|disable|start|stop|relocate|status|add|remove|modify|getenv|setenv|unsetenv|config
        objects: database|instance|service|nodeapps|asm|listener
    For detailed help on each command and object and its options use:
        srvctl <command> <object> -h

<br/>

    srvctl -h

    Usage: srvctl [-V]
    Usage: srvctl add database -d <name> -o <oracle_home> [-m <domain_name>] [-p <spfile>] [-A <name|ip>/netmask] [-r {PRIMARY | PHYSICAL_STANDBY | LOGICAL_STANDBY}] [-s <start_options>] [-n <db_name>] [-y {AUTOMATIC | MANUAL}]
    Usage: srvctl add instance -d <name> -i <inst_name> -n <node_name>
    Usage: srvctl add service -d <name> -s <service_name> -r "<preferred_list>" [-a "<available_list>"] [-P <TAF_policy>]
    Usage: srvctl add service -d <name> -s <service_name> -u {-r "<new_pref_inst>" | -a "<new_avail_inst>"}
    Usage: srvctl add nodeapps -n <node_name> -o <oracle_home> -A <name|ip>/netmask[/if1[|if2|...]]
    Usage: srvctl add asm -n <node_name> -i <asm_inst_name> -o <oracle_home> [-p <spfile>]
    Usage: srvctl config database
    Usage: srvctl config database -d <name> [-a] [-t]
    Usage: srvctl config service -d <name> [-s <service_name>] [-a] [-S <level>]
    Usage: srvctl config nodeapps -n <node_name> [-a] [-g] [-o] [-s] [-l]
    Usage: srvctl config asm -n <node_name>
    Usage: srvctl config listener -n <node_name>
    Usage: srvctl disable database -d <name>
    Usage: srvctl disable instance -d <name> -i "<inst_name_list>"
    Usage: srvctl disable service -d <name> -s "<service_name_list>" [-i <inst_name>]
    Usage: srvctl disable asm -n <node_name> [-i <inst_name>]
    Usage: srvctl enable database -d <name>
    Usage: srvctl enable instance -d <name> -i "<inst_name_list>"
    Usage: srvctl enable service -d <name> -s "<service_name_list>" [-i <inst_name>]
    Usage: srvctl enable asm -n <node_name> [-i <inst_name>]
    Usage: srvctl getenv database -d <name> [-t "<name_list>"]
    Usage: srvctl getenv instance -d <name> -i <inst_name> [-t "<name_list>"]
    Usage: srvctl getenv service -d <name> -s <service_name> [-t "<name_list>"]
    Usage: srvctl getenv nodeapps -n <node_name> [-t "<name_list>"]
    Usage: srvctl modify database -d <name> [-n <db_name] [-o <ohome>] [-m <domain>] [-p <spfile>]  [-r {PRIMARY | PHYSICAL_STANDBY | LOGICAL_STANDBY}] [-s <start_options>] [-y {AUTOMATIC | MANUAL}]
    Usage: srvctl modify instance -d <name> -i <inst_name> -n <node_name>
    Usage: srvctl modify instance -d <name> -i <inst_name> {-s <asm_inst_name> | -r}
    Usage: srvctl modify service -d <name> -s <service_name> -i <old_inst_name> -t <new_inst_name> [-f]
    Usage: srvctl modify service -d <name> -s <service_name> -i <avail_inst_name> -r [-f]
    Usage: srvctl modify service -d <name> -s <service_name> -n -i <prefered_inst> [-a <available_list>] [-f]
    Usage: srvctl modify asm -n <node_name> -i <asm_inst_name> -p <spfile>
    Usage: srvctl relocate service -d <name> -s <service_name> -i <old_inst_name> -t <new_inst_name> [-f]
    Usage: srvctl remove database -d <name> [-f]
    Usage: srvctl remove instance -d <name> -i <inst_name> [-f]
    Usage: srvctl remove service -d <name> -s <service_name> [-i <inst_name>] [-f]
    Usage: srvctl remove nodeapps -n "<node_name_list>" [-f]
    Usage: srvctl remove asm -n <node_name> [-i <asm_inst_name>] [-f]
    Usage: srvctl setenv database -d <name> {-t <name>=<val>[,<name>=<val>,...] | -T <name>=<val>}
    Usage: srvctl setenv instance -d <name> [-i <inst_name>] {-t "<name>=<val>[,<name>=<val>,...]" | -T "<name>=<val>"}
    Usage: srvctl setenv service -d <name> [-s <service_name>] {-t "<name>=<val>[,<name>=<val>,...]" | -T "<name>=<val>"}
    Usage: srvctl setenv nodeapps -n <node_name> {-t "<name>=<val>[,<name>=<val>,...]" | -T "<name>=<val>"}
    Usage: srvctl start database -d <name> [-o <start_options>] [-c <connect_str> | -q]
    Usage: srvctl start instance -d <name> -i "<inst_name_list>" [-o <start_options>] [-c <connect_str> | -q]
    Usage: srvctl start service -d <name> [-s "<service_name_list>" [-i <inst_name>]] [-o <start_options>] [-c <connect_str> | -q]
    Usage: srvctl start nodeapps -n <node_name>
    Usage: srvctl start asm -n <node_name> [-i <asm_inst_name>] [-o <start_options>] [-c <connect_str> | -q]
    Usage: srvctl start listener -n <node_name> [-l <lsnr_name_list>]
    Usage: srvctl status database -d <name> [-f] [-v] [-S <level>]
    Usage: srvctl status instance -d <name> -i "<inst_name_list>" [-f] [-v] [-S <level>]
    Usage: srvctl status service -d <name> [-s "<service_name_list>"] [-f] [-v] [-S <level>]
    Usage: srvctl status nodeapps -n <node_name>
    Usage: srvctl status asm -n <node_name>
    Usage: srvctl stop database -d <name> [-o <stop_options>] [-c <connect_str> | -q]
    Usage: srvctl stop instance -d <name> -i "<inst_name_list>" [-o <stop_options>] [-c <connect_str> | -q]
    Usage: srvctl stop service -d <name> [-s "<service_name_list>" [-i <inst_name>]] [-c <connect_str> | -q] [-f]
    Usage: srvctl stop nodeapps -n <node_name>
    Usage: srvctl stop asm -n <node_name> [-i <asm_inst_name>] [-o <stop_options>] [-c <connect_str> | -q]
    Usage: srvctl stop listener -n <node_name> [-l <lsnr_name_list>]
    Usage: srvctl unsetenv database -d <name> -t "<name_list>"
    Usage: srvctl unsetenv instance -d <name> [-i <inst_name>] -t "<name_list>"
    Usage: srvctl unsetenv service -d <name> [-s <service_name>] -t "<name_list>"
    Usage: srvctl unsetenv nodeapps -n <node_name> -t "<name_list>"

<br/>

    srvctl config database -d racnode
    srvctl status database -d racnode
    srvctl config scan
    srvctl status nodeapps

<br/>

    $ srvctl stop scan
    $ srvctl status scan_listener
    $ srvctl stop scan_listener
    $ srvctl status scan

<br/>

    $ crsctl check cluster -all
    **************************************************************
    rac1:
    CRS-4537: Cluster Ready Services is online
    CRS-4529: Cluster Synchronization Services is online
    CRS-4533: Event Manager is online
    **************************************************************
    rac2:
    CRS-4537: Cluster Ready Services is online
    CRS-4529: Cluster Synchronization Services is online
    CRS-4533: Event Manager is online
    **************************************************************



    ./crsctl start resource -all

<br/>

    cd /tmp/grid
    ./runcluvfy.sh stage -post crsinst -n rac1,rac2 -verbose

<br/>

    $ ocrcheck

    Status of Oracle Cluster Registry is as follows :
             Version                  :          3
             Total space (kbytes)     :     262120
             Used space (kbytes)      :       2596
             Available space (kbytes) :     259524
             ID                       :   13470289
             Device/File Name         :      +DATA
                                        Device/File integrity check failed

                                        Device/File not configured

                                        Device/File not configured

                                        Device/File not configured

                                        Device/File not configured

             Cluster registry integrity check failed

             Logical corruption check bypassed due to insufficient quorum

<br/>

    srvctl status scan

<br/>

    srvctl config scan_listener

<br/>

    srvctl status scan_listener

<br/>

    Verifying local resources that are online
    crsctl stat res -init -t -w "STATE = ONLINE"

<br/>

    Check Cluster Resources that are offline
    crsctl stat res -t -w "STATE = OFFLINE"

<br/>

    srvctl status scan

http://sosdba.wordpress.com/tag/11g/
