---
title: 'IIS 7 component not installed_LonghornIIS7WindowsAuthNotInstalled: Exchange 2013 Help'
TOCTitle: IIS 7 component not installed_LonghornIIS7WindowsAuthNotInstalled
ms:assetid: f0e75196-5d0d-4e6d-8931-e6c576f55caa
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.longhorniis7windowsauthnotinstalled(v=EXCHG.150)
ms:contentKeyID: 46629169
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# IIS 7 component not installed\_LonghornIIS7WindowsAuthNotInstalled

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2010 Setup or Microsoft Exchange Server 2007 Setup cannot install the Client Access Server (CAS) role or the Mailbox server role on a Microsoft Windows Server 2008-based computer or on a Windows Server 2008 R2-based computer because the required Internet Information Server (IIS) 7 components are not installed.

Exchange 2010 Setup and Exchange 2007 Setup require that the Windows Server 2008-based computer or the Windows Server 2008 R2-based computer on which you are installing the CAS role already has the following IIS 7 components installed.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Required IIS 7 Components for the CAS server role</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dynamic Content Compression</p></td>
</tr>
<tr class="even">
<td><p>Static Content Compression</p></td>
</tr>
<tr class="odd">
<td><p>Basic Authentication</p></td>
</tr>
<tr class="even">
<td><p>Windows Authentication</p></td>
</tr>
<tr class="odd">
<td><p>IIS 7 Digest Authentication</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>Client Certificate Mapping</p></td>
</tr>
<tr class="even">
<td><p>Directory Browsing</p></td>
</tr>
<tr class="odd">
<td><p>HTTP Errors</p></td>
</tr>
<tr class="even">
<td><p>HTTP Logging</p></td>
</tr>
<tr class="odd">
<td><p>HTTP Redirection</p></td>
</tr>
<tr class="even">
<td><p>Tracing</p></td>
</tr>
<tr class="odd">
<td><p>ISAPI Filters</p></td>
</tr>
<tr class="even">
<td><p>Request Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Static Content</p></td>
</tr>
</tbody>
</table>


Exchange 2010 Setup and Exchange 2007 Setup require that the Windows Server 2008-based computer or the Windows Server 2008 R2-based computer on which you are installing the Mailbox server role already has the following IIS 7 components installed.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Required IIS 7 Components for the Mailbox server role</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Basic Authentication</p></td>
</tr>
<tr class="even">
<td><p>Windows Authentication</p></td>
</tr>
</tbody>
</table>


To address this issue, follow the appropriate steps to install the required IIS 7 components on the destination computer, and then run Microsoft Exchange Setup again.

**Install the IIS 7 Components for the CAS server role by using the Windows Server 2008 Server Manager**

1.  Click **Start**, click **Administrative Tools**, and then click **Server Manager**.

2.  In the navigation pane, expand **Roles**, right-click **Web Server (IIS),** and then click **Add Role Services**.

3.  In the **Select Role Services** pane, scroll down to **IIS**.

4.  In the **Security** area, click to select the following check boxes:
    
      - **Basic Authentication**
    
      - **Digest Authentication**
    
      - **Windows Authentication**

5.  In the **Performance** area, click to select the following check boxes:
    
      - **Static Compression**
    
      - **Dynamic Compression**

6.  In the **Select Role Services** pane, click **Next**, and then click **Install** in the **Confirm Installations Selections** pane.

7.  Click **Close** to exit the Add Role Services wizard.

**Install the IIS 7 Components for the Mailbox server role by using the Windows Server 2008 Server Manager**

1.  Click **Start**, click **Administrative Tools**, and then click **Server Manager**.

2.  In the navigation pane, expand **Roles**, right-click **Web Server (IIS),** and then click **Add Role Services**.

3.  In the **Select Role Services** pane, scroll down to **IIS**.

4.  In the **Security** area, click to select the following check boxes:
    
      - **Basic Authentication**
    
      - **Windows Authentication**

5.  In the **Select Role Services** pane, click **Next**, and then click **Install** in the **Confirm Installations Selections** pane.

6.  Click **Close** to exit the Add Role Services wizard.

