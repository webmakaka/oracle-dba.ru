---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Настройка Display Manger
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/setup-display-manager/
---


<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>:: Настройка Display Manger

<br/>

### Подготовка и проверка

192.168.1.5 -  ip адрес компьютера, с которого происходит процесс управления установкой.<br/>
192.168.56.101 - ip адрес сервера<br/>


<br/>

## Если установка происходит с Windows машины

Устанавливаем XMing и доп шрифты. :<br/>
http://sourceforge.net/projects/xming/<br/>
http://sourceforge.net/projects/xming/files/Xming-fonts/

Перезагружаемся. Если не перезагрузить, при инсталляции в 10 версии RAC, возникали проблемы (кнопка не отображались на последнем шаге инсталляции).

Далее, необходимо настроить правила доступа.<br/>
В самом простом варианте, правой кнопкой мыши по ярлыку xming. Зайти в свойства и в target дописать -ac (т.е. без контроля доступа)

<br/>

<div align="center">
    <img src="http://img.oradba.net/img/oracle/database/simple/12.1/XMing.png" border="0" alt="XMing">
</div>


<br/>

## Если установка происходит с Linux машины

<br/>

### Подготовка клиента Oracle Linux 7.3 с gnome environment


    # yum install -y nmap nc xclock

<br/>

	# vi /etc/gdm/custom.conf

<br/>

Добавляю в блоки:

    [security]
    DisallowTCP=false

    [xdmcp]
    Enable=true


<br/>

    # service gdm restart


<br/>

    $ xclock -display 192.168.1.5:0


Если часы появились, все ок и больше ничего не нужно.

<br/>

<div align="center">
    <img src="http://img.oradba.net/img/oracle/database/simple/11.2/xclock.png" border="0" alt="Oracle installation">
</div>

<br/>


<br/>

### Подготовка клиента Ubuntu


$ sudo apt-get install -y nmap nc xclock


<div align="center">
<img src="http://img.oradba.net/img/oracle/database/simple/11.2/gdm.png" border="0" alt="Oracle installation">
</div>


<br/>

Вариант с lightdm.

Если что, можно потом переключиться командами:

<br/>

    # dpkg-reconfigure gdm
    # dpkg-reconfigure lightdm


<br/>

	# vi /etc/lightdm/lightdm.conf

<br/>


{% highlight shell %}

###########################

[SeatDefaults]
user-session=ubuntu
greeter-session=unity-greeter
xserver-allow-tcp=true

###########################

{% endhighlight %}


<br/>

    # sudo restart lightdm

<br/>

    $ xclock -display 192.168.1.5:0

Если часы появились, все ок и больше ничего не нужно.


<br/>

<div align="center">
    <img src="http://img.oradba.net/img/oracle/database/simple/11.2/xclock.png" border="0" alt="Oracle installation">
</div>

<br/>


<br/>

### Если часы не появились:

    $ ps ax | grep dm
    $ ps lf -C Xorg


Не должно быть строчки "no-listen tcp" (Или что-то похожее так)


<br/>

	$ netstat -an | grep -F 6000

<br/>

	tcp        0      0 0.0.0.0:6000            0.0.0.0:*               LISTEN
	tcp6       0      0 :::6000                 :::*                    LISTEN


<br/>

	# nmap -p 6000 192.168.1.5

<br/>

    Starting Nmap 6.40 ( http://nmap.org ) at 2017-11-23 09:02 MSK
    Nmap scan report for 10.14.3.43
    Host is up (0.000048s latency).
    PORT     STATE SERVICE
    6000/tcp open  X11


<br/>

	$ nc -vv 192.168.1.5 6000
	Connection to 192.168.1.200 6000 port [tcp/x11] succeeded!=


<br/>

### Разрешить вывод с сервера форм на клиенте

Потом на клиенте под root делаю:

    # xhost +


<!-- $ xhost +192.168.56.101

<br/> -->



<br/>

## На сервере:

Проверяем открыт и доступен ли нам порт клиента

    # yum install -y nmap

<br/>

	# nmap -p 6000 192.168.1.5

результат

    ***
    6000/tcp open  X11


<br/>

Далее лучше всего сделать следующее:

-- если не установили ранее, установите пакет xdpyinfo. Он нужен для отображения окон на клиентской машине.

<br/>

	# yum install -y xdpyinfo xclock
    # su - oracle12

<br/>

    $ xclock -display 192.168.1.5:0

<br/>

Можно, также попробовать

	$ export DISPLAY=192.168.1.5:0.0

<br/>

    $ xdpyinfo
    name of display:    192.168.1.5:0.0
    version number:    11.0
    vendor string:    The X.Org Foundation
    vendor release number:    11702000
    X.Org version: 1.17.2
    maximum request size:  16777212 bytes
    motion buffer size:  256
    bitmap unit, bit order, padding:    32, LSBFi
    *****
