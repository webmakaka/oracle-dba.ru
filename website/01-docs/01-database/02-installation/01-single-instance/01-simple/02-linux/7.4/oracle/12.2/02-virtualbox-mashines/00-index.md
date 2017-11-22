---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Создание виртуальной машины VirtualBox для инсталляции базы данных
permalink: /database/installation/single-instance/simple/oel/7.4/oracle/db/12.2/
---


<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Создание виртуальной машины VirtualBox для инсталляции базы данных


<br/>

О том как инсталлировал virtualbox, переменные и каталоги, смотри  
<a href="//sysadm.ru/linux/virtual/virtualbox/">здесь</a>


<br/>

### Создание виртуальной машины:

    # su - vmadm

Задаем имя виртуальной машине:

    $ vm=vm_oel_7.4_oracle_db_12.2


Создаем каталоги для виртуальной машины  и для snapshots

    $ mkdir -p ${VM_HOME}/${vm}/snapshots


### Создание и регистрация виртуальной машины:

    $ VBoxManage createvm \
    --name ${vm} \
    --ostype Oracle_64 \
    --basefolder ${VM_HOME}/${vm} \
    --register


### Устанавливаем планку оперативной памяти:


    $ VBoxManage modifyvm ${vm} --memory 4096


### Подключаю видеокарту на 32 MB:


    $ VBoxManage modifyvm ${vm} --vram 32


### Снимаю sound карту, вытаскиваем дисковвод:

    $ VBoxManage modifyvm ${vm} --floppy disabled --audio none


### Подключаю контроллер жестких дисков (SAS):


    $ VBoxManage storagectl ${vm} \
    --add sas \
    --name "SAS Controller"


### Создание и подключение жестких дисков:


Создаю виртуальные жесткие диски. Размер (size), рекомендуется задавать согласно имеющихся ресурсов. Иначе возможны проблемы и крах виртуальной машины):

    $ cd ${VM_HOME}/${vm}/${vm}

Создать 8 дисков 1 командой:

    $ for i in $(seq 1 8 )
    do VBoxManage createhd --filename ${vm}_dsk_dsk$i.vdi --size 40960 --format VDI --variant Standard
    done



### Подключаю диски к SAS контроллеру:


Подключить 8 дисков 1 командой:

    $ for i in $(seq 1 8 )
    do let port=$i-1; VBoxManage storageattach ${vm} --storagectl "SAS Controller" --port $port --type hdd --medium ${vm}_dsk_dsk$i.vdi
    done



### Подключаю IDE контроллер к которому будет позднее подключен DVD-ROM:


    $ VBoxManage storagectl ${vm} \
    --add ide \
    --name "IDE Controller"


### Подключаю к IDE контроллеру DVD образ инсталлируемой операционной системы:


    $ VBoxManage storageattach ${vm} \
    --storagectl "IDE Controller" \
    --port 0 \
    --device 0 \
    --type dvddrive \
    --medium  /mnt/dsk1/oracle/OracleLinux/7.4/V921569-01.iso


### Подключение сетевых интерфейсов:


Вариант настройки, когда сервер будет работать на моем компьютере и не должен быть доступен за ее пределами.


Понадобился 1 hostonly адаптер для подключения к виртуальной машине по SSH с хоста.

    $ VBoxManage modifyvm ${vm} \
    --nictype1 82540EM \
    --nic1 hostonly \
    --hostonlyadapter1 vboxnet0


И 1  адаптер с NAT, чтобы компьютер мог выходить в интернет.

    $ VBoxManage modifyvm ${vm} \
    --nictype2 82540EM \
    --nic2 nat

<br/>

ifconfig на хост машине должен выводить vboxnet0.

vboxnet0 - виртуальный адаптер хостовой машины.

Если виртуального адаптера нет, нуно его самостоятельно создать.


    $ VBoxManage hostonlyif create

<br/>

    $ vboxmanage list hostonlyifs
    Name:            vboxnet0
    GUID:            786f6276-656e-4074-8000-0a0027000000
    DHCP:            Disabled
    IPAddress:       192.168.56.1
    NetworkMask:     255.255.255.0
    IPV6Address:
    IPV6NetworkMaskPrefixLength: 0
    HardwareAddress: 0a:00:27:00:00:00
    MediumType:      Ethernet
    Status:          Down
    VBoxNetworkName: HostInterfaceNetworking-vboxnet0

Присвоить ip, если у него нет.

    $ VBoxManage hostonlyif ipconfig vboxnet0 --ip 192.168.56.1

Стартовать, если нужно

    $ sudo ifconfig vboxnet0 up


Если что-то пошло не так, можно удалить созданный интерфейс командой:

    $ VBoxManage modifyvm ${vm} --nic2 none


<br/>

### Определяем порядок устройств, с которых будет произведена попытка стартовать систему:


    $ VBoxManage modifyvm ${vm} \
    --boot1 disk \
    --boot2 dvd


### Определяем каталог для снапшотов:


    $ VBoxManage modifyvm ${vm} \
    --snapshotfolder ${VM_HOME}/${vm}/snapshots



### Предоставим возможность подключения к машине по RDP:


    $ VBoxManage modifyvm ${vm} \
    --vrde on \
    --vrdemulticon on \
    --vrdeauthtype null \
    --vrdeaddress 192.168.1.5 \
    --vrdeport 3389

Здесь мы указываем:  

--vrdeaddress - ip адрес машины, на которой установлен vitrualbox  
--vrdeauthtype null - аутентификация не требуется.  
--vrdemulticon on - разрешено множественное подключение к виртуальным машинам.  
--vrdeport - порт к которому можно будет подключиться при старте виртуальной машины.  


### Показать результат созданнойвиртуальной машины:

    $ VBoxManage showvminfo ${vm}


### Создание снапшота перед инсталляцией ОС

    $ VBoxManage snapshot ${vm} take before_os_installation

<br/>

## ВИРТУАЛЬНАЯ МАШИНА ГОТОВА ДЛЯ ИНСТАЛЛЯЦИИ ОПЕРАЦИОННОЙ СИСТЕМЫ


Более подробный документ с созданием снапшотов и резервныхкопий виртуальных машин смотри
<a href="//sysadm.ru/linux/virtual/virtualbox/">здесь</a>

<br/>

### Стартуем виртуальную машину с возможностью подключения по RDP:


    $ VBoxHeadless --startvm ${vm}



<br/>

### Подключаюсь по RDP к виртуальной машине.


В Windows это может быть консоль для удаленного подключения (start --> RUN --> mstsc).
В linux - remmina или rdesktop и еще куча всего.


Делаю в Ubuntu 12.04

    $ sudo apt-get install -y rdesktop

<br/>

В Oracle Linux пакета нет в подключенных мной стандартных репо.

Делал так:

    # rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
    # rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
    # yum install rdesktop

<br/>

    $ rdesktop \
    -r sound:local \
    -k common  \
    -g  1600x1024 \
    192.168.1.5:3389


В первом окне нажимаю tab и дописываю linux text, чтобы инсталляция проходила в удобном для меня режиме. Устанавливать операционную следует на 1 диск.
