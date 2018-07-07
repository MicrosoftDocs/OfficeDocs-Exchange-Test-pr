---
title: 'Safelist Aggregation: Exchange 2013 Help'
TOCTitle: Safelist Aggregation
ms:assetid: f05430a0-0405-4b65-a18d-18c9e86a13c4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb125168(v=EXCHG.150)
ms:contentKeyID: 49248692
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Safelist Aggregation

 

_**Applies to:** Exchange Server 2013_


In Microsoft Exchange Server 2013, *safelist aggregation* refers to anti-spam functionality shared across Microsoft Outlook and Exchange. This functionality collects data from the anti-spam Safe Recipients Lists, Safe Senders Lists, Blocked Senders Lists, and contact data that Outlook users configure, and makes this data available to the Exchange anti-spam agents.

When you enable and correctly configure safelist aggregation, the Content Filter agent passes safe email messages to the enterprise mailbox without additional processing. Email messages that Outlook users receive from contacts that those users have added to their Outlook Safe Recipients List or Safe Senders List or have trusted are identified by the Content Filter agent as safe. An Outlook *contact* is a person, inside or outside the user's organization, about whom the user can save several types of information, such as email and street addresses, telephone and fax numbers, and Web page URLs.

In Exchange 2013, the safelist aggregation process also allows the Sender Filtering agent to block incoming messages from the per-recipient Block Senders List.

Safelist aggregation can help reduce the instances of false-positives in anti-spam filtering performed by Exchange. In the context of spam filtering, a *false-positive* occurs when a spam filter incorrectly identifies a legitimate message as spam.

For organizations that filter hundreds of thousands of messages from the Internet every day, even a small percentage of false-positives means that users might not receive many messages that were incorrectly identified as spam if those messages were quarantined or deleted.

Safelist aggregation is likely the most effective way to reduce false-positives. In Outlook 2010 or newer versions, users can create *Safe Senders Lists*. Safe Senders Lists specify a list of domain names and email addresses from which the Outlook user wants to receive messages. By default, email addresses in Outlook Contacts and in the Exchange global address list are included in this list. By default, Outlook adds all external contacts to which the user sends mail to the Safe Senders List.

**Contents**

Information stored in the Outlook user's safelist collection

How Exchange uses the safelist collection

Hashing of safelist collection entries

Enabling safelist aggregation

## Information stored in the Outlook user's safelist collection

A *safelist collection* is the combined data from the user's Safe Senders List, Safe Recipients List, Blocked Senders List, and external contacts. This data is stored in Outlook and in the Exchange mailbox.

The following types of information are stored in an Outlook user's safelist collection:

  - **Safe senders and safe recipients**   The From message header indicates a sender. The To field of the email message indicates a recipient. Safe senders and safe recipients are represented by full SMTP addresses, such as masato@contoso.com. Outlook users can add senders and recipients to their safe lists.

  - **Blocked senders**   Just like safe senders, users can block unwanted senders by adding them to their Blocked Senders Lists.

  - **Safe domain**   The domain is the part of an SMTP address that follows the @ symbol. For example, contoso.com is the domain in the masato@contoso.com address. Outlook users can add sending domains to their safe lists.
    

    > [!IMPORTANT]
    > By default, Exchange doesn't include the domains during safelist aggregation. However, you can configure safelist aggregation to include the safe domain data for the anti-spam agents. For more information, see <A href="configure-content-filtering-to-use-safe-domain-data-exchange-2013-help.md">Configure Content Filtering to Use Safe Domain Data</A>.



  - **External contacts**   Two types of external contacts can be included in the safelist aggregation. The first type of external contact includes contacts to whom Outlook users have sent mail. This class of contact is added to the Safe Senders List only if an Outlook user selects the corresponding option in the Junk Email settings in Outlook 2007.
    
    The second type of external contact includes the users' Outlook contacts. Users can add or import these contacts into Outlook. This class of contact is added to the Safe Senders List only if an Outlook user selects the corresponding option in the Junk Email Filter settings in Outlook 2010 or Outlook 2007.

Return to top

## How Exchange uses the safelist collection

The safelist collection is stored on the user's Mailbox server. A user can have up to 1,024 unique entries in a safelist collection. Exchange 2013 has a mailbox assistant, called the Junk Email Options mailbox assistant, which monitors changes to the safelist collection for your mailboxes. It then replicates these changes to Active Directory, where the safelist collection is stored on each user object. When the safelist collection is stored on the user object in Active Directory, the safelist collection is aggregated with the anti-spam functionality of Exchange 2013 and is optimized for minimized storage and replication. Exchange uses the safelist collection data during content filtering. If you have a subscribed Edge Transport server in your perimeter network, the Microsoft Exchange EdgeSync service replicates the safelist collection to the Active Directory Lightweight Directory Services (AD LDS) instance on the Edge Transport server.


> [!IMPORTANT]
> Although the safe recipient data is stored in Outlook and can be aggregated into the safelist collection, the content filtering functionality doesn't act on safe recipient data.



Return to top

## Hashing of safelist collection entries

Safelist collection entries are hashed (SHA-256) one way before they are stored as array sets across three user object attributes, **msExchSafeSenderHash**, **msExchSafeRecipientHash**, and **msExchBlockedSendersHash**, as a binary large object. When data is hashed, an output of fixed length is produced, and the output is likely to be unique. For hashing of safelist collection entries, a 4-byte hash is produced. When a message is received from the Internet, Exchange hashes the sender address and compares it to the hashes stored on behalf of the Outlook user to whom the message was sent. If the sender matches the safe senders hash, the message bypasses content filtering. If the sender matches the blocked senders hash, the message is blocked.

One-way hashing of safelist collection entries performs the following important functions:

  - **Minimizes storage and replication space**   Most of the time, hashing reduces the size of the data hashed. Therefore, saving and transmitting a hashed version of a safelist collection entry conserves storage space and replication time. For example, a user who has 200 entries in his or her safelist collection would create about 800 bytes of hashed data stored and replicated in Active Directory.

  - **Renders user safelist collections unusable by malicious users**   Because one-way hash values are impossible to reverse-engineer into the original SMTP address or domain, the safelist collections don't yield usable email addresses for malicious users who might compromise an Exchange server.

Return to top

## Enabling safelist aggregation

Safelist aggregation is enabled by default in Exchange 2013. Unlike in Exchange Server 2007, you don't need to manually run the **Update-SafeList** cmdlet to hash and write the safelist collection data to Active Directory. In Exchange 2013, the safelist collection data is written to Active Directory by the Junk Email Options mailbox assistant.

To make the safelist aggregation data in Active Directory available to Edge Transport servers in the perimeter network, you need to install and configure the Microsoft Exchange EdgeSync service so that the safelist aggregation data is replicated to AD LDS.

You can still manually run safelist aggregation by using the **UpdateSafelist** cmdlet. However, you need to be mindful of the network and replication traffic that may be generated when you run this command. Running **Update-Safelist** on multiple mailboxes where safelists are heavily used may generate a significant amount of traffic. We recommend that if you run the command on multiple mailboxes, you should run the command during off-peak, non-business hours.

The **Update-SafeList** cmdlet reads the safelist collection from the user's mailbox, hashes each entry, sorts the entries for easy search, and then converts the hash to a binary attribute. Finally, the **Update-SafeList** cmdlet compares the binary attribute that was created to any value stored on the attribute. If the two values are identical, the **Update-SafeList** cmdlet doesn't update the user attribute value with the safelist aggregation data. If the two attribute values are different, the **Update-SafeList** cmdlet updates the safelist aggregation value.

Return to top

