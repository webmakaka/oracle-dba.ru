---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Подготовка ASM дисков к инсталляции базы данных
permalink: /database/installation/single/asm/linux/6.7/oracle/12.1/prepare-asm-disks/
---

# <a href="/database/installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Подготовка ASM дисков к инсталляции базы данных



В каталоге /u01 будет храниться программное обеспечения для работы с базами данных (Database Software). Файлы данных будут храниться на ASM.


    # ls /dev/sd*
    /dev/sda   /dev/sda2  /dev/sdc  /dev/sde  /dev/sdg
    /dev/sda1  /dev/sdb   /dev/sdd  /dev/sdf  /dev/sdh


Создаем разделы на дисках

    # fdisk /dev/sdb
    # fdisk /dev/sdc
    # fdisk /dev/sdd
    # fdisk /dev/sde
    # fdisk /dev/sdf
    # fdisk /dev/sdg
    # fdisk /dev/sdh

<br/>


    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
             switch off the mode (command 'c') and change display units to
             sectors (command 'u').

    Command (m for help): c
    DOS Compatibility flag is not set

    Command (m for help): u
    Changing display/entry units to sectors

    Command (m for help): n
    Command action
       e   extended
       p   primary partition (1-4)
    p
    Partition number (1-4): 1
    First sector (2048-83886079, default 2048):
    Using default value 2048
    Last sector, +sectors or +size{K,M,G} (2048-83886079, default 83886079):
    Using default value 83886079

    Command (m for help): w
    The partition table has been altered!

    Calling ioctl() to re-read partition table.
    Syncing disks.


<br/>

    # ls /dev/sd*
    /dev/sda   /dev/sdb   /dev/sdc1  /dev/sde   /dev/sdf1  /dev/sdh
    /dev/sda1  /dev/sdb1  /dev/sdd   /dev/sde1  /dev/sdg   /dev/sdh1
    /dev/sda2  /dev/sdc   /dev/sdd1  /dev/sdf   /dev/sdg1


На первый диск устанавливается DataBase Software. Остальные диски планируется использовать в качестве хранилища ASM

    # mkfs.ext4 /dev/sdb1

    # mkdir /u01

    # cp /etc/fstab /etc/fstab.bkp
    # echo "/dev/sdb1 /u01 ext4 defaults 1 2" >> /etc/fstab

    # mount /u01

    # mount | grep sdb1
    /dev/sdb1 on /u01 type ext4 (rw)



<br/>

### Настройка конфигурации для работы в ASM

    # /etc/init.d/oracleasm configure

<br/>

    Default user to own the driver interface []: oracle12
    Default group to own the driver interface []: dba
    Start Oracle ASM library driver on boot (y/n) [n]: y
    Scan for Oracle ASM disks on boot (y/n) [y]: y
    Writing Oracle ASM library driver configuration: done
    Initializing the Oracle ASMLib driver:                     [  OK  ]
    Scanning the system for Oracle ASMLib disks:               [  OK  ]


<br/>

    # /etc/init.d/oracleasm status

<br/>

    Checking if ASM is loaded: yes
    Checking if /dev/oracleasm is mounted: yes


<br/>

**Маркируем диски как ASM диски:**


    # /etc/init.d/oracleasm createdisk ASMDISK1 /dev/sdc1
    # /etc/init.d/oracleasm createdisk ASMDISK2 /dev/sdd1
    # /etc/init.d/oracleasm createdisk ASMDISK3 /dev/sde1
    # /etc/init.d/oracleasm createdisk ASMDISK4 /dev/sdf1
    # /etc/init.d/oracleasm createdisk ASMDISK5 /dev/sdg1
    # /etc/init.d/oracleasm createdisk ASMDISK6 /dev/sdh1

    Marking disk "ASMDISK" as an ASM disk:                        [  OK  ]



<br/>

// Посмотреть список дисков

    # /etc/init.d/oracleasm listdisks
    ASMDISK1
    ASMDISK2
    ASMDISK3
    ASMDISK4
    ASMDISK5
    ASMDISK6


<br/>

### Рекомендации

**Перестартовать oracleasm**

    # /etc/init.d/oracleasm restart

<br/>

**Проверить логи**

    # less /var/log/oracleasm

<br/>

