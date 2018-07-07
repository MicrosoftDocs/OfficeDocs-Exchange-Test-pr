---
title: 'The primary DNS server cannot be contacted_PrimaryDNSTestFailed: Exchange 2013 Help'
TOCTitle: The primary DNS server cannot be contacted_PrimaryDNSTestFailed
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 46628919
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# The primary DNS server cannot be contacted\_PrimaryDNSTestFailed

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup cannot continue because communication with the primary Domain Name System (DNS) server cannot be established.

Exchange 2007 setup requires that the local computer communicate with the authoritative DNS database for the domain.

Microsoft Exchange depends on DNS to resolve the IP Address of its next internal or external destination server.

Communication with the primary DNS server can fail for the following reasons:

  - The local TCP/IP configuration does not point to the correct DNS server.

  - The DNS server is down or unreachable because of a network failure or other reasons.

To resolve this issue:

  - Verify that the local TCP/IP configuration points to the correct DNS server.

**To verify the local TCP/IP configuration**

1.  Review the local TCP/IP configuration:
    
    For more information, see "Configure TCP/IP to use DNS" ([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094)).

<!-- end list -->

  - Verify that the DNS server is running and can be contacted.

**To verify that the DNS server is running and can be contacted**

1.  Verify that the DNS server is running by doing one or more of the following checks:
    
      - Look at the DNS server status from the DNS Administration program on the DNS server.
    
      - Restart the DNS server.
        
        For more information, see "Start, stop, pause, or restart a DNS server" ([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999)).
    
      - Verify the DNS server responsiveness by using the **nslookup** command.
        
        For more information, see the instructions in "Verify DNS server responsiveness using the nslookup command" ([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000)).

