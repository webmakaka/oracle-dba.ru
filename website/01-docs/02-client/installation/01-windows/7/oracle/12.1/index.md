---
layout: page
title: Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)
permalink: /client/installation/windows/7/oracle/12.1/
---

# [Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)]


В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, пишите мне адрес эл. почты:


<div>
	<img src="/img/a3333333mail.gif" alt="Marley" border="0">
</div>


<br/>


Oracle Clietn необходим для удаленного подключения к базе данных разного рода программ. Программы, написанные на Java - так называемые (тонкие клиенты), могут  обходится и без клиента. Например, SQL Developer и JDeveloper. Это также относится и к web приложениям, которые запущены непосредственно на сервере, такие как APEX, Enterprise Manager, iSQLPLUS.

Для подключения остальных программ TOAD, PL/SQL Developer, SQL PLUS и большинства других, требуется библиотека oci.dll (oracle call interface), которая собственно и предоставляет такую возможность и разумеется она включена в набор всевозможных дополнительных программ, которые объединены под одним общим названием Oracle Client.

Скачать дистрибутив Oracle Client можно с rutracker или более позднюю версию с официального сайта. Если у Вас есть доступ к MetaLink, рекомендуется качать самую последнюю версию именно оттуда.


Oracle client для Windows  
hxxp://rutracker.org/forum/viewtopic.php?t=4803357

Для инсталляции клиента достаточно 1 архива  
winnt_12102_client32.zip

**Устанавливать 64 битный клиент конечно можно и с ним замечательно будет работать sqlplus. Правда PL/SQL Developer пока умеет работать только с 32-х битным клиентом, поэтому ниже описывается именно он**

<br/>

### Подготовка среды

Для начала, нужно установить 1 библиотеку в Windows 2008. Без нее установка 32-х битного клиента завершится ошибкой. При этом 64 битному клиенту эта библиотека не требуется.


https://www.microsoft.com/en-gb/download/details.aspx?id=5555


<br/>

**hosts**

Отредактируйте файл hosts, таким образом, чтобы не приходилось обращаться к серверу баз данных по его IP

Файл hosts нужно отредактировать, например в notepad запущенном от учетной записью с правами администратора.

C:\WINDOWS\system32\drivers\etc\hosts

    127.0.0.1   	localhost
    192.168.1.11	oracle12.localdomain oracle12


<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/01-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>


<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/02-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>



<br/>

### Инсталляция Oracle Client


<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/03-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/04-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/05-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/06-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/07-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/08-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>


Вообще нужен только Oracle Call Interface. Но для удобства настройки и работы, лично я устанавливаю 3 компонента:

<ul>
<li>SQL Plus</li>
<li>Oracle Call Interface (OCI)</li>
<li>Connection Manager</li>
</ul>


<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/09-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/10-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/11-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>


<br/>

### Генерация конфига в мастере для подключения к базе:


<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/12-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/13-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/14-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/15-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/16-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/17-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/18-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/19-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/20-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>



Параметры подключения можно посмотреть на сервере в файле tnsnames.ora

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/21-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/22-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/23-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/24-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/25-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/26-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/27-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/28-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/29-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/30-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/31-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/32-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/33-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>


<br/>

### В результате инсталлируются библиотеки и генерируется файл tnsnames.ora


<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/34-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/35-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>


    ORCL12 =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = oracle12.localdomain)(PORT = 1521))
        )
        (CONNECT_DATA =
          (SERVICE_NAME = orcl12.localdomain)
        )
      )

<br/>

### Проверка


    C:\> tnsping oracl12


system - login  
manager - password  

    C:\>sqlplus /nolog  
    SQL> conn system/manager@oracle12

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/36-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/37-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/38-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>


<br/>

### Переменные Oracle в реестре

Вместо AMERICAN_AMERICA.WE8MSWIN1252 устанавливаю AMERICAN_AMERICA.AL32UTF8



<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/39-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/40-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/41-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>



<br/>

### Подкючаемся к базе с помощью PL/SQL Developer


<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/42-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/43-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>

<br/><br/>

<div>
	<img src="https://img.oracledba.net/02-client/installation/windows/7/oracle/12.1/44-oracle_client_12_installation_on_windows_7.png" border="0" alt="Инсталляция Oracle Client 12C (32 bit) в операционной системе Windows 7 (64 bit)">
</div>
