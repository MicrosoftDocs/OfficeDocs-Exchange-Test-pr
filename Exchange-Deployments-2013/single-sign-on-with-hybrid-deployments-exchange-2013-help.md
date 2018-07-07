---
title: 'Single sign-on with hybrid deployments: Exchange 2013 Help'
TOCTitle: Single sign-on with hybrid deployments
ms:assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Hh563846(v=EXCHG.150)
ms:contentKeyID: 48157712
ms.date: 02/05/2016
mtps_version: v=EXCHG.150
---

# Single sign-on with hybrid deployments

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


Single sign-on enables users to access both the on-premises and Office 365 organizations with a single user name and password. It provides users with a familiar sign-on experience and can allow administrators to easily control account policies for Exchange Online organization mailboxes by using on-premises Active Directory management tools. While you don't have to configure a hybrid deployment with single sign-on enabled, we strongly recommend that you do. Without single sign-on, users will need to remember two different sets of credentials, one for your on-premises organization, and one for Office 365. Here are a few other advantages to single sign-on:

  - **Exchange Online Archiving**   When single sign-on is deployed, on-premises Outlook users are prompted for their credentials when accessing archived content in the Exchange Online organization for the first time. However, users can then temporarily avoid future credential prompting by choosing “save password” and then will only be prompted for credentials again when their on-premises account password is changed. If single sign-on isn’t deployed in Exchange organizations and Exchange Online Archiving is enabled, the on-premises user principal name (UPN) must match their Exchange Online account and users will always be prompted for their on-premises credentials when accessing their archive.

  - **Policy control**   You can control account policies through Active Directory, which gives you the ability to manage password policies, workstation restrictions, lock-out controls, and more, without having to perform additional tasks in your Office 365 organization.

  - **Reduced support calls**   Forgotten passwords are a common source of support calls in all companies. If users have fewer passwords to remember, they are less likely to forget them.

You have a couple of options when deploying single sign-on: password synchronization and Active Directory Federation Services (AD FS). Both options are provided by Azure Active Directory Connect. We strongly recommend using the password synchronization method unless you have a specific need that requires AD FS. Password synchronization provides many of the same benefits of AD FS without the complexity of its deployment. The following table provides some common advantages and disadvantages for each option.


> [!NOTE]
> By default, if you deploy AD FS and your on-premises AD FS servers aren't reachable from the Internet for any reason, Office 365 will fall back to password synchronization to authenticate users. This allows users with Office 365 mailboxes to continue working uninterrupted even if your on-premises servers aren't available.



To learn more about each option, see [Azure AD Connect User Sign-on options](http://go.microsoft.com/fwlink/p/?linkid=723514)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Single sign-on method</p></th>
<th><p>Advantages</p></th>
<th><p>Disadvantages</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Password synchronization (recommended)</p></td>
<td><ul>
<li><p>Significantly less complex than AD FS</p></li>
<li><p>Users can log in to Office 365 even if your on-premises Active Directory is unavailable.</p></li>
<li><p>Fewer additional servers are required to deploy password synchronization.</p></li>
<li><p>No third-party certificates are required.</p></li>
<li><p>Doesn't require external access to your on-premises Active Directory via AD FS.</p></li>
<li><p>Deployment can often be completed in just a few hours.</p></li>
</ul></td>
<td><ul>
<li><p>Disabling a user account in your on-premises Active Directory doesn't disable it in Office 365. You need to manually disable the account in the Office 365 Admin portal.</p></li>
<li><p>Requires on-premises Active Directory. Other directory services aren't supported.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AD FS</p></td>
<td><ul>
<li><p>Password changes are immediate.</p></li>
<li><p>Disabling a user in your on-premises Active Directory disables both their on-premises network access and their Office 365 account.</p></li>
<li><p>Supports directory services other than Active Directory.</p></li>
<li><p>Supports very large and diverse deployments.</p></li>
<li><p>Support for two-factor authentication.</p></li>
</ul></td>
<td><ul>
<li><p>Requires more servers, at least one of which needs to reside in your perimeter network.</p></li>
<li><p>Requires a public IP address and TCP port 443 to be opened on your firewall.</p></li>
<li><p>Connectivity with your on-premises Active Directory is required to detect changes to account passwords and with an account has recently been enabled or disabled.</p></li>
</ul></td>
</tr>
</tbody>
</table>

