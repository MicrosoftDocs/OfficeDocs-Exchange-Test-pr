---
title: 'FAQ: Exchange admin center: Exchange 2013 Help'
TOCTitle: 'FAQ: Exchange admin center'
ms:assetid: 3de0042f-74a6-458f-947c-3cd6eeacd6ab
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ552409(v=EXCHG.150)
ms:contentKeyID: 48679374
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# FAQ: Exchange admin center

 

_**Applies to:** Exchange Server 2013_


This topic provides you with a list of frequently asked questions for the new Exchange admin center (EAC) in Microsoft Exchange Server 2013. Have other questions about EAC not answered here? Send us an email at [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## Was the EAC developed solely for Exchange Online?

The EAC serves all deployment options for Exchange 2013, including customers who want to deploy on-premises, in the cloud with Exchange Online, or a hybrid deployment.

## Did you remove the Exchange Management Console (EMC) because you’re building the interface primarily for small and mid-sized customers?

The EAC was developed to provide a single, intuitive management experience for all our customers and was designed to help make the execution of the most common administration tasks simpler.

We created a single interface that provides a superset of scenario coverage over the Exchange Management Console (EMC) and the Exchange Control Panel (ECP) and one that addressed key challenges and scenarios for customers.

Additionally, we listened to customers of all sizes and their primary concerns were the following:

  - Maintaining and downloading patches in order to operate an administrative tool is an operational overhead for customers which, in turn, increases operational costs.

  - As the IT workforce becomes increasingly mobile, customers wanted to be able to manage their environments from anywhere, not only from the desktops and servers where their administrative tools are installed.

  - Using multiple tools for different deployment options becomes confusing and increases training and operational costs

## Is PowerShell logging and cmdlet exposure coming back to EAC?

We have taken early customer feedback on this and are evaluating the possibility of addressing this in a future update.

## Will the EMC be reintroduced an upcoming service pack?

No. We fully support the EAC experience.

## Can you use the Exchange 2010 EMC to manage Exchange 2013 objects?

No. You can’t use the Exchange 2010 EMC to manage Exchange 2013 objects and servers. While customers upgrade to Exchange 2013, we encourage them to use the EAC to:

1.  Manage Exchange 2013 mailboxes, servers, and corresponding services.

2.  View and update Exchange 2010 mailboxes and properties.

3.  View and update Exchange 2007 mailboxes and properties.

We encourage customers to use Exchange 2010 EMC to create and manage Exchange 2010 mailboxes.

We encourage customers to use Exchange 2007 EMC to create and manage Exchange 2007 mailboxes.

Customers can continue to perform management tasks using the Exchange Management Shell and script tasks.

## Why isn’t the search box always visible?

As part of our design principles for Exchange 2013, we wanted to help make sure that nothing is in your way until you need it. This simplicity is represented in all our end user experiences (including the EAC). The search box slides out after you click the icon. This provides more room for the user to type their query in the text box, and also provides type-downs that display once real-time query matching occurs. This improvement allows us to hide unnecessary complexity without diminishing the management experience. We will continue to enhance all of our experiences based on feedback.

## Will EAC work on tablets?

Administration through tablets and mobile devices isn’t supported at this time.

## Why does Exchange 2010 ECP open when I try to access the Exchange 2013 EAC?

If your mailbox exists on an Exchange 2010 Mailbox server, the Exchange 2010 ECP will automatically load in your browser. This is by design. You can access the EAC by adding the Exchange version to the URL. For example, to access the EAC whose virtual directory is hosted on the Client Access server CAS01-NA, use the following URL: `https://CAS01-NA/ecp?ExchClientVer=15`.

## How do you limit where EAC can be used?

To limit Internet versus intranet access, Exchange provides partitioning at the level of the virtual directory in IIS. Administrators can explicitly allow or deny IT management scenarios from being performed by external internet clients (for example, from clients not joined to a domain within the corporate firewall). For more information, see [Turn off access to the Exchange admin center](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

## What’s changed for the Exchange 2013 Toolbox?

In Exchange 2007 and Exchange 2010, the EMC contained the Toolbox, which provided access to various tools for managing your Exchange organization. The Exchange 2013 Toolbox is considerably pared down from the previous versions. The Details Templates Editor, Remote Connectivity Analyzer, and the Queue Viewer are still available in the Exchange 2013 Toolbox. The remaining tools were either repurposed or moved into the EAC.

The following table lists the changes to the Exchange 2013 Toolbox:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tool</th>
<th>Where is it now?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practices Analyzer (ExBPA)</p></td>
<td><p>The ExBPA has been retired. Readiness checks have replaced the ExBPA to make sure that your Active Directory forest and Exchange servers are ready for Exchange 2013. Each readiness check topic describes the actions that you can take to resolve issues that are found when the readiness checks are run. You should only perform the steps outlined in a readiness check topic if that readiness check was displayed during setup.</p></td>
</tr>
<tr class="even">
<td><p>Mail Flow Troubleshooter</p></td>
<td><p>The Mail Flow Troubleshooter has been retired. You can now use the messaging tracking feature in the EAC. Go to <strong>Mail flow</strong> &gt; <strong>Delivery reports</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Performance Monitor</p></td>
<td><p>The Performance Monitor has been retired from the Toolbox. You can still find the Performance Monitor under <strong>Administrative Tools</strong> in Windows Server 2008 and Windows Server 2012.</p></td>
</tr>
<tr class="even">
<td><p>Performance Troubleshooter</p></td>
<td><p>The Performance Troubleshooter has been retired from the Toolbox.</p></td>
</tr>
<tr class="odd">
<td><p>Routing Log Viewer</p></td>
<td><p>The Routing Log Viewer has been retired.</p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management Console</p></td>
<td><p>Public folders are now managed from within the EAC. In the EAC, go to <strong>Public Folders</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Role Based Access Control (RBAC) User Editor</p></td>
<td><p>RBAC is now managed from within the EAC. In the EAC, go to <strong>Permissions</strong>.</p></td>
</tr>
</tbody>
</table>

