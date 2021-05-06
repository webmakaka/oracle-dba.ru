---
layout: page
title: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Описание окружения для инсталляции Oracle RAC
description: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Описание окружения для инсталляции Oracle RAC
keywords: Oracle DataBase 12.1, Oracle Linux 6.7, RAC, (ISCSI + ASM)
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/environment-description/
---

# [Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM)]: Описание окружения для инсталляции Oracle RAC

<br/>

RAC выглядит приблизительно следующим образом:

<div align="center">
<img src="https://img.oracledba.net/img/oracle/database/rac/11.2/OracleRac_11.2.jpg" alt="oracle rac" border="0">
</div>

<br/><br/>

<hr>
<br/><br/>

В документи приводится пример пример развертывания <strong>Oracle Real Applicatoin Cluster 12.1 </strong> с использованием 4 виртуальных машин virtualbox.

<br/><br/>

<ul>
<li>Узлы кластера: rac1, rac2</li>
<li>Сервер с общим хранилищем: storage </li>
<li>DNS сервер: dnsserv</li>
</ul>

<br/><br/>

<div align="center">
	<img src="https://img.oracledba.net/img/oracle/database/rac/11.2/rac1.png" alt="oracle rac" border="0">
</div>

<br/><br/>

<ul>
<li>2 виртуальные машины используются в качестве узлов кластера или кластерных нод (кому как больше нравится). На них устанавливается программное обеспечение Oracle: Oracle Grid и Oracle DataBase Software</li>
<li>1 виртуальная машина, которая выступает в роли хранилища данных, диски которого смонтированы в файловой системе узлов кластера по протоколу Network File System (NFS). </li>
<li>1 виртуальная машина используется в качестве DNS - сервера. SCAN адреса должны быть обязательно прописаны в DNS. Иначе возможны ошибки или вообще не удастся корректно установить RAC</li>
</ul>

В качестве операционных систем на виртуальных машинах используется Oracle Linux 6.7

Каждый из узлов кластера имеет 4,5 GB (минимум 2 GB) оперативной памяти. На Storage и DNS сервер можно выделить значительно меньше.

На узлах кластера по 2 жестких диска размером в 40 GB, на storage 8 дисков, также по 40 GB. Диски расшряемые по мере надобности. Т.е. реально занимают меньше, если указанный объем не используется.<br/>

На узлах кластера установлено по 3 сетевых адаптера. Для Storage достаточно 2-х сетевых адаптеров, для DNS сервера 1-го.

<ul>
	<li>eth0 – public</li>
	<li>eth1 – interconnect (для связи межу узлами кластера)</li>
	<li>eth2 – private (для связи узлов кластера с внешним хранилищем (storage))</li>
</ul>

<br/><br/>
<strong>Для инсталляции RAC, необходимо в одной подсети выделить IP адреса:</strong>
<br/><br/>

<ul>
	<li>1 public IP для каждого узла (просто для того, чтобы подключиться к серверу и выполнять задачи по администрированию)</li>
	<li>1 vip IP для каждого узла ((в той же подсети, что и public) желательно, чтобы vip были прописаны в DNS)</li>
	<li>3 IP адреса для SCAN ((в той же подсети, что и public) обязательно должны быть прописаны в DNS (иначе возникнут ошибки при инсталляции). Клиент обращается к SCAN адресу, который перенаправляет запрос на поднятый на узле кластера vip адрес)</li>
</ul>
