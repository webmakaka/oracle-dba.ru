---
layout: page
title: Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle в Linux
description: Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle в Linux
keywords: Oracle Database, Подготовка окружения для инсталляции базы данных Oracle в Linux, VirtualBox
permalink: /database/installation/virtualbox-machines/oracle-linux/
---

# Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle в Linux

Пример создания виртуальной машины VirtualBox для инсталляции сервера баз данных Oracle<br/>
Виртуальная машина создается в ubuntu. <br/>
Аналогичным образом виртуальная машина создается в redhat дистрибутивах.

Задаем переменную с именем создаваемой виртуальной машины, чтобы в дальнейшем лишний раз не подставлять данное значение в команды.

    # su - vmadm
    $ vm=vm_oel6.4_oradb12.1
    $ echo $vm

Создаем каталоги для виртуальной машины и для snapshots

    $ mkdir -p ${VM_HOME}/${vm}/snapshots

### Создание и регистрация виртуальной машины:

Узнать список поддерживаемых операционных систем

    $ VBoxManage list ostypes

Если создается виртуальная машина Oracle Linux 64:

    $ VBoxManage createvm \
    --name ${vm} \
    --ostype Oracle_64 \
    --basefolder ${VM_HOME}/${vm} \
    --register

Должно появиться сообщение:<br/>
Virtual machine 'vm_oel6.4_oradb12.1' is created and registered.

<br/>

Выбираю материнскую плату с более современным чипсетом . По умолчанию piix3

    $ VBoxManage modifyvm ${vm}  --chipset piix3

Устанавливаю процессоры.

    $ VBoxManage modifyvm ${vm}  --cpus 2

Устанавливаем планку оперативной памяти

    $ VBoxManage modifyvm ${vm} --memory 4096

Подключаем видеокарту на 32 MB

    $ VBoxManage modifyvm ${vm} --vram 32

Снимаем sound карту, вытаскиваем дисковвод

    $ VBoxManage modifyvm ${vm} --floppy disabled --audio none

Подключаю контроллер жестких дисков (SAS)

    $ VBoxManage storagectl ${vm} \
    --add sas \
    --name "SAS Controller"

Создаю виртуальные жесткие диски. Размер (size), рекомендуется задавать согласно имеющихся ресурсов. Иначе возможны проблемы и крах виртуальной машины):

    $ cd ${VM_HOME}/${vm}/${vm}

Если не хочется копипастить 8 раз одно и тоже, можно воспользоваться всего одной командой:

Создать диски 1 командой:

    $ for i in $(seq 1 8 )
    do VBoxManage createhd --filename ${vm}_dsk_dsk$i.vdi --size 40960 --format VDI --variant Standard
    done

Подключить диски 1 командой:

    $ for i in $(seq 1 8 )
    do let port=$i-1; VBoxManage storageattach ${vm} --storagectl "SAS Controller" --port $port --type hdd --medium ${vm}_dsk_dsk$i.vdi
    done

<!--
<br/><br/>
Или вручную (Так надежнее):
<br/><br/>

       <div class="linuxCommand">
	$ VBoxManage createhd \<br/>
--filename ${vm}_dsk1.vdi \<br/>
--size 40960 \<br/>
--format VDI \<br/>
--variant Standard<br/>
       </div>


<br/><br/>


       <div class="linuxCommand">
$ VBoxManage createhd \<br/>
--filename ${vm}_dsk2.vdi \<br/>
--size 40960 \<br/>
--format VDI \<br/>
--variant Standard<br/>
       </div>



<br/><br/>


       <div class="linuxCommand">
$ VBoxManage createhd \<br/>
--filename ${vm}_dsk3.vdi \<br/>
--size 40960 \<br/>
--format VDI \<br/>
--variant Standard<br/>
       </div>


<br/><br/>


       <div class="linuxCommand">
$ VBoxManage createhd \<br/>
--filename ${vm}_dsk4.vdi \<br/>
--size 40960 \<br/>
--format VDI \<br/>
--variant Standard<br/>
       </div>



<br/><br/>


       <div class="linuxCommand">
$ VBoxManage createhd \<br/>
--filename ${vm}_dsk5.vdi \<br/>
--size 40960 \<br/>
--format VDI \<br/>
--variant Standard<br/>
       </div>


<br/><br/>


       <div class="linuxCommand">
$ VBoxManage createhd \<br/>
--filename ${vm}_dsk6.vdi \<br/>
--size 40960 \<br/>
--format VDI \<br/>
--variant Standard<br/>
       </div>


<br/><br/>


       <div class="linuxCommand">
$ VBoxManage createhd \<br/>
--filename ${vm}_dsk7.vdi \<br/>
--size 40960 \<br/>
--format VDI \<br/>
--variant Standard<br/>
       </div>

<br/><br/>


       <div class="linuxCommand">
$ VBoxManage createhd \<br/>
--filename ${vm}_dsk8.vdi \<br/>
--size 40960 \<br/>
--format VDI \<br/>
--variant Standard<br/>
       </div>

<br/><br/>
Подключаю диски к SAS контроллеру (максимум 8):


       <div class="linuxCommand">
$ VBoxManage storageattach ${vm} \<br/>
--storagectl "SAS Controller" \<br/>
--port 0 \<br/>
--type hdd \<br/>
--medium ${vm}_dsk1.vdi<br/>
       </div>

<br/><br/>

       <div class="linuxCommand">
$ VBoxManage storageattach ${vm} \<br/>
--storagectl "SAS Controller" \<br/>
--port 1 \<br/>
--type hdd \<br/>
--medium ${vm}_dsk2.vdi<br/>
       </div>

<br/><br/>

       <div class="linuxCommand">
$ VBoxManage storageattach ${vm} \<br/>
--storagectl "SAS Controller" \<br/>
--port 2 \<br/>
--type hdd \<br/>
--medium ${vm}_dsk3.vdi<br/>
       </div>

<br/><br/>

       <div class="linuxCommand">
$ VBoxManage storageattach ${vm} \<br/>
--storagectl "SAS Controller" \<br/>
--port 3 \<br/>
--type hdd \<br/>
--medium ${vm}_dsk4.vdi<br/>
       </div>

<br/><br/>

       <div class="linuxCommand">
$ VBoxManage storageattach ${vm} \<br/>
--storagectl "SAS Controller" \<br/>
--port 4 \<br/>
--type hdd \<br/>
--medium ${vm}_dsk5.vdi<br/>
       </div>

<br/><br/>

<div class="linuxCommand">
$ VBoxManage storageattach ${vm} \<br/>
--storagectl "SAS Controller" \<br/>
--port 5 \<br/>
--type hdd \<br/>
--medium ${vm}_dsk6.vdi<br/>
</div>

<br/><br/>

<div class="linuxCommand">
$ VBoxManage storageattach ${vm} \<br/>
--storagectl "SAS Controller" \<br/>
--port 6 \<br/>
--type hdd \<br/>
--medium ${vm}_dsk7.vdi<br/>
</div>

<br/><br/>

<div class="linuxCommand">
$ VBoxManage storageattach ${vm} \<br/>
--storagectl "SAS Controller" \<br/>
--port 7 \<br/>
--type hdd \<br/>
--medium ${vm}_dsk8.vdi<br/>
</div>

-->

Подключаем IDE контроллер к которому будет позднее подключен DVD-ROM:

    $ VBoxManage storagectl ${vm} \
    --add ide \
    --name "IDE Controller"

Подключаю к IDE контроллеру DVD образ инсталлируемой операционной системы:

    $ VBoxManage storageattach ${vm} \
    --storagectl "IDE Controller" \
    --port 0 \
    --device 0 \
    --type dvddrive \
    --medium /mnt/dsk2/_ISO/_OEL/OracleLinux-R6-U4-Server-x86_64-dvd.iso

### Подключение сетевых интерфейсов:

(Мой компьютер подключен к маршрутизатору (обычный домашний роутер). Обмен данных между моим компьютером и виртуальной машиной будет проходить через него. Если вы не используете маршрутизатор или коммутатор, вам нужно создать сетевые интерфейсы с параметром не bridget а internal connection.)

Наберите команду;

    $ VBoxManage list bridgedifs

Обратите внимание на значение:

    Name:            eth0

Я использую eth0 как основной физический интерфейс, который будут использовать виртуальные машины в качестве моста.

Подключаю к виртуальной машине 2 виртуальных сетевых интерфеса “Intel® 82540EM Gigabit Ethernet Controller”, работающих как bridget:

    $ VBoxManage modifyvm ${vm} \
    --nictype1 82540EM \
    --nic1 bridged \
    --bridgeadapter1 eth0

Подключаем к IDE контроллеру DVD образ инсталлируемой операционной системы:

    $ VBoxManage modifyvm ${vm} \
    --nictype2 82540EM
    --nic2 bridged \
    --bridgeadapter2 eth0

(Если планируется инсталлировать RAC, рекомендуется установить 3-й интерфейс)

    $ VBoxManage modifyvm ${vm} \
    --nictype3 82540EM \
    --nic3 bridged \
    --bridgeadapter3 eth0

Определяем порядок устройств, с которых будет произведена попытка стартовать систему

    $ VBoxManage modifyvm ${vm} \
    --boot1 disk \
    --boot2 dvd

Определяем каталог для снапшотов

    $ VBoxManage modifyvm ${vm} \
    --snapshotfolder ${VM_HOME}/${vm}/snapshots

Предоставим возможность подключения к машине по RDP:

$ VBoxManage modifyvm ${vm} \
--vrde on \
--vrdemulticon on \
--vrdeauthtype null \
--vrdeaddress 192.168.1.5 \
--vrdeport 3389

Здесь мы указываем:

--vrdeaddress - ip адрес машины, на которой установлен vitrualbox.  
--vrdeauthtype null - аутентификация не требуется.  
--vrdemulticon on - разрешено множественное подключение к виртуальным машинам.  
--vrdeport порт к которому можно будет подключиться при старте виртуальной машины.

Создание снапшота перед инсталляцией ОС

    $ VBoxManage snapshot ${vm} take before_os_installation

ВИРТУАЛЬНАЯ МАШИНА ГОТОВА ДЛЯ ИНСТАЛЛЯЦИИ ОПЕРАЦИОННОЙ СИСТЕМЫ

Показать результат созданнойвиртуальной машины:

    $ VBoxManage showvminfo ${vm}  | less

Стартуем виртуальную машину с возможность подключения по RDP

    $ VBoxHeadless --startvm ${vm}

Посмотреть стартованные виртуальные машины можно командой

    $ vboxmanage list runningvms

Если работаете в linux, подключиться к виртуальной машине можно с помощью rdesktop

    $ rdesktop \
    -r sound:local \
    -k common  \
    -g  1600x1024 \
    192.168.1.5:3389

Если нужно подключиться с определенной “геометрией”, используйте параметр -g 1600x1024

Если нужно работать в полноэкранном режиме, нужно убрать ключ -g и заменить его ключом -f

Для выхода из полноэкранного режима - CTRL+ALT+ENTER

rdesktop - всевозможные ключи:  
http://manpages.ubuntu.com/manpages/lucid/man1/rdesktop.1.html

В Windows для этого вполне подойдет Remote Desktop Connecton (mstsc.exe). В Linux есть аналогичная программа для подключения к удаленным рабочим столам - Remmina.

Более подробный документ с созданием снапшотов и резервныхкопий виртуальных машин:<br/>
https://docs.google.com/document/d/1ZU6Hk5DYitFYwlRFqN2qmJr6maPpvgsVc6ZTiZ1kYVA/edit
