---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Проверка работы Display Manager на компьютере с GUI
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/check-display-manager/
---



# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Проверка работы Display Manager на компьютере с GUI



# LINUX (Ubuntu)


### Подготовка и проверка

192.168.1.5 -  ip адрес компьютера, с которого происходит процесс управления установкой.<br/>
192.168.1.11 - ip адрес сервера<br/>

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



<br/>

# Windows

Устанавливаем XMing и доп шрифты. :<br/>
http://sourceforge.net/projects/xming/<br/>
http://sourceforge.net/projects/xming/files/Xming-fonts/

Перезагружаемся. Если не перезагрузить, при инсталляции в 10 версии RAC, возникали проблемы (кнопка не отображались на последнем шаге инсталляции).

Далее, необходимо настроить правила доступа.<br/>
В самом простом варианте, правой кнопкой мыши по ярлыку xming. Зайти в свойства и в target дописать -ac (т.е. без контроля доступа)


<img src="http://img.oradba.net/img/oracle/database/simple/12.1/XMing.png" border="0" alt="XMing">


<br/>

### На сервере (на одной из нод):

Проверить работу можно установив xterm или xclock


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


<br/><img src="http://img.oradba.net/img/oracle/database/simple/11.2/xclock.png" border="0" alt="Oracle installation"><br/>

Далее все формы, использующиеся при инсталляции отображаются точно таким же способом.
