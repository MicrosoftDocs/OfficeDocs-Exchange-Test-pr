---
title: 'Anti-Virus Software in the Operating System on Exchange Servers: Exchange 2013 Help'
TOCTitle: Anti-Virus Software in the Operating System on Exchange Servers
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 48385271
ms.date: 07/22/2016
mtps_version: v=EXCHG.150
---

# Anti-Virus Software in the Operating System on Exchange Servers

 

_**Applies to:** Exchange Server 2013_


This topic describes the effects of file-level antivirus programs on computers that are running Microsoft Exchange Server 2013. If you implement the recommendations described in this topic, you can help enhance the security and health of your Exchange organization.

File-level scanners are frequently used. However, if they are configured incorrectly, they can cause problems in Exchange 2013. There are two types of file-level scanners:

  - *Memory-resident file-level scanning* refers to a part of file-level antivirus software that is loaded in memory at all times. It checks all the files that are used on the hard disk and in computer memory.

  - *On-demand file-level scanning* refers to a part of file-level antivirus software that you can configure to scan files on the hard disk manually or on a schedule. Some versions of antivirus software start the on-demand scan automatically after virus signatures are updated to make sure that all files are scanned with the latest signatures.

The following problems may occur when you use file-level scanners with Exchange 2013:

  - File-level scanners may scan a file when the file is being used or at a scheduled interval. This can cause the scanners to lock or quarantine an Exchange log or a database file while Exchange 2013 tries to use the file. This behavior may cause a severe failure in Exchange 2013 and may also cause -1018 event log errors.

  - File-level scanners don't provide protection against email viruses, such as Storm Worm. Storm Worm was a backdoor Trojan horse program that propagated itself through email messages. The worm joined the infected computer to a botnet, where the computer was used to send spam in periodic bursts.

## Recommendations for using file-level scanning with Exchange 2013

If you're deploying file-level scanners on Exchange 2013 servers, make sure that the appropriate exclusions, such as directory exclusions, process exclusions, and file name extension exclusions, are in place for both memory-resident and file-level scanning. This section describes recommended directory exclusions, process exclusions, and file name extension exclusions.

**Contents**

Directory exclusions

Process exclusions

File name extension exclusions

## Directory exclusions

You must exclude specific directories for each Exchange server on which you run a file-level antivirus scanner. This section describes the directories that you should exclude from file-level scanning.

  - **Mailbox servers**
    
      - **Mailbox databases**
        
          - Exchange databases, checkpoint files, and log files. By default, these are located in sub-folders under the %ExchangeInstallPath%Mailbox folder. To determine the location of a mailbox database, transaction log, and checkpoint file, run the following command: `Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - Database content indexes. By default, these are located in the same folder as the database file.
        
          - Group Metrics files. By default, these files are located in the %ExchangeInstallPath%GroupMetrics folder.
        
          - General log files, such as message tracking and calendar repair log files. By default, these files are located in subfolders under the %ExchangeInstallPath%TransportRoles\\Logs folder and %ExchangeInstallPath%Logging folder. To determine the log paths being used, run the following command in the Exchange Management Shell: `Get-MailboxServer <servername> | Format-List *path*`
        
          - The Offline Address Book files. By default, these are located in subfolders under the %ExchangeInstallPath%ClientAccess\\OAB folder.
        
          - IIS system files in the %SystemRoot%\\System32\\Inetsrv folder.
        
          - The Mailbox database temporary folder: %ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **Members of Database Availability Groups**
        
          - All the items listed in the **Mailbox databases** list, and the cluster quorum database that exists at %Windir%\\Cluster.
        
          - The witness directory files. These files are located on another server in the environment, typically a Client Access server that isn’t installed on the same computer as a Mailbox server. By default, the witness directory files are located in %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\>.
    
      - **Transport service**
        
          - Log files, for example, message tracking and connectivity logs. By default, these files are located in subfolders under the %ExchangeInstallPath%TransportRoles\\Logs folder. To determine the log paths being used, run the following command in the Exchange Management Shell: `Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - Pickup and Replay message directory folders. By default, these folders are located under the %ExchangeInstallPath%TransportRoles folder. To determine the paths being used, run the following command in the Exchange Management Shell: `Get-TransportService <servername>| Format-List *dir*path*`
        
          - The queue databases, checkpoints, and log files. By default, these are located in the %ExchangeInstallPath%TransportRoles\\Data\\Queue folder.
        
          - The Sender Reputation database, checkpoint, and log files. By default, these are located in the %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation folder.
        
          - The temporary folders that are used to perform conversions:
            
              - By default, content conversions are performed in the Exchange server’s %TMP% folder.
            
              - By default, rich text format (RTF) to MIME/HTML conversions are performed in %ExchangeInstallPath%\\Working\\OleConverter folder.
        
          - The content scanning component is used by the Malware agent and data loss prevention (DLP). By default, these files are located in the %ExchangeInstallPath%FIP-FS folder.
    
      - **Mailbox Transport service**
        
          - Log files, for example, connectivity logs. By default, these files are located in subfolders under the %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox folder. To determine the log paths being used, run the following command in the Exchange Management Shell: `Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **Unified Messaging**
        
          - The grammar files for different locales, for example en-EN or es-ES. By default, these are stored in the subfolders in the %ExchangeInstallPath%UnifiedMessaging\\grammars folder.
        
          - The voice prompts, greetings and informational message files. By default, these are stored in the subfolders in the %ExchangeInstallPath%UnifiedMessaging\\Prompts folder
        
          - The voicemail files that are temporarily stored in the %ExchangeInstallPath%UnifiedMessaging\\voicemail folder.
        
          - The temporary files generated by Unified Messaging. By default, these are stored in the %ExchangeInstallPath%UnifiedMessaging\\temp folder.
    
      - **Setup**
        
          - Exchange Server setup temporary files. These files are typically located in %SystemRoot%\\Temp\\ExchangeSetup.
    
      - **Exchange Search service**
        
          - Temporary files used by the Exchange Search service and Microsoft Filter Pack to perform file conversion in a sandboxed environment. These files are located in %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\.

<!-- end list -->

  - **Client Access servers**
    
      - **Web components**
        
          - For servers using Internet Information Services (IIS) 7.0, the compression folder that is used with Microsoft Outlook Web App. By default, the compression folder for IIS 7.0 is located at %SystemDrive%\\inetpub\\temp\\IIS Temporary Compressed Files.
        
          - IIS system files in the %SystemRoot%\\System32\\Inetsrv folder
        
          - Inetpub\\logs\\logfiles\\w3svc
        
          - Sub-folders in %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET Files
    
      - **POP3 and IMAP4 protocol logging**
        
          - POP3 folder: %ExchangeInstallPath%Logging\\POP3
        
          - IMAP4 folder: %ExchangeInstallPath%Logging\\IMAP4
    
      - **Front End Transport service**
        
          - Log files, for example, connectivity logs and protocol logs. By default, these files are located in subfolders under the %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd folder. To determine the log paths being used, run the following command in the Exchange Management Shell: `Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **Setup**
        
          - Exchange Server setup temporary files. These files are typically located in %SystemRoot%\\Temp\\ExchangeSetup.

Return to top

## Process exclusions

Many file-level scanners now support the scanning of processes, which can adversely affect Microsoft Exchange if the incorrect processes are scanned. Therefore, you should exclude the following processes from file-level scanners.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Process</th>
<th>Path</th>
<th>Comments</th>
<th>Servers</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>Active Directory Lightweight Directory Services (AD LDS) on subscribed Edge Transport servers.</p></td>
<td><p>Edge Transport servers</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Transport service worker process</p></td>
<td><p>Mailbox servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Content scanning component that's used by the Malware agent and DLP.</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Microsoft Exchange Search Host Controller service (HostControllerService)</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Anti-spam Update service (MSExchangeAntispamUpdate)</p></td>
<td><p>Mailbox servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>Content Filter agent</p></td>
<td><p>Mailbox servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Diagnostics service (MSExchangeDiagnostics)</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Active Directory Topology service (MSExchangeADTopology)</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Credential service (MSExchangeEdgeCredential)</p></td>
<td><p>Edge Transport servers</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange EdgeSync service (MSExchangeEdgeSync)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 service (MSExchangeImap4)</p></td>
<td><p>Client Access servers</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 Backend service (MSExchangeIMAP4BE)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange POP3 service (MSExchangePop3)</p></td>
<td><p>Client Access servers</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange POP3 Backend service (MSExchangePOP3BE)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Service Host service (MSExchangeServiceHost)</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange RPC Client Access service (MSExchangeRPC)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Search service (MSExchangeFastSearch)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Service Host service (MSExchangeServiceHost)</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Information Store service (MSExchangeIS)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Information Store service worker process</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Microsoft Exchange Unified Messaging Call Router service (MSExchangeUMCR)</p></td>
<td><p>Client Access servers</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange DAG Management service (MSExchangeDagMgmt)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Mailbox Transport Delivery service (MSExchangeDelivery)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Frontend Transport service (MSExchangeFrontEndTransport)</p></td>
<td><p>Client Access servers</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Health Manager service (MSExchangeHM)</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Health Manager service worker process</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Mailbox Assistants service (MSExchangeMailboxAssistants)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Mailbox Replication service (MSExchangeMailboxReplication)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Migration Workflow service (MSExchangeMigrationWorkflow)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Replication service (MSExchangeRepl)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Mailbox Transport Submission service (MSExchangeSubmission)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Transport service (MSExchangeTransport)</p></td>
<td><p>Mailbox servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Transport Log Search service (MSExchangeTransportLogSearch)</p></td>
<td><p>Mailbox servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Throttling service (MSExchangeThrottling)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Microsoft Exchange Search service (MSExchangeFastSearch)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Converts rich text format (RTF) messages to MIME/HTML for external recipients.</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Microsoft Exchange Search service (MSExchangeFastSearch)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Exchange Management Shell</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p>
<p>Edge Transport servers</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Content scanning component that's used by the Malware agent and DLP.</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Content scanning component that's used by the Malware agent and DLP.</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>WebReady Document Viewing in Outlook Web App.</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Unified Messaging service (MSExchangeUM)</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Unified Messaging service worker process</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Content scanning component that's used by the Malware agent and DLP.</p></td>
<td><p>Mailbox servers</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>Mailbox servers</p>
<p>Client Access servers</p></td>
</tr>
</tbody>
</table>


Return to top

## File name extension exclusions

In addition to excluding specific directories and processes, you should exclude the following Exchange-specific file name extensions in case directory exclusions fail or files are moved from their default locations.

  - Application-related extensions:
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - Database-related extensions:
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - Offline address book-related extensions:
    
      - .lzx

<!-- end list -->

  - Content Index-related extensions:
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - Unified Messaging-related extensions:
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - Group Metrics-related extensions:
    
      - .dsc
    
      - .txt

Return to top

