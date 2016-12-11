---
layout: page
title: Процессы Oracle RAC
permalink: /database/installation/distributed/rac/process/
---


# Процессы Oracle RAC

<br/>


Oracle Real Application Clusters (RAC) Specific Background Processes

Oracle RAC is composed of two or more database instances. They are composed of memory structures and background processes same as the single instance database.


    Oracle RAC instances are composed of following background processes:
    ACMS    — Atomic Control file to Memory Service (ACMS)
    GTX0-j  — Global Transaction Process
    LMON    — Global Enqueue Service Monitor
    LMD     — Global Enqueue Service Daemon
    LMS     — Global Cache Service Process
    LCK0    — Instance Enqueue Process
    DIAG    — Diagnosability Daemon
    RMSn    — Oracle RAC Management Processes (RMSn)
    RSMN    — Remote Slave Monitor


These processes spawned for supporting the multi-instance coordination.


ACMS (from Oracle 11g)
ACMS stands for Atomic Control file Memory Service. In an Oracle RAC environment ACMS is an agent that ensures a distributed SGA memory update(ie) SGA updates are globally committed on success or globally aborted in event of a failure.

GTX0-j  (from Oracle 11g)
The process provides transparent support for XA global transactions in a RAC environment. The database auto tunes the number of these processes based on the workload of XA global transactions.


LMON
The Global Enqueue Service Monitor (LMON), monitors the entire cluster to manage the global enqueues and the resources and performs global enqueue recovery operations. LMON manages instance and process failures and the associated recovery for the Global Cache Service (GCS) and Global Enqueue Service (GES). In particular, LMON handles the part of recovery associated with global resources. LMON provided services are also known as cluster group services (CGS). Lock monitor manages global locks and resources. It handles the redistribution of instance locks whenever instances are started or shutdown. Lock monitor also recovers instance lock information prior to the instance recovery process. Lock monitor co-ordinates with the Process Monitor (PMON) to recover dead processes that hold instance locks.


LMDx
The Global Enqueue Service Daemon (LMD) is the lock agent process that manages enqueue manager service requests for Global Cache Service enqueues to control access to global enqueues and resources. This process manages incoming remote resource requests within each instance. The LMD process also handles deadlock detection and remote enqueue requests. Remote resource requests are the requests originating from another instance. LMDn processes manage instance locks that are used to share resources between instances. LMDn processes also handle deadlock detection and remote lock requests.


LMSx
The Global Cache Service Processes (LMSx) are the processes that handle remote Global Cache Service (GCS) messages. Real Application Clusters software provides for up to 10 Global Cache Service Processes. The number of LMSx varies depending on the amount of messaging traffic among nodes in the cluster.

This process maintains statuses of datafiles and each cached block by recording information in a Global Resource Directory(GRD). This process also controls the flow of messages to remote instances and manages global data block access and transmits block images between the buffer caches of different instances. This processing is a part of cache fusion feature.

The LMSx handles the acquisition interrupt and blocking interrupt requests from the remote instances for Global Cache Service resources. For cross-instance consistent read requests, the LMSx will create a consistent read version of the block and send it to the requesting instance. The LMSx also controls the flow of messages to remote instances.

The LMSn processes handle the blocking interrupts from the remote instance for the Global Cache Service resources by:
Managing the resource requests and cross-instance call operations for the shared resources.

Building a list of invalid lock elements and validating the lock elements during recovery.

Handling the global lock deadlock detection and Monitoring for the lock conversion timeouts.


LCKx
This process manages the global enqueue requests and the cross-instance broadcast. Workload is automatically shared and balanced when there are multiple Global Cache Service Processes (LMSx). This process is called as instance enqueue process. This process manages non-cache fusion resource requests such as library and row cache requests. The instance locks that are used to share resources between instances are held by the lock processes.


DIAG
Diagnosability Daemon – Monitors the health of the instance and captures the data for instance process failures.


RMSn
This process is called as Oracle RAC Management Service/Process. These processes perform manageability tasks for Oracle RAC. Tasks include creation of resources related Oracle RAC when new instances are added to the cluster.

RSMN
This process is called as Remote Slave Monitor. This process manages background slave process creation and communication on remote instances. This is a background slave process. This process performs tasks on behalf of a coordinating process running in another instance.


Oracle RAC instances use two processes GES(Global Enqueue Service), GCS(Global Cache Service) that enable cache fusion. The GES and GCS maintain records of the statuses of each datafile and each cached block using global resource directory (GRD). This process is referred to as cache fusion and helps in data integrity.

Oracle RAC is composed of two or more instances. When a block of data is read from datafile by an instance within the cluster and another instance is in need of the same block, it is easy to get the block image from the instance which has the block in its SGA rather than reading from the disk. To enable inter instance communication Oracle RAC makes use of interconnects. The Global Enqueue Service(GES) monitors and Instance enqueue process manages the cache fusion.
