---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /oracle-database-installation/linux/6.4/oracle/12.1/setup-display-manager/
---

# <a href="/oracle-database-installation/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Настройка Display Manger



### Подготовка и проверка

192.168.1.5 -  ip адрес компьютера, с которого происходит процесс управления установкой.<br/>
192.168.1.10 - ip адрес сервера<br/>

### На клиенте:

	$ sudo apt-get install -y gdm



<br/><img src="http://img.oradba.net/img/oracle/database/simple/11.2/gdm.png" border="0" alt="Oracle installation"><br/>


### Если выбран gdm

	# vi /etc/gdm/custom.conf

<br/>

	###########################
	[xdmcp]

	[chooser]

	[security]
	DisallowTCP=false

	[debug]
	###########################



### Если выбран lightgdm


	# vi /etc/lightdm/lightdm.conf

<br/>

	###########################

	[SeatDefaults]
	user-session=ubuntu
	greeter-session=unity-greeter
	xserver-allow-tcp=true

	###########################

<br/>

	# reboot


### Команды проверки


	$ sudo apt-get install -y nmap nc

<br/>

	$ netstat -an | grep -F 6000

<br/>

	tcp        0      0 0.0.0.0:6000            0.0.0.0:*               LISTEN
	tcp6       0      0 :::6000                 :::*                    LISTEN


<br/>

	# nmap -p 6000 192.168.1.5

<br/>

	Starting Nmap 5.21 ( http://nmap.org ) at 2013-08-18 04:13 MSK
	Nmap scan report for 192.168.1.5
	Host is up (0.000044s latency).
	PORT     STATE SERVICE
	6000/tcp open  X11


<br/>

	$ nc -vv 192.168.1.5 6000
	Connection to 192.168.1.200 6000 port [tcp/x11] succeeded!=


<br/>

	$ xhost +192.168.1.10


### На сервере:

Проверить работу можно установив xterm или xclock

<br/>


-- если не установили ранее, установите пакет xdpyinfo. Он нужен для отображения окон на клиентской машине.


	# yum install -y xdpyinfo

<br/>

	# yum install -y xclock

<br/>

	$ export DISPLAY=192.168.1.5:0.0

<br/>

	$ xclock

-- можно даже проще, просто выполните команду:

	$ xclock -display 192.168.1.5:0

<br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/database/simple/11.2/xclock.png" border="0" alt="Oracle installation"><br/>

<br/><br/>
Если процесс управления инсталляцией проводится на машине с операионной системой windows, то смотри

<a href="/oracle-database-installation/linux/6.3/oracle/11.2/oracle-database-software-installation/">здесь</a>.
