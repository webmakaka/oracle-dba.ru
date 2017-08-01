---
layout: page
title: Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle в Windows 2008 Server
permalink: /database/installation/single-instance/simple/windows/2008/oracle/12.1/virtualbox-mashines/windows/2008/
---

# <a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/">[Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server]</a>: Создание виртуальной машины VirtualBox для инсталляции базы данных Oracle в Windows 2008 Server

<br/>

О том как инсталлировал virtualbox, переменные и каталоги, смотри  
<a href="//sysadm.ru/linux/virtual/virtualbox/">здесь</a>


Задаем переменную с именем создаваемой виртуальной машины, чтобы в дальнейшем лишний раз не подставлять данное значение в команды.

    # su - vmadm
    $ vm=vm_win2k8_oradb12.1
    $ echo $vm


Создаем каталоги для виртуальной машины и для snapshots

	$ mkdir -p ${VM_HOME}/${vm}/snapshots

<br/>

### Создание и регистрация виртуальной машины:


Узнать список поддерживаемых операционных систем


	$ VBoxManage list ostypes


Для виртуальной машины Windows 2k8


    $ VBoxManage createvm \
    --name ${vm} \
    --ostype Windows2008_64  \
    --basefolder ${VM_HOME}/${vm} \
    --register


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


Подключаю контроллер жестких дисков (SATA). (С подключенным контроллером SAS, Windows не видит жесткие диски)


    $ VBoxManage storagectl ${vm} \
    --add sata \
    --name "SATA Controller"

Создаю виртуальные жесткие диски. Размер (size), рекомендуется задавать согласно имеющихся ресурсов. Иначе возможны проблемы и крах виртуальной машины):

	$ cd ${VM_HOME}/${vm}/${vm}


Если не хочется копипастить 8 раз одно и тоже, можно воспользоваться всего одной командой:

Создать диски 1 командой:

    $ for i in $(seq 1 8 )  
    do VBoxManage createhd --filename ${vm}_dsk_dsk$i.vdi --size 40960 --format VDI --variant Standard
    done


Подключить диски 1 командой:

    $ for i in $(seq 1 8 )
    do VBoxManage storageattach ${vm} --storagectl "SATA Controller" --device 0 --port $i --type hdd --medium ${vm}_dsk_dsk$i.vdi
    done


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
    --medium /mnt/dsk2/_ISO/_Microsoft/win2k8/x64/en_windows_server_2008_with_sp2_x64_dvd_342336.iso

### Подключение сетевых интерфейсов:

(Мой компьютер подключен к маршрутизатору (обычный домашний роутер). Обмен данных между моим компьютером и виртуальной машиной будет проходить через него. Если вы не используете маршрутизатор или коммутатор, вам нужно создать сетевые интерфейсы с параметром не bridget а internal connection.)


Наберите команду;

    $ VBoxManage list bridgedifs

Обратите внимание на значение:

    Name:            eth0


Я использую eth0 как основной физический интерфейс, который будут использовать виртуальные машины в качестве моста.


Подключаю к виртуальной машине 2 виртуальных сетевых интерфеса “Intel® 82540EM Gigabit Ethernet Controller”, работающих как bridget:

Подключаю к IDE контроллеру DVD образ инсталлируемой операционной системы:

    $ VBoxManage modifyvm ${vm} \
    --nictype1 82540EM \
    --nic1 bridged \
    --bridgeadapter1 eth0


Подключаем к IDE контроллеру DVD образ инсталлируемой операционной системы:

    $ VBoxManage modifyvm ${vm} \
    --nictype2 82540EM \
    --nic2 bridged \
    --bridgeadapter2 eth0


Определяем порядок устройств, с которых будет произведена попытка стартовать систему


    $ VBoxManage modifyvm ${vm} \
    --boot1 disk \
    --boot2 dvd


Определяем каталог для снапшотов


    $ VBoxManage modifyvm ${vm} \
    --snapshotfolder ${VM_HOME}/${vm}/snapshots

<br/>

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


Показать результат созданнойвиртуальной машины:

    $ VBoxManage showvminfo ${vm}  | less


Создание снапшота перед инсталляцией ОС

    $ VBoxManage snapshot ${vm} take before_os_installation


## ВИРТУАЛЬНАЯ МАШИНА ГОТОВА ДЛЯ ИНСТАЛЛЯЦИИ ОПЕРАЦИОННОЙ СИСТЕМЫ


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


Если нужно подключиться с определенной “геометрией”, используйте параметр  
-g  1600x1024


Если нужно работать в полноэкранном режиме, нужно убрать ключ -g и заменить его ключом -f

Для выхода из полноэкранного режима - CTRL+ALT+ENTER


rdesktop - всевозможные ключи:<br/>
http://manpages.ubuntu.com/manpages/lucid/man1/rdesktop.1.html<br/>


В Windows для этого вполне подойдет Remote Desktop Connecton (mstsc.exe). В Linux есть аналогичная программа для подключения к удаленным рабочим столам - Remmina.


Более подробный документ с созданием снапшотов и резервныхкопий виртуальных машин смотри
<a href="//sysadm.ru/linux/virtual/virtualbox/">здесь</a>


Для нормальной работы в Windows также нужно будет установить VirtualBox Guest Additions  
http://download.virtualbox.org/virtualbox/4.3.30/
