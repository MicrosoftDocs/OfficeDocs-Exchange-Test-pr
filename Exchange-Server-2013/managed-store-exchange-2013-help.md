---
title: 'Managed Store: Exchange 2013 Help'
TOCTitle: Managed Store
ms:assetid: efdaf80b-335c-491c-8eb5-1fafd297e8a2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn792020(v=EXCHG.150)
ms:contentKeyID: 62613984
ms.date: 06/04/2016
mtps_version: v=EXCHG.150
---

# Managed Store

 

_**Applies to:** Exchange Server 2013_


All previous versions of Exchange Server, from Exchange Server 4.0 to Exchange Server 2010, have supported running a single instance of the Information Store process (Store.exe) on the Mailbox server role. This single Store instance hosts all databases on the server: active, passive, lagged, and recovery. In the previous Exchange architectures, there is little, if any, isolation between the different databases hosted on a Mailbox server. An issue with a single mailbox database has the potential to negatively affect all other databases, and crashes resulting from a mailbox corruption can affect service for all users whose databases are hosted on that server.

Another challenge with a single Store instance in previous versions of Exchange is that the Extensible Storage Engine (ESE) scales well to 8-12 processor cores, but beyond that, cross-processor communication and cache synchronization issues lead to negative scale. Given today’s much larger servers, with 16+ core systems available, this would mean impose the administrative challenge of managing the affinity of 8-12 cores for ESE and using the other cores for non-Store processes (for example, Assistants, Search Foundation, Managed Availability, etc.). Moreover, the previous architecture restricted scale-up for the Store process.

The Store.exe process has evolved considerably throughout the years as Exchange Server itself evolved, but as a single process, ultimately its scalability is limited, and it represents a single point of failure. Because of these limits, Store.exe is gone in Exchange 2013 and replaced by the Managed Store.

## Managed Store

The Managed Store is the name for the Information Store (aka the Store) processes in Exchange Server 2013. The Managed Store uses a controller/worker process model that provides storage process isolation and faster database failover. The Managed Store also includes a new static database caching mechanism that replaces the dynamic buffer algorithm in previous versions of Exchange Server. In the multi-process model used by the Managed Store, there is a single store service controller process (in this case, Microsoft.Exchange.Store.Service.exe aka MSExchangeIS), and one worker process (in this case, Microsoft.Exchange.Store.Worker.exe) for each mounted database. When a database is mounted, a new worker process is instantiated that services only that database. When a database is dismounted, the worker process for that database is terminated.

For example, if you have 40 databases mounted on a server, there will be 41 processes running for the Managed Store, one for each database, and one for the store service process controller.

The store service process controller is very thin and very reliable, but if it dies or is terminated, all of its worker processes die (they will detect the service controller process is gone and exit). The store process controller monitors the health of all store worker processes on the server. A forcible or unexpected termination the Microsoft.Exchange.Store.Service.exe causes an immediate failover of all active database copies. The Managed Store is also tightly integrated with the Microsoft Exchange Replication service (MSExchangeRepl.exe) and Active Manager. The controller process, worker processes, and Replication service work together to provide greater availability and reliability:

  - Microsoft Exchange Replication service process (MSExchangeRepl.exe)
    
      - Responsible for issuing mount and dismount operations to the Store
    
      - Initiates recovery action on storage or database failures reported by the Store, the Extensible Storage Engine (ESE), and Managed Availability responders
    
      - Detects unexpected database failures
    
      - Provides the administrative interface for management tasks

  - Store service process/controller (Microsoft.Exchange.Store.Service.exe)
    
      - Manages each worker process lifetime based on the mount and dismount operations received from the Replication service
    
      - Handles incoming requests from the Windows Service Control Manager
    
      - Logs failure items when store worker process problems detected (for example, hang or unexpected exit)
    
      - Terminates store worker processes in response failover event

  - Store worker process (Microsoft.Exchange.Store.Worker.exe)
    
      - Responsible for executing RPC operations for mailboxes on a database
    
      - RPC endpoint instance within worker process is the database GUID
    
      - Provides database cache for a database

## Static Database Caching Algorithm

The database caching algorithm known as dynamic buffer allocation that was introduced in Exchange Server 5.5 and also used by the Information Store in Exchange 2000 Server, Exchange Server 2003, Exchange Server 2007 and Exchange Server 2010, is also gone from Exchange 2013. Exchange 2013 uses a very simple and straightforward algorithm for determining database cache. The Managed Store no longer dynamically reallocates cache between databases when failover occurs, which greatly simplifies internal cache management. Instead, the memory allocated for each database cache (e.g., each store worker process) is based on number of local database copies and value of *MaximumActiveDatabases*, if configured. If the value of *MaximumActiveDatabases* is greater than number of current database copies, then the cache calculation is based on the number of database copies.

The static algorithm used by Exchange 2013 allocates memory for each store worker process’ ESE cache based on physical RAM. This is referred to as a database’s *Max Cache Target*. 25% of total server memory is allocated to the ESE cache. This is referred to as the *Server Cache Size Target*.


> [!NOTE]
> The Server Cache Size Target, and therefore the amount of memory allocated to the Store for ESE cache, can be overridden using <EM>msExchESEParamCacheSizeMax</EM> attribute of the <EM>InformationStore</EM> object in Active Directory (the value configured is the number of 32 KB pages to allocate across all store processes).



A static amount of this cache is allocated to active and passive copies. The store worker process will be allocated the Max Cache Target only when servicing an active database copy. Passive database copies are allocated 20 percent of the Max Cache Target. The remainder is reserved by the Store, and allocated to the worker process if the database transitions from passive to active.

Max Cache Target is calculated only at Store startup. Therefore, if you add or remove databases or database copies, you must restart the Store controller service (MSExchangeIS) so that the cache can be adjusted accordingly. If the service is not restarted, then newly created databases will have a smaller cache size target than databases created prior to the service startup. In this event, the sum of database cache size targets will likely exceed the Server Cache Size Target until MSExchangeIS is restarted.

## Example Database Cache Calculations

Below are example database caching calculations that are based on a Mailbox server’s memory and database configuration.

**Example 1**

In this example, the Mailbox server has 48 GB of memory, and it hosts two active databases and two passive databases. In addition, the *MaximumActiveDatabases* parameter is not configured. In this configuration, the amount of database cache is 3 GB for each active database copy worker process and 0.6 GB for each passive database copy worker process. Here’s how these values were obtained.

To get the Server Cache Size Target, multiply the amount memory by 25%:

48 GB X 25% = 12 GB

To get the Database Max Cache Target, divide the Server Cache Size Target by the total number of active and passive databases:

12 GB / 4 databases = 3 GB

To determine the amount of memory used for the passive database copies, multiply the Database Max Cache Target by 20%:

3 GB X 20% = 0.6 GB

Out of the 12 GB of memory assigned to the Server Cache Size Target, 7.2 GB will be in use by database worker processes, and 4.8 GB will be reserved by the Information Store for the two passive database copies in case they become active copies. In that event, they will use their Max Cache Target of 3 GB.

**Example 2**

In this example, the Mailbox server also has 48 GB of memory and hosts two active databases and two passive databases; however, the *MaximumActiveDatabases* parameter is configured with a value of 2. In this configuration, the amount of database cache is 5 GB for each active database copy worker process and 0.2 GB for each passive database copy worker process. Here’s how these values were obtained.

To get the Server Cache Size Target, multiply the amount memory by 25%:

48 GB X 25% = 12 GB

To get the Database Max Cache Target, divide the Server Cache Size Target by the total number of active database plus the total number of passive databases multiplied by 20%:

12 GB / (2A + (2P X 20%)) = 5 GB

To determine the amount of memory used for the passive database copies, multiply the Database Max Cache Target by 20%:

5 GB X 20% = 1 GB

Out of the 12 GB of memory assigned to the Server Cache Size Target, 12 GB will be in use by database worker processes, and no memory will be reserved by the Information Store for the two passive database copies because they cannot become active copies in this configuration (because *MaximumActiveDatabases* is configured with a value of 2, and there are already 2 active database copies on the server).

