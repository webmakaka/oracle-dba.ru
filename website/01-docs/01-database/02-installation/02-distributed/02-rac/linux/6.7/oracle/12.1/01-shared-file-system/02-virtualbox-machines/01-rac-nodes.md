---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Конфиги виртуальных машин для узлов кластера
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/vm/rac-nodes/
---

# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Конфиги виртуальных машин для инсталляции узлов кластера


    # su - vmadm

<br/>

    $ vm=vm_oel_rac1


Создаем каталоги для виртуальной машины  и для snapshots

    $ mkdir -p ${VM_HOME}/${vm}/snapshots


### Создание и регистрация виртуальной машины:

    $ VBoxManage createvm \
    --name ${vm} \
    --ostype RedHat_64 \
    --basefolder ${VM_HOME}/${vm} \
    --register



### Устанавливаем планку оперативной памяти:


    $ VBoxManage modifyvm ${vm} --memory 4608


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

	$ VBoxManage createhd \
    --filename ${vm}_dsk1.vdi \
    --size 40960 \
    --format VDI \
    --variant Standard

    $ VBoxManage createhd \
    --filename ${vm}_dsk2.vdi \
    --size 40960 \
    --format VDI \
    --variant Standard




### Подключаю диски к SAS контроллеру:


	$ VBoxManage storageattach ${vm} \
	--storagectl "SAS Controller" \
	--port 0 \
	--type hdd \
	--medium ${vm}_dsk1.vdi

	$ VBoxManage storageattach ${vm} \
	--storagectl "SAS Controller" \
	--port 1 \
	--type hdd \
	--medium ${vm}_dsk2.vdi



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
    --medium  /home/marley/Downloads/OracleLinux6U7/x64/OracleLinux-R6-U7-Server-x86_64-dvd.iso


### Подключение сетевых интерфейсов:


Наберите команду;

    $ VBoxManage list bridgedifs

Обратите внимание на значение:

Name:                eth0

Я использую eth0 как основной физический интерфейс, который будут использовать виртуальные машины в качестве моста.

Подключаю к виртуальной машине 3 виртуальных сетевых “Intel® 82540EM Gigabit Ethernet Controller”, работающих как bridget (3 адаптера нужные в случае необходимости установить RAC):

    $ VBoxManage modifyvm ${vm} \
    --nictype1 82540EM \
    --nic1 bridged \
    --bridgeadapter1 eth0

    $ VBoxManage modifyvm ${vm} \
    --nictype2 82540EM \
    --nic2 bridged \
    --bridgeadapter2 eth0

    $ VBoxManage modifyvm ${vm} \
    --nictype3 82540EM \
    --nic3 bridged \
    --bridgeadapter3 eth0


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
--vrdeport порт к которому можно будет подключиться при старте виртуальной машины.  



### Показать результат созданнойвиртуальной машины:


    $ VBoxManage showvminfo ${vm}


<br/>

## ВИРТУАЛЬНАЯ МАШИНА ГОТОВА ДЛЯ ИНСТАЛЛЯЦИИ ОПЕРАЦИОННОЙ СИСТЕМЫ

<br/>

### Стартуем виртуальную машину с возможностью подключения по RDP:


    $ VBoxHeadless --startvm ${vm}


Подключаюсь по RDP к виртуальной машине. В Windows это консоль для удаленного подключения (mstsc вроде), в linux remmina или rdesktop.


В первом окне нажимаю tab и дописываю linux text, чтобы инсталляция проходила в удобном для меня режиме. Устанавливать операционную следует на 1 диск. Второй будет для Oracle.

Таких виртуальных машин должно быть 2. После инсталляции предлагаю клонировать.


    $ vboxmanage clonevm vm_oel_rac1 --name vm_oel_rac2 --register
    $ vm=vm_oel_rac2
    $ VBoxHeadless --startvm ${vm}

<!--

Нужно поменять mac адреса вирту

    $ vboxmanage modifyvm ${vm} --macaddress1 auto
    $ vboxmanage modifyvm ${vm} --macaddress2 auto
    $ vboxmanage modifyvm ${vm} --macaddress3 auto


-->

Нужно отредактировать или удалить содержимое файла в котором явно прописывается какому интерфейсу какой mac адрес соответствует.


     # cat /dev/null > /etc/udev/rules.d/70-persistent-net.rules


И перезагрузиться.
