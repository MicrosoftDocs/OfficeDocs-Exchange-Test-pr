---
title: 'Shared free/busy in Exchange hybrid deployments: Exchange 2013 Help'
TOCTitle: Shared free/busy in Exchange hybrid deployments
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 49345771
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Shared free/busy in Exchange hybrid deployments

 

_**Applies to:** Exchange Server 2013, Exchange Server 2016_


Sharing free/busy (calendar availability) information between users located on-premises and in the Exchange Online organization is one of the primary benefits of a hybrid deployment. Users in both organizations can view each other's calendars just as if they were located in the same physical organization. This makes scheduling meetings and resources easy and efficient.

Several components in a hybrid deployment are required to enable the shared free/busy feature between your on-premises Exchange organization and Exchange Online.

  - **Federation trust**   Both the on-premises and Office 365 service organizations need to have a federation trust established with the Azure AD authentication system. A federation trust is a one-to-one relationship with the Azure AD authentication system that defines parameters for your Exchange organization. The system uses these parameters when acting as a trust broker between your on-premises and Office 365 service organization to exchange free/busy information between on-premises and Exchange Online organization users.
    
    A federation trust with the system is automatically configured for your Office 365 service organization when the account is created. The Hybrid Configuration wizard automatically checks to see if there is an existing federation trust with the Azure AD authentication system for the on-premises organization. If present, the existing federation trust is used to support the hybrid deployment. If not present, the wizard creates a federation trust for the on-premises organization with the Azure AD authentication system. The wizard also adds any domains selected within the Hybrid Configuration wizard to the on-premises organization federation trust.
    
    Learn more at [Sharing](https://technet.microsoft.com/en-us/library/dd638083\(v=exchg.150\)).

  - **Organization relationships**   Organization relationships are needed for both the on-premises and Exchange Online organization and are configured automatically by the Hybrid Configuration wizard. An organization relationship defines the level of free/busy information shared for an organization.
    
    By default, the free/busy data access sharing level is **Free/busy access with time, plus subject and location** for both the on-premises and Exchange Online organization relationships. If you want to modify the free/busy sharing access between your on-premises and Exchange Online organization users, you can manually configure the organization relationship access level after the Hybrid Configuration wizard has completed.
    
    Learn more at [Sharing](https://technet.microsoft.com/en-us/library/dd638083\(v=exchg.150\)).

When configuring your organization for a hybrid deployment, configuring shared free/busy calendar access is automatically configured by the Hybrid Configuration wizard in all scenarios. Creating a federation trust with the Azure AD authentication system and configuring organization relationships for the on-premises and Exchange Online organization are hybrid deployment requirements. If you don't want to allow free/busy sharing between your on-premises and Exchange Online organization users in the hybrid deployment, you can manually disable free/busy sharing by using the Exchange Management Shell and the [Set-HybridConfiguration](https://technet.microsoft.com/en-us/library/hh529932\(v=exchg.150\)) cmdlet after the Hybrid Configuration wizard has completed.

The hybrid deployment features shown in the following table have a dependency on federation trusts and organization relationships.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Messaging area</th>
<th>Feature</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Email client</p></td>
<td><ul>
<li><p>Message tracking</p></li>
<li><p>MailTips</p></li>
<li><p>Multi-mailbox search</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Compliance</p></td>
<td><ul>
<li><p>Exchange Online Archiving</p></li>
<li><p>Exchange In-place eDiscovery</p></li>
</ul></td>
</tr>
</tbody>
</table>

