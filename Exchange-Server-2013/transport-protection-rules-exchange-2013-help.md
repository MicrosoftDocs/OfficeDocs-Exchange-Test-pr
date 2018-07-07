---
title: 'Transport protection rules: Exchange 2013 Help'
TOCTitle: Transport protection rules
ms:assetid: 9bd6d049-165e-4e51-a79f-3b8ff409da55
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd298166(v=EXCHG.150)
ms:contentKeyID: 49319926
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Transport protection rules

 

_**Applies to:** Exchange Server 2013_


Email messages and attachments increasingly contain business critical information such as product specifications, business strategy documents, and financial data, or personally identifiable information (PII) such as contact details, social security numbers, credit card numbers, and employee records. There are a number of industry-specific and local regulations in many parts of the world that govern the collection, storage, and disclosure of PII.

To help protect sensitive information, organizations create messaging policies that provide guidelines about how to handle this information. In Microsoft Exchange Server 2013, you can use transport protection rules to implement these messaging policies by inspecting message content, encrypting sensitive email content, and using rights management to control access to the content.

For management tasks related to managing IRM, see [Information Rights Management procedures](information-rights-management-procedures-exchange-2013-help.md).

## Transport protection rules and AD RMS

Transport protection rules allow you to use transport rules to IRM-protect messages by applying an [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823) (AD RMS) rights policy template.


> [!NOTE]
> AD&nbsp;RMS is an information protection technology that works with Rights Management Service (RMS)-enabled applications and clients to protect sensitive information online and offline. To use IRM protection in an on-premise Exchange deployment, Exchange 2013 requires an on-premises deployment of AD&nbsp;RMS running on Windows Server 2008 or later.



AD RMS uses XML-based policy templates to allow compatible IRM-enabled applications to apply consistent protection policies. In Windows Server 2008 and later, the AD RMS server exposes a Web service that can be used to enumerate and acquire templates. Exchange 2013 ships with the Do Not Forward template.

When the Do Not Forward template is applied to a message, only the recipients addressed in the message can decrypt the message. The recipients can't forward the message to anyone else, copy content from the message, or print the message.

Additional RMS templates can be created in the on-premises AD RMS deployment to meet rights protection requirements in your organization.


> [!IMPORTANT]
> If a rights policy template is removed from the AD&nbsp;RMS server, you must modify any transport protection rules that use the removed template. If a transport protection rule continues to use a rights policy template that's been removed, the AD&nbsp;RMS server will fail to license the content to any of the recipients, and a non-delivery report (NDR) will be delivered to the sender.<BR>In Windows Server 2008 and later, rights policy templates can be archived instead of deleted. Archived templates can still be used to license content, but when you create or modify a transport protection rule, archived templates aren't included in the list of templates.



For more information about creating AD RMS templates, see [AD RMS Rights Policy Templates Deployment Step-by-Step Guide](https://go.microsoft.com/fwlink/p/?linkid=136593).

## Automatic protection using transport protection rules

Messages containing business critical information or PII can be identified by using a combination of transport rule conditions, including regular expressions to identify text patterns such as social security numbers. Organizations require different levels of protection for sensitive information. Some information may be restricted to employees, contractors, or partners; while other information may be restricted only to full-time employees. The desired level of protection can be applied to messages by applying an appropriate rights policy template. For example, users may mark messages or email attachments as Company Confidential. As illustrated in the following figure, you can create a transport protection rule to inspect message content for the words "Company Confidential", and automatically IRM-protect the message.

For more information about creating transport rules to enforce rights protection, see [Create a Transport Protection Rule](create-a-transport-protection-rule-exchange-2013-help.md).

## Persistent protection of email attachments

Users send business critical information and PII in email attachments using common Microsoft Office file formats such as Microsoft Office Word, Excel, and PowerPoint. All of these file formats support persistent protection via IRM, and you can make sure that the business critical information and PII in these documents are properly protected. Transport protection rules apply the same protection to email messages and attachments in supported file formats.

## Transport rules agent and encryption agent

When you use transport protection rules to IRM-protect messages based on rule conditions, the Transport Rules agent on the Transport service inspects messages. If they meet all the conditions and none of the exceptions, it flags the message to be IRM-protected. The Encryption agent, a built-in transport agent that fires on the **OnRoutedMessage** event, actually applies IRM protection to the message. The Encryption agent acts on messages only if IRM is enabled for internal messages. For more information about enabling IRM, see [Enable or Disable IRM for Internal Messages](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

When the transport service is restarted, and it processes the first message that requires IRM encryption, the Encryption agent must be able to reach an AD RMS server in the organization. For subsequent messages, the agent doesn't need to contact the AD RMS server. Upon failure to encrypt a message due to transient conditions, Exchange retries the message three times at 10-minute intervals. After three retries, if the message can't be encrypted, it isn't delivered to recipients. An NDR is sent to the sender. We recommend that you plan your AD RMS deployment for high availability to make sure message flow isn't impacted.

When planning to use transport protection rules, you must consider the type of information you want to protect and plan on creating rules accordingly. In Exchange 2013, transport rules have a large number of predicates that allow you to inspect message content, including supported attachments, message headers, sender and recipient addresses, their Active Directory attributes such as department, distribution group membership, and management relationships of the sender with recipients. For more details about transport rule predicates available in Exchange 2013, see [Transport rule conditions (predicates)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

You must also consider the messaging traffic in your organization, and the number of messages that will be protected using transport protection rules. Applying IRM protection to a large number of messages requires more resources on the Mailbox server. Additionally, protecting a large number of messages or all messages also impacts the client experience, particularly for Microsoft Outlook users.

