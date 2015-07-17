---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /oracle_database_installation/rac/linux/5.8/oracle/11.2/tests/
---

# <a href="/oracle_database_installation/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Некоторые запросы и команды

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

	./crsctl check cluster -all
	./crsctl stat res -t
	./crsctl start resource -all

<br/>

	cd /tmp/grid
	./runcluvfy.sh stage -post crsinst -n devsp037,devsp037 -verbose

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

	$ srvctl config scan

	SCAN name: devsp037-scan.netcracker.com, Network: 1/10.232.0.0/255.255.0.0/eth0
	SCAN VIP name: scan1, IP: /devsp037-scan.netcracker.com/10.232.2.204
	SCAN VIP name: scan2, IP: /devsp037-scan.netcracker.com/10.232.2.205
	SCAN VIP name: scan3, IP: /devsp037-scan.netcracker.com/10.232.2.206


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
