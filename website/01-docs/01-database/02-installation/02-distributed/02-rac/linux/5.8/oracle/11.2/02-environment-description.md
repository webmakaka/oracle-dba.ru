---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 (ISCSI + ASM) - Описание окружения для инсталляции Oracle RAC
description: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 (ISCSI + ASM) - Описание окружения для инсталляции Oracle RAC
keywords: database, installation, distributed, rac, linux, 5.8, oracle, 11.2, Описание окружения для инсталляции Oracle RAC
permalink: /database/installation/distributed/rac/linux/5.8/oracle/11.2/environment-description/
---

# <a href="/database/installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Описание окружения для инсталляции Oracle RAC

<br/>

RAC выглядит приблизительно следующим образом:

<div align="center">
<img src="https://img.oracledba.net/img/oracle/database/rac/11.2/OracleRac_11.2.jpg" alt="oracle rac" border="0">
</div>

<br/><br/>

<hr>
<br/><br/>

В документи приводится пример пример развертывания <strong>Oracle Real Applicatoin Cluster 11.2 </strong> с использованием 4 виртуальных машин virtualbox, созданных "приблизительно" следующим образом:<br/>
https://docs.google.com/document/d/1ZU6Hk5DYitFYwlRFqN2qmJr6maPpvgsVc6ZTiZ1kYVA/edit

<br/><br/>
<br/><br/>

<div align="center">
	<img src="https://img.oracledba.net/img/oracle/database/rac/11.2/rac1.png" alt="oracle rac" border="0">
</div>

<br/><br/>

<ul>
<li>2 виртуальные машины используются в качестве узлов кластера или кластерных нод (кому как больше нравится). На них устанавливается программное обеспечение Oracle: Oracle Grid и Oracle DataBase Software</li>
<li>1 виртуальная машина, которая выступает в роли хранилища данных, диски которого смонтированы в файловой системе узлов кластера по технологии iSCSI. </li>
<li>1 виртуальная машина используется в качестве DNS - сервера.</li>
</ul>

<br/><br/>
Каждый из узлов кластера имеет 4 GB оперативной памяти и 3 сетевых адаптера:<br/>
В качестве операционной системы выбран Oracle Linux 5.8
<br/><br/>

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
