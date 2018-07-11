---
layout: page
title: Запуск Oracle XE 11 в Docker контейнере под Linux
permalink: /database/installation/single-instance/simple/linux/docker/oracle/11/xe/
---


<br/>

# Запуск Oracle XE 11 в Docker контейнере под Linux

Делаю: 

11.07.2018


Если вы работаете в Linux, то базу можно запустить парой команд. Под Windows докер тоже работает, но там не так очевидны преимущества, всилу того, что приходится использовать VirtualBox как промежуточно звено виртуализации. В linux, этот слой нет особого смысла использовать.


<br/>

Наверное, это лучшее решение, когда нужно просто запустить базу для каких-нибудь тестовых целей и сделать это как можно быстрее. 

Итак.

База данных Oracle бесплатной верии может быть запущена в контейнере буквально парой команд. (Можно даже одной командой, не суть.)

Должен быть установлен Docker.  
Например, следующим образом, это можно сделать в:  

**Ubuntu like дистрибутивах:**  
http://sysadm.ru/linux/containers/docker/installation/ubuntu/

**CentOS 7.3 like дистрибутивах:**  
http://sysadm.ru/linux/containers/docker/installation/centos/7/


<br/>

Информацию о подготовленном контейнере, можно посмотреть здесь (Можно и не смотреть, а сразу заняться запуском):  
https://hub.docker.com/r/alexeiled/docker-oracle-xe-11g/

<br/>

    -- скачать имидж к себе на компьютер
    $ docker pull alexeiled/docker-oracle-xe-11g
    
    -- создать и запустить на основе скачанного имиджа контейнер (наверное, имеет смысл еще задать имя контейнера)
    $ docker run -d --shm-size=2g -p 1521:1521 -p 8080:8080 alexeiled/docker-oracle-xe-11g

<br/>

Остается только подключиться, например, как это сделал я с помощью бесплатного инструмента для работы с базой - SQLDeveloper, который можно скачать с сайта oracle.

<br/>

**Параметры подключения:**

    hostname: localhost
    port: 1521
    sid: xe
    username: system
    password: oracle
    
    username: sys
    password: oracle

<br/>

**Connect to Oracle Application Express web management console**

    url: http://localhost:8080/apex
    workspace: internal
    user: admin
    password: oracle

<br/>

**Не забудьте поменять пароль, предупреждает создатель контейнера**

<br/>

Как обстоят дела с серьезными базами в контейнерах, мне пока неизвестно.

Поменять пароль можно командой:

    alter user system identified by NewPassword;
