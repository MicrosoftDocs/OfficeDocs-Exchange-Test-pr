---
title: 'Message size limits: Exchange 2013 Help'
TOCTitle: Message size limits
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 49284660
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Message size limits

 

_**Applies to:** Exchange Server 2013_


You can apply limits to messages that move through the Microsoft Exchange Server 2013 organization. You can restrict the total size of a message or the size of the individual components of a message, such as the message header, the message attachments, and the number of recipients. You can apply limits globally for the whole Exchange organization, or specifically to a connector or user object.

As you plan the message size limits for your Exchange organization, consider the following questions:

  - What size limits should I impose on all incoming messages?

  - What size limits should I impose on all outgoing messages?

  - What is the mailbox quota for my Exchange organization?

  - How do the message size limits that I have chosen relate to the mailbox quota size?

  - Are there users in my Exchange organization who must send or receive messages that are larger than the specified allowed size?

  - Does my Exchange network topology include other messaging systems or distinctly separate business units that have different message size limits?

This topic provides guidance to help you answer these questions.

**Contents**

Types of message size limits

Scope of limits

Order of precedence for message size limits

Messages exempt from size limits

## Types of message size limits

Following are the basic categories of the size limits available for individual messages:

  - **Message header size limits**   These limits apply to the total size of all message header fields that are present in a message. The size of the message body or attachments isn’t considered. Because the header fields are plain text, the size of the header is determined by the number of characters in each header field and by the total number of header fields. Each character of text consumes 1 byte.
    

    > [!NOTE]
    > Some third-party firewalls or proxy servers apply their own message header size limits. These third-party firewalls or proxy servers may have difficulty processing messages that contain attachment file names that are greater than 50&nbsp;characters or attachment file names that contain non-US-ASCII characters.



  - **Message size limits**   These limits apply to the total size of a message, which includes the message header, the message body, and any attachments. Message size limits may be imposed on incoming messages or outgoing messages. For internal message flow, Exchange uses the custom `X-MS-Exchange-Organization-OriginalSize:` message header to record the original message size of the message as it enters the Exchange organization. Whenever the message is checked against the specified message size limits, the lower value of the current message size or the original message size header is used. The size of the message can change because of content conversion, encoding, and agent processing.

  - **Attachment size limits**   These limits apply to the maximum allowed size of a single attachment within a message. The message may contain many attachments that greatly increase the overall size of the message. However, an attachment size limit applies to the size of an individual attachment only.

  - **Recipient limits**   These limits apply to the total number of message recipients. When a message is first composed, the recipients exist in the `To:`, `Cc:`, and `Bcc:` header fields. When the message is submitted for delivery, the message recipients are converted into `RCPT TO:` entries in the message envelope. A distribution group is counted as a single recipient during message submission.

Return to top

## Scope of limits

Following are the basic categories for the scope of the limits available for individual messages:

  - **Organizational limits**   These limits apply to all Exchange 2013 Mailbox servers and Exchange 2010 and Exchange 2007 Hub Transport servers that exist in the organization. If you have an Edge Transport server installed in the perimeter network, the specified limits apply to the specific server.

  - **Connector limits**   These limits apply to any messages that use the specified Send connector, Receive connector, Delivery Agent connector, or Foreign connector for message delivery. Send connectors are defined in the Transport service on Mailbox servers and on Edge Transport servers. Receive connectors are defined in the Transport service on Mailbox servers, in the Front End Transport service on Client Access servers, and on Edge Transport servers.

  - **Active Directory site links**   The Transport service on Mailbox servers use Active Directory sites and the costs that are assigned to the Active Directory IP site links as one of the factors to determine the least-cost routing path between Mailbox servers in the organization. You can assign specific message size limits to the Active Directory site links in your organization.

  - **Server limits**   These limits apply to a specific Mailbox server or Edge Transport server. You can set the specified message limits independently on each Mailbox server or Edge Transport server.
    
    In Outlook Web App, the maximum HTTP request size limit setting on the Client Access servers also controls the size of messages that Outlook Web App users can send.

  - **User limits**   These limits apply to a specific user object, such as a mailbox, contact, distribution group, or public folder.

The following tables show the message limits, including information about how to configure the limits in the Exchange Management Shell or the Exchange Administrator Center (EAC).

### Organizational limits

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Size limit</th>
<th>Default value</th>
<th>Shell configuration</th>
<th>EAC configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Maximum size for messages received</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parameter: <em>MaxReceiveSize</em></p></td>
<td><p><strong>Mail flow</strong> &gt; <strong>Receive connectors</strong> &gt; <strong>More options</strong> <img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="More Options Icon" alt="More Options Icon" /> &gt; <strong>Organization transport settings</strong> &gt; <strong>Limits</strong> tab &gt; <strong>Maximum receive message size</strong></p></td>
</tr>
<tr class="even">
<td><p>Maximum size for messages sent</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parameter: <em>MaxSendSize</em></p></td>
<td><p><strong>Mail flow</strong> &gt; <strong>Receive connectors</strong> &gt; <strong>More options</strong> <img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="More Options Icon" alt="More Options Icon" /> &gt; <strong>Organization transport settings</strong> &gt; <strong>Limits</strong> tab &gt; <strong>Maximum send message size</strong></p></td>
</tr>
<tr class="odd">
<td><p>Maximum number of recipients per message</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ126650.note(EXCHG.150).gif" title="Note" alt="Note" />Note:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
</tr>
</tbody>
</table>

</td>
<td><p>5000</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parameter: <em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p><strong>Mail flow</strong> &gt; <strong>Receive connectors</strong> &gt; <strong>More options</strong> <img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="More Options Icon" alt="More Options Icon" /> &gt; <strong>Organization transport settings</strong> &gt; <strong>Limits</strong> tab &gt; <strong>Maximum number of recipients</strong></p></td>
</tr>
<tr class="even">
<td><p>Maximum attachment size in Transport rules that apply to all Mailbox servers in the organization</p></td>
<td><p>Not configured</p></td>
<td><p>Cmdlets: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Parameter: <em>AttachmentSizeOver</em></p></td>
<td><p><strong>Mail flow</strong> &gt; <strong>Rules</strong> &gt; <strong>Add</strong> <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Add Icon" alt="Add Icon" /> or <strong>Edit</strong> <img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Edit icon" alt="Edit icon" />.</p>
<p>Use the predicate <strong>Apply this rule if</strong> &gt; <strong>Any attachment</strong> &gt; <strong>is greater than or equal to</strong></p>
<p>Use the predicate <strong>Apply this rule if</strong> &gt; <strong>The message</strong> &gt; <strong>size is greater than or equal to</strong></p></td>
</tr>
<tr class="odd">
<td><p>Maximum message size in Transport rules that apply to all Mailbox servers in the organization</p></td>
<td><p></p></td>
<td><p>Cmdlets: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Parameter: <em>MessageSizeOver</em></p></td>
<td><p><strong>Mail flow</strong> &gt; <strong>Rules</strong> &gt; <strong>Add</strong> <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Add Icon" alt="Add Icon" /> or <strong>Edit</strong> <img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Edit icon" alt="Edit icon" />.</p>
<p>Use the predicate <strong>Apply this rule if</strong> &gt; <strong>The message</strong> &gt; <strong>size is greater than or equal to</strong></p></td>
</tr>
</tbody>
</table>


Return to top

### Connector limits

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Size limit</th>
<th>Default value</th>
<th>Shell configuration</th>
<th>EAC configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Maximum header size through a Receive connector</p></td>
<td><p>128 KB</p></td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parameter: <em>MaxHeaderSize</em></p></td>
<td><p>N/A</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Maximum message size through a Receive connector</p>

> [!NOTE]
> The actual message size may be smaller due to message encoding and content conversion.


</td>
<td><p><strong>Transport service on Mailbox servers</strong></p>
<p>35 MB for the Default and Client Proxy Receive connectors</p>
<p><strong>Front End Transport service on Client Access servers</strong></p>
<p>36 MB for the Default Frontend and Outbound Proxy Frontend Receive connectors.</p>
<p>35 MB for the Client Frontend Receive connector.</p></td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parameter: <em>MaxMessageSize</em></p></td>
<td><p><strong>Mail flow</strong> &gt; <strong>Receive connectors</strong> &gt; <strong>Edit</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Edit icon" alt="Edit icon" /> &gt; <strong>General</strong> tab &gt; <strong>Maximum receive message size</strong></p></td>
</tr>
<tr class="odd">
<td><p>Maximum number of recipients per message through a Receive connector</p></td>
<td><p><strong>Transport service on Mailbox servers</strong></p>
<p>5,000 for the Default Receive connector</p>
<p>200 for the Client Proxy Receive connector</p>
<p><strong>Front End Transport service on Client Access servers</strong></p>
<p>200 for the Default Frontend, Client Frontend, and Client Proxy Frontend Receive connectors.</p>

> [!NOTE]
> If the number of recipients is exceeded for an anonymous sender, the message is accepted for the first 200&nbsp;recipients. Most SMTP messaging servers detect that a recipient limit is in effect. The SMTP messaging server continues to resend the message in groups of 200&nbsp;recipients until the message is delivered to all recipients.


</td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parameter: <em>MaxRecipientsPerMessage</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>Maximum message size through a Send connector</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlets: <strong>New-SendConnector</strong>, <strong>Set-SendConnector</strong></p>
<p>Parameter: <em>MaxMessageSize</em></p></td>
<td><p><strong>Mail flow</strong> &gt; <strong>Send connectors</strong> &gt; <strong>Edit</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Edit icon" alt="Edit icon" /> &gt; <strong>General</strong> tab &gt; <strong>Maximum send message size</strong></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Maximum message size through an Active Directory site link</p></td>
<td><p>Unlimited</p></td>
<td><p>Cmdlet: <strong>Set-AdSiteLink</strong></p>
<p>Parameter: <em>MaxMessageSize</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>Maximum message size through a delivery agent connector</p></td>
<td><p>Unlimited</p></td>
<td><p>Cmdlets: <strong>New-DeliveryAgentConnector</strong>, <strong>Set-DeliveryAgentConnector</strong></p>
<p>Parameter: <em>MaxMessageSize</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Maximum message size through a foreign connector</p></td>
<td><p>Unlimited</p></td>
<td><p><strong>Cmdlet: Set-ForeignConnector</strong> Parameter: <em>MaxMessageSize</em></p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


Return to top

### Server limits

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Size limit</th>
<th>Default value</th>
<th>Shell configuration</th>
<th>EAC configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Maximum header size for messages in the pickup directory</p></td>
<td><p>64 KB</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>Parameter: <em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>Maximum number of recipients per message for messages in the pickup directory</p></td>
<td><p>100</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>Parameter: <em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Client-specific maximum messages size limits for Outlook Web App, Exchange ActiveSync, and Exchange Web Services clients</p></td>
<td><p>Outlook Web App   35 MB</p>
<p>Exchange ActiveSync   10 MB</p>
<p>Exchange Web Services   64 MB</p>

> [!NOTE]
> These values are approximately 33% larger than the actual usable maximum message size because of the overhead that's associated with Base64 encoding.


</td>
<td><p>You configure these values in the appropriate web.config XML application configuration file on Client Access servers. For more information, see <a href="configure-client-specific-message-size-limits-exchange-2013-help.md">Configure client-specific message size limits</a>.</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


Return to top

### User limits

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Size Limit</th>
<th>Default value</th>
<th>Shell configuration</th>
<th>EAC configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Maximum message size that can be sent by this recipient</p></td>
<td><p>Unlimited</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>Parameter: <em>MaxSendSize</em></p></td>
<td><p>For mailboxes:</p>
<p><strong>Recipients</strong> &gt; <strong>Mailboxes</strong> &gt; <strong>Edit</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Edit icon" alt="Edit icon" /> &gt; <strong>Mailbox features</strong> &gt; <strong>Mail flow</strong> &gt; <strong>Message size restrictions</strong> &gt; <strong>View details</strong> &gt; <strong>Sent messages</strong></p>

> [!NOTE]
> This setting isn't configurable using the EAC for other recipient types.


</td>
</tr>
<tr class="even">
<td><p>Maximum message size that can be sent to this recipient</p></td>
<td><p>Unlimited</p>
<p>For site mailbox provisioning policies: 36 MB</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>Parameter: <em>MaxReceiveSize</em></p></td>
<td><p>For mailboxes:</p>
<p><strong>Recipients</strong> &gt; <strong>Mailboxes</strong> &gt; <strong>Edit</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Edit icon" alt="Edit icon" /> &gt; <strong>Mailbox features</strong> &gt; <strong>Mail flow</strong> &gt; <strong>Message size restrictions</strong> &gt; <strong>View details</strong> &gt; <strong>Received messages</strong></p>

> [!NOTE]
> This setting isn't configurable using the EAC for other recipient types.


</td>
</tr>
<tr class="odd">
<td><p>Maximum number of recipients per message sent by this recipient</p></td>
<td><p>Unlimited</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>Parameter: <em>RecipientLimits</em></p>
<p></p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


Return to top

## Order of precedence for message size limits

You can set different message size limits at different levels in the Exchange organization. As a message is routed through your Transport infrastructure, it may be subjected to several different message size restrictions. You should plan your message size restrictions in a way that makes sure that messages in the transport pipeline are rejected as early as possible if they violate message size limits. Generally speaking, you should set more restrictive limits at the points where messages enter your infrastructure. For example, any message size restrictions on your Receive connectors that receive messages from the Internet should be less than or equal to the message size restrictions you configure for your internal Exchange organization. It would be a waste of system resources for the Exchange server to accept and process a message from the Internet that would be rejected by the Transport service on your Mailbox servers. Make sure that your organization, server, and connector limits are configured in a way that minimizes any unnecessary processing of messages.

One exception to this approach is the user limits. User level limits take precedence over other message size restrictions. Therefore, you can configure a user to exceed the default message size limits for your organization. For example, you can allow a specific group of user mailboxes to send larger messages than the rest of the organization by configuring custom send and receive limits for those mailboxes.

The exceptions for the user limits only apply to message exchanges between authenticated users. If a message is sent to or received by a recipient on the Internet, the organizational limits will be applied. For example, assume that you have an organizational message size restriction of 10 MB, but you have configured the users in your marketing department to send and receive messages up to 50 MB. These users will be able to exchange large messages with each other, but they still won’t be able to receive large messages from Internet users because such messages will be coming from unauthenticated senders.

Return to top

## Messages exempt from size limits

The following list shows the types of messages generated by a Mailbox server or an Edge Transport server and exempted from all message size limits:

  - System messages

  - Agent-generated message

  - Delivery status notification (DSN) messages

  - Journal report messages

  - Quarantined messages

However, these messages are still subject to the organizational value for maximum number of recipients in a message.

Return to top

