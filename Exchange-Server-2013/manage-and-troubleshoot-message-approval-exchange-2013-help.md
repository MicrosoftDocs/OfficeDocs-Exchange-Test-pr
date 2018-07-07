---
title: 'Manage and troubleshoot message approval: Exchange 2013 Help'
TOCTitle: Manage and troubleshoot message approval
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 50934218
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Manage and troubleshoot message approval

 

_**Applies to:** Exchange Server 2013_


You may receive the following error when you attempt to remove an arbitration mailbox:


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Can't remove the arbitration mailbox &lt;<em>mailbox</em>&gt; because it's being used for the approval workflow for existing recipients that have either membership restrictions or moderation enabled. You should either disable the approval features on those recipients or specify a different arbitration mailbox for those recipients before removing this arbitration mailbox.</p></td>
</tr>
</tbody>
</table>


An arbitration mailbox can be used to handle the approval workflow for moderated recipients and distribution group membership approvals. You use PowerShell to find all the recipients that are configured to use the arbitration mailbox. After you identify the recipients, you can either configure them to use a different arbitration mailbox, or you can disable moderation for them.

## What do you need to know before you begin?

  - Estimated time to complete: 15 minutes

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Aribtration" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Step 1: Use the Shell to find all the recipients that use the arbitration mailbox you are trying to delete

Run the following commands:

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

For example, to find all the recipients that use the arbitration mailbox named Arbitration Mailbox01, run the following commands:

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}


> [!NOTE]
> The arbitration mailbox is specified using the distinguished name (DN). If you know the DN of the arbitration mailbox, you can run the single command: <CODE>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</CODE>.



## Step 2: Use the Shell to specify a different arbitration mailbox or disable moderation for the recipients

To stop moderated recipients from using the arbitration mailbox you are trying to delete, you can either specify a different arbitration mailbox, or you can disable moderation for the recipients.

If you choose to specify a different arbitration mailbox for the recipients, run the following command:

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

For example, to reconfigure the distribution group named All Employees to use the arbitration mailbox named Arbitration Mailbox02 for membership approval, run the following command:

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

If you choose to disable moderation for the recipients, run the following command:

    Set-<RecipientType> <Identity> -ModerationEanbled $false

For example, to disable moderation for the mailbox named Human Resources, run the following command:

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## How do you know this worked?

The procedure was successful if you can delete the arbitration mailbox without receiving the error that it's being used.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

