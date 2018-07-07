---
title: 'Place all mailboxes on hold: Exchange 2013 Help'
TOCTitle: Place all mailboxes on hold
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62527086
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Place all mailboxes on hold

 

_**Applies to:** Exchange Online, Exchange Server 2013_



> [!NOTE]
> We've postponed the July 1, 2017 deadline for creating new In-Place Holds in Exchange Online (in Office 365 and Exchange Online standalone plans). But later this year or early next year, you won't be able to create new In-Place Holds in Exchange Online. As an alternative to using In-Place Holds, you can use <A href="https://go.microsoft.com/fwlink/?linkid=780738">eDiscovery cases</A> or <A href="https://go.microsoft.com/fwlink/?linkid=827811">retention policies</A> in the Office 365 Security &amp; Compliance Center. After we decommission new In-Place Holds, you'll still be able to modify existing In-Place Holds, and creating new In-Place Holds in Exchange Server 2013 and Exchange hybrid deployments will still be supported. And, you'll still be able to place mailboxes on Litigation Hold.



Your organization may require all mailbox data to be preserved for a specific period. You can use Litigation Hold or In-Place Hold to meet this requirement. After you place a mailbox on Litigation Hold or In-Place Hold, mailbox items that are modified or that are permanently deleted are preserved in the Recoverable Items folder. For more information, see [In-Place Hold and Litigation Hold](in-place-hold-and-litigation-hold-exchange-2013-help.md).

Before you place all mailboxes in an organization on Litigation Hold or In-Place Hold, consider the following:

  - When you place mailboxes on hold, content in a user's archive mailbox (if it's enabled) is also placed on hold.

  - Placing all mailboxes in an organization on hold can significantly impact mailbox sizes. In an Exchange Server 2013 deployment, plan for adequate storage to meet your organization’s preservation requirements. In Exchange Online, [mailbox storage limits](https://go.microsoft.com/fwlink/?linkid=403645) for your users depend on the user’s subscription license.

  - Preserving mailbox data for a long duration will result in growth of the Recoverable Items folder in a user’s primary mailbox and archive mailbox. The Recoverable Items folder has its own storage limit, so items in the folder don’t count towards the mailbox storage limit. In Exchange Server 2013 and Exchange Online, the default storage limit for the Recoverable Items folder is 30 GB.
    
      - In Exchange Online, the quota for the Recoverable Items folder is automatically increased to 100 GB when you place a mailbox on hold.
    
      - In Exchange Server 2013, we recommend that you periodically monitor the size of this folder to ensure it doesn’t reach the limit. For more information, see [Recoverable Items folder](recoverable-items-folder-exchange-2013-help.md).

## Choosing between Litigation Hold and In-Place Hold

Here are some factors to consider when deciding the hold feature you should use to place all mailboxes in your organization on hold.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>You want to…</th>
<th>Use Litigation Hold</th>
<th>Use In-Place Hold</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Use the EAC</p></td>
<td><p>Yes</p>
<p>For setting Litigation Hold, EAC is best suited for quick one-off actions on a few mailboxes. We recommend using the Shell for setting Litigation Hold for all users in your organization.</p></td>
<td><p>Yes</p>
<p>However, you can’t select more than 500 source mailboxes in the EAC.</p></td>
</tr>
<tr class="even">
<td><p>Use the Shell</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="odd">
<td><p>Place more than 10,000 mailboxes on hold</p></td>
<td><p>Yes</p>
<p>Litigation Hold is a mailbox property. You can place all mailboxes in an organization on hold by using the <strong>Set-Mailbox</strong> cmdlet.</p></td>
<td><p>Yes; use multiple In-Place Holds</p>
<p>You can use distribution groups to specify a maximum of 10,000 mailboxes in a single In-Place Hold. To place additional mailboxes on hold, you must create additional In-Place Holds. This will result in additional management overhead. Using Litigation Hold placing large numbers of mailboxes on hold is simpler.</p></td>
</tr>
<tr class="even">
<td><p>Place many different mailboxes on hold for different periods.</p></td>
<td><p>Yes</p>
<p>Litigation Hold is a mailbox property. You can place each mailbox (or sets of mailboxes) on hold for a different duration.</p>
<p>See the More information section for examples of using recipient properties in a filter so you can place a Litigation Hold on a subset of mailboxes.</p></td>
<td><p>Yes</p>
<p>If you’re placing individual holds on thousands of mailboxes, we recommend using Litigation Hold. If you’re creating holds for specific events that involve multiple users, use a single in-Place hold for the group of users.</p>
<p>It’s not recommended to create separate In-place Holds for each mailbox as this will create many In-Place Hold queries that will be more difficult to manage than Litigation Holds. A large number of In-Place Hold objects may also result in slow performance in the EAC when refreshing, creating, or modifying hold objects.</p></td>
</tr>
<tr class="odd">
<td><p>Automatically place new mailboxes on hold</p></td>
<td><p>No</p>
<p>You have to place a new mailbox on Litigation Hold after it’s created. You can schedule the command or script to run as frequently as required to achieve the same effect.</p></td>
<td><p>No</p>
<p>You have to add a new mailbox to an In-Place Hold, even if you specified a distribution group when you created the In-Place Hold. You can also schedule the command or script to run as frequently as required to achieve the same effect. We recommend that the script check if an existing In-Place Hold has already reached the 10,000 mailbox limit, and then create a new In-Place Hold if required.</p></td>
</tr>
<tr class="even">
<td><p>Place all public folders on hold</p></td>
<td><p>No</p>
<p>In Exchange Online, placing a Litigation Hold on public folder mailboxes isn't supported. You have to use In-Place Hold.</p></td>
<td><p>Yes</p></td>
</tr>
</tbody>
</table>


## Place all mailboxes on Litigation Hold

You can easily and quickly place all mailboxes on hold indefinitely or for a specified duration using the Shell. This command places all mailboxes on hold for 2555 days (approximately 7 years).

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555

The example uses the [Get-Mailbox](https://technet.microsoft.com/en-us/library/bb123685\(v=exchg.150\)) cmdlet and a recipient filter to retrieve all user mailboxes in the organization, and then pipes the list of mailboxes to the [Set-Mailbox](https://technet.microsoft.com/en-us/library/bb123981\(v=exchg.150\)) cmdlet to enable the Litigation Hold and specify a hold duration. For more information, see [Place a mailbox on Litigation Hold](place-a-mailbox-on-litigation-hold-exchange-2013-help.md).

## Place all mailboxes on In-Place Hold

You can use the EAC to select up to 500 mailboxes and place them on hold. For details, see [Create or remove an In-Place Hold](create-or-remove-an-in-place-hold-exchange-2013-help.md).


> [!TIP]
> To place more than 500 users on In-Place Hold, use the Shell. See <A href="https://technet.microsoft.com/en-us/library/dd298064(v=exchg.150)">New-MailboxSearch</A>.



## More information

  - When you place all mailboxes in your organization on hold, only the mailboxes that exist at the time you run the command are placed on hold. If you create new mailboxes later, run the command again to place them on hold. If you frequently create new mailboxes, you can run the command as a scheduled task as frequently as required.

  - Placing mailboxes on hold preserves data by preventing deletion before the specified period and saving the original version of a message before it’s modified. It doesn’t automatically delete messages after the specified period. Combine Litigation Hold or In-Place Hold with a Retention Policy, which can automatically delete messages after the specified period, to meet your organization’s email retention requirements. See [Retention tags and retention policies](retention-tags-and-retention-policies-exchange-2013-help.md) for details.

  - The PowerShell command used in this topic to place a Litigation Hold on all mailboxes uses a recipient filter that returns all user mailboxes. You can use other recipient properties to return a list of specific mailboxes that you can then pipe to the **Set-Mailbox** cmdlet to place a Litigation Hold on those mailboxes.
    
    Here are some examples of using the **Get-Mailbox** and **Get-Recipient** cmdlets to return a subset of mailboxes based on common user or mailbox properties. These examples assume that relevant mailbox properties (such as *CustomAttributeN* or *Department*) have been populated.
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    
    You can use other user mailbox properties in a filter to include or exclude mailboxes. For details, see [Filterable properties for the -Filter parameter](https://technet.microsoft.com/en-us/library/bb738155\(v=exchg.150\)).

