---
layout: page
title: Запуск Oracle XE 11 в Docker контейнере под Linux
permalink: /database/installation/single-instance/simple/linux/docker/oracle/11/xe/
---


<br/>

# Запуск Oracle XE 11 в Docker контейнере под Linux

Делаю: 

03.04.2018

<br/>

Наверное, это лучшее решение, когда нужно просто запустить базу для каких-нибудь тестовых целей. Был вопрос в чате. Инсталлировать базу совсем не хотелось. Под рукой установленных не было.


Итак.

База данных Oracle бесплатной верии может быть запущена в контейнере буквально парой команд. (Можно даже одной командой, не суть.)

Должен быть установлен Docker.  
Например, следующим образом, это можно сделать в:  

Ubuntu like дистрибутивах:  
http://sysadm.ru/linux/containers/docker/installation/ubuntu/

CentOS 7.3 like дистрибутивах:  
http://sysadm.ru/linux/containers/docker/installation/centos/7/


<br/>

Подготовленны контейнер с Oracle XE 11 можно взять здесь:  
https://hub.docker.com/r/alexeiled/docker-oracle-xe-11g/

<br/>

    $ docker pull alexeiled/docker-oracle-xe-11g
    $ docker run -d --shm-size=2g -p 1521:1521 -p 8080:8080 alexeiled/docker-oracle-xe-11g


Видим 2 команды. 
1) взять контейнер
2) запустить

Остается только подключиться, как сделал я с помощью бесплатного SQLDeveloper, который можно скачать с сайта oracle.

<br/>

**Параметры подключения:**

    hostname: localhost
    port: 1521
    sid: xe
    username: system
    password: oracle
    Password for SYS user

    oracle

<br/>

**Connect to Oracle Application Express web management console**

    url: http://localhost:8080/apex
    workspace: internal
    user: admin
    password: oracle

<br/>

**Не забедте поменять пароль, предупреждает создатель контейнера**

<br/>

Как обстоят дела с серьезными базами в контейнерах, мне пока неизвестно.

Поменять пароль можно командой:

    alter user system identified by NewPassword;
