---
title: 'Configure Content Filtering to Use Safe Domain Data: Exchange 2013 Help'
TOCTitle: Configure Content Filtering to Use Safe Domain Data
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 58899940
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Configure Content Filtering to Use Safe Domain Data

 

_**Applies to:** Exchange Server 2013_


Safe domain data is an entire domain (for example, @contoso.com) that's stored in a user's Safe Senders List. By default, the Content Filter agent doesn't use safe domain data to identify senders that are allowed to bypass content filtering.

This default setting helps reduce the amount of spam that's delivered into your organization. For example, a user might add the domain of a large email provider to their Safe Senders List. If this domain is frequently used or spoofed by spammers, and if content filtering is configured to use safe domain data to mark the messages as safe, messages from any sender in that domain would be delivered to recipients in your organization.

We recommend that you don't modify the default setting in most cases. However, you can configure users' safe domain data to be stored in Active Directory and used by content filtering to mark messages as safe. To do this, you need to modify the MSExchangeMailboxAssistants.exe.config XML application configuration file that's associated with the Microsoft Exchange Mailbox Assistants service, as detailed later in this topic. When you make this configuration change, the safe domain data is hashed and stored in each user's **msExchSafeSenderHash** user object attribute in Active Directory as part of safelist aggregation. The Content Filter agent can then use the safe domain data to mark messages from senders in those domains as safe. For more information about safelist aggregation, see [Safelist Aggregation](safelist-aggregation-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 10 minutes

  - Exchange permissions don't apply to the procedures in this topic. These procedures are performed in the operating system of the Exchange Server.

  - Changes you save to the MSExchangeMailboxAssistants.exe.config file are applied after you restart the Microsoft Exchange Mailbox Assistants service.

  - Any customized per-server settings you make in Exchange XML application configuration files, for example, web.config files on Client Access servers or the EdgeTransport.exe.config file on Mailbox servers, will be overwritten when you install an Exchange Cumulative Update (CU). Make sure that you save this information so you can easily re-configure your server after the install. You must re-configure these settings after you install an Exchange CU.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use a command prompt to configure content filtering to use safe domain data

1.  In the Command Prompt window, open the MSExchangeMailboxAssistants.exe.config file in Notepad by running the following command:
    
        Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config

2.  Locate the *\</appsettings\>* key at the end of the file, and paste the following key before the *\</appsettings\>* key:
    
        <add key="IncludeSafeDomains" value="true" />

3.  When you are finished, save and close the MSExchangeMailboxAssistants.exe.config file.

4.  Restart the Microsoft Exchange Mailbox Assistants service by running the following command:
    
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants

## How do you know this worked?

To verify that you have successfully configured content filtering to use safe domain data, do the following:

1.  Verify that adding a domain to a user's Safe Senders List in Outlook updates the user's **msExchSafeSenderHash** attribute in Active Directory. To do this, view the attribute in ADSIEdit.exe or LDP.exe, open the user's mailbox in Outlook, add a domain to the Safe Senders List, run the command `Update-Safelist <username>`, and verify that the original and current values of **msExchSafeSenderHash** are different.

2.  After you've verified the safe domain data is stored in Active Directory, send a test message from an external sender in that domain to a user in your organization. Verify the message is marked as safe by examining the anti-spam header fields in the message header.

