---
title: 'Configure a spam quarantine mailbox: Exchange 2013 Help'
TOCTitle: Configure a spam quarantine mailbox
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 49300568
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Configure a spam quarantine mailbox

 

_**Applies to:** Exchange Server 2013_


Messages determined to be spam by the Content Filter agent can be directed to a spam quarantine mailbox. If the spam confidence level (SCL) quarantine threshold is enabled, all messages that are quarantined are wrapped as non-delivery reports (NDR) and are sent to the SMTP address that you specify as the spam quarantine mailbox. You can review quarantined messages and release them to their intended recipients by using the Send Again feature in Microsoft Outlook.

## What do you need to know before you begin?

  - Estimated time to complete this task: 45 minutes.

  - By default, anti-spam features aren't enabled in the Transport service on a Mailbox server. Typically, you only enable the anti-spam features on a Mailbox server if your Exchange organization doesn't do any prior anti-spam filtering before accepting incoming messages. For more information, see [Enable anti-spam functionality on Mailbox servers](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - The person responsible for the spam quarantine mailbox can view potentially private and sensitive messages, and then send mail on behalf of anybody in the Exchange organization.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## How do you do this?

## Step 1: Verify content filtering is enabled

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Anti-spam features" entry in the [Anti-spam and anti-malware permissions](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) topic.

1.  Run the following command to verify the Content Filter agent is installed and enabled on the Exchange server:
    
        Get-TransportAgent "Content Filter Agent"

2.  Run the following command to verify content filtering is enabled:
    
        Get-ContentFilterConfig | Format-List Enabled

For more information, see [Manage content filtering](manage-content-filtering-exchange-2013-help.md).

## Step 2: Create a dedicated mailbox for spam quarantine

To create a dedicated spam quarantine mailbox, follow these steps:

  - **Create a dedicated Exchange database**   We recommend that you create a dedicated database for the spam quarantine mailbox. The spam quarantine mailbox should have a large database, because if the storage quota limit is reached, messages will be lost. For more information, see [Manage mailbox databases in Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

  - **Create a dedicated mailbox and user account**   We recommend that you create a dedicated mailbox and Active Directory user account for the spam quarantine mailbox. For more information, see [Create user mailboxes](create-user-mailboxes-exchange-2013-help.md).
    
    You may apply recipient policies, such as messaging records management, mailbox quotas, and delegation rights, according to your organization's compliance policies and needs. For more information, see [Messaging records management](messaging-records-management-exchange-2013-help.md).
    

    > [!NOTE]
    > If a quarantined message is rejected because of a storage quota, the message will be lost. Exchange doesn't generate NDRs for quarantined messages because the quarantined messages are wrapped as NDRs.



  - **Configure Outlook**   You need to configure the Outlook delegate access permissions to meet the needs of your organization. In addition, we recommend that you configure the Outlook profile to show the original `Sender[#0x0069001E]`, `Recipient[#0x0E04001E]`, and `Bcc[#0x0E02001E]` fields in the **Message** view. For more information, see [Release quarantined messages from the spam quarantine mailbox](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

## Step 3: Specify the spam quarantine mailbox

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Anti-spam features" entry in the [Anti-spam and anti-malware permissions](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) topic.

Run the following command:

    Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>

This example sends all messages that exceed the spam quarantine threshold to spamQ@contoso.com.

    Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com

## How do you know this step worked?

To verify that you have successfully specified the spam quarantine mailbox, do the following:

1.  Run the following command:
    
        Get-ContentFilterConfig | Format-List QuarantineMailbox

2.  Verify the value displayed is the value you configured.

## Step 4: Configure the SCL quarantine threshold

The SCL quarantine threshold is the value at which a particular message identified as potential spam is delivered to the spam quarantine mailbox. You can set the SCL quarantine threshold to a value from 0 through 9, where 0 is considered less likely to be spam, and 9 is considered most likely to be spam.

For more information about how to adjust SCL thresholds to suit your organization's requirements and how to adjust per-recipient SCL thresholds, see [Manage content filtering](manage-content-filtering-exchange-2013-help.md).

## Step 5: Manage the spam quarantine mailbox

When you manage your spam quarantine mailbox, follow these guidelines:

  - Release items that have been sent to the spam quarantine mailbox by using the Send Again feature in Outlook to resend the original message.
    
    For more information, see [Release quarantined messages from the spam quarantine mailbox](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

  - Monitor the spam quarantine mailbox so that the size of the spam quarantine mailbox remains in an acceptable range. The volume of email messages can change because of a larger set of recipients, the natural trend of larger messages, or the threshold on the SCL quarantine action.

  - Monitor the spam quarantine mailbox for false positives. If your spam quarantine mailbox includes many false positives, adjust your SCL quarantine threshold. For more information about how to determine why false positives are being delivered to the spam quarantine mailbox, see [Anti-spam stamps](anti-spam-stamps-exchange-2013-help.md).

  - Use the same Outlook profile to recover quarantined messages from the spam quarantine mailbox. Applying permissions to a different Outlook profile to recover messages isn't supported. You can't use a different Outlook profile to recover or release messages from the spam quarantine mailbox.


> [!IMPORTANT]
> NDRs identified as spam are deleted, even if their SCL rating indicates that they should be quarantined. NDRs aren't delivered to the spam quarantine mailbox. To track such messages, use the agent log or the message tracking log. For more information, see <A href="anti-spam-agent-logging-exchange-2013-help.md">Anti-spam agent logging</A>.



## Step 6: Adjust the SCL quarantine threshold

After you configure the SCL quarantine threshold, periodically monitor the settings and adjust them based on your organization's needs. For example, if too many false positives are filtered into the spam quarantine mailbox, raise the SCL quarantine threshold to a larger number. For more information about how to adjust the SCL quarantine threshold, see [Spam Confidence Level Threshold](spam-confidence-level-threshold-exchange-2013-help.md).

