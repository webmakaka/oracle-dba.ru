---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Конфиги виртуальных машин для storage
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/vm/storage/
---

# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Конфиги виртуальных машин для storage


    # su - vmadm

<br/>

    $ vm=vm_oel_storage


Создаем каталоги для виртуальной машины  и для snapshots

    $ mkdir -p ${VM_HOME}/${vm}/snapshots


### Создание и регистрация виртуальной машины:

    $ VBoxManage createvm \
    --name ${vm} \
    --ostype RedHat_64 \
    --basefolder ${VM_HOME}/${vm} \
    --register



### Устанавливаем планку оперативной памяти:


    $ VBoxManage modifyvm ${vm} --memory 512


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
    --medium  /home/marley/Downloads/OracleLinux6U7/x64/OracleLinux-R6-U7-Server-x86_64-dvd.iso


### Подключение сетевых интерфейсов:


    $ VBoxManage modifyvm ${vm} \
    --nictype1 82540EM \
    --nic1 bridged \
    --bridgeadapter1 eth0

    $ VBoxManage modifyvm ${vm} \
    --nictype2 82540EM \
    --nic2 bridged \
    --bridgeadapter2 eth0


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



### Показать результат созданнойвиртуальной машины:


    $ VBoxManage showvminfo ${vm}


<br/>

## ВИРТУАЛЬНАЯ МАШИНА ГОТОВА ДЛЯ ИНСТАЛЛЯЦИИ ОПЕРАЦИОННОЙ СИСТЕМЫ

<br/>

### Стартуем виртуальную машину с возможностью подключения по RDP:


    $ VBoxHeadless --startvm ${vm}


Устанавливать операционную следует на 1 диск.
