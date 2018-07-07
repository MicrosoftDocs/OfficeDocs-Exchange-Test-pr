---
title: 'Checklist: Perform a new installation of Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Checklist: Perform a new installation of Exchange 2013'
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 49289467
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Checklist: Perform a new installation of Exchange 2013

 

_**Applies to:** Exchange Server 2013_


Use this checklist to deploy Microsoft Exchange Server 2013. Before you start working with this checklist, make sure you're familiar with the concepts discussed in:

  - [Planning and deployment](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Deployment security checklist](deployment-security-checklist-exchange-2013-help.md)

This checklist is generic in that it provides guidance for a typical scenario.


> [!NOTE]
> The Exchange Server Deployment Assistant provides you with customized step-by-step guidance about how to deploy Exchange Server. The Deployment Assistant can help you deploy a new installation of Exchange Server 2013, upgrade a previous version to Exchange 2013, or configure a hybrid deployment of Exchange 2013 and Exchange Online. To learn more, see <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server Deployment Assistant</A>.



## Checklist for a new installation of Exchange 2013


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Done?</p></td>
<td><p>Task</p></td>
<td><p>Topic</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Read the release notes.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Release notes for Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. Verify system requirements.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 system requirements</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. Confirm prerequisite steps are done.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 prerequisites</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. Configure disjoint namespace.</p>

> [!NOTE]
> This step is optional. It's only necessary if your organization is running a disjoint namespace.


</td>
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">Disjoint namespace scenarios</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. Install the Mailbox server role.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Install Exchange 2013 using the Setup wizard</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. Install the Client Access server role.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Install Exchange 2013 using the Setup wizard</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Install the Edge Transport server role.</p>

> [!NOTE]
> This step is optional. It's only necessary if you want to install an Edge Transport server. For more information, see <A href="edge-transport-servers-exchange-2013-help.md">Edge Transport servers</A>.


</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Install the Exchange 2013 Edge Transport role using the Setup wizard</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Create an EdgeSync subscription.</p>
<p>This step is optional. It's only necessary if you've installed an Edge Transport server and want to configure an EdgeSync subscription between your Edge Transport server and a Hub Transport server. For more information, see <a href="edge-subscriptions-exchange-2013-help.md">Edge Subscriptions</a>.</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configure Internet mail flow through a subscribed Edge Transport server</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Configure Transport.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Add additional accepted domains.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configure email address policies.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. Configure settings on virtual directories, including the offline address book, Exchange Web Services, Exchange Administration Center (EAC), Outlook Web App, and Exchange ActiveSync virtual directories.</p>

> [!NOTE]
> This step is necessary if you want to use Exchange Web Services, Outlook Anywhere, or the offline address book. It also may be required if you need to change any of the default settings for EAC, Outlook Web App, or Exchange ActiveSync.


</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. Add digital certificates on the Client Access server.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. Configure Unified Messaging.</p>

> [!NOTE]
> This step is optional. It's only necessary if you want to use Unified Messaging in your organization.


</td>
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Deploying voice mail and UM</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configure additional Unified Messaging and Lync Server settings.</p>

> [!NOTE]
> This step is optional. It's only necessary if you’ve configured Unified Messaging in your organization and want to integrate it with Lync Server.


</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Deploying Exchange 2013 UM and Lync Server overview</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. Post-installation tasks.</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 post-Installation tasks</a></p></td>
</tr>
</tbody>
</table>

