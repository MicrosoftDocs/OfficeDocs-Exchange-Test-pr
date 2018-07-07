---
title: 'Accepted domains: Exchange 2013 Help'
TOCTitle: Accepted domains
ms:assetid: c1839a5b-49f9-4c53-b247-f4e5d78efc45
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124423(v=EXCHG.150)
ms:contentKeyID: 49289400
ms.date: 06/17/2016
mtps_version: v=EXCHG.150
---

# Accepted domains

 

_**Applies to:** Exchange Server 2013_


An accepted domain is any SMTP namespace for which a Microsoft Exchange Server 2013 organization sends or receives email. Accepted domains include those domains for which the Exchange organization is authoritative. An Exchange organization is authoritative when it handles mail delivery for recipients in the accepted domain. Accepted domains also include domains for which the Exchange organization receives mail and then relays it to an email server that's outside the organization for delivery to the recipient.

**Contents**

Configuring accepted domains

Authoritative domains

Relay domains

Internal relay domain

External relay domain

Accepted domains and email address policies

## Configuring accepted domains

Accepted domains are configured as global settings for the Exchange organization. You need to configure every domain for which your Exchange organization relays or delivers messages as an accepted domain in your organization.

There are three types of accepted domains: authoritative, internal relay, and external relay. These accepted domain types are described in the following sections.


> [!NOTE]
> If you have a subscribed Edge Transport server in your perimeter network, you configure accepted domains on a Mailbox server in your Exchange organization. The accepted domains configuration is replicated to the Edge Transport server during EdgeSync synchronization. For more information, see <A href="edge-subscriptions-exchange-2013-help.md">Edge Subscriptions</A>.



## Authoritative domains

An organization may have more than one SMTP domain. The set of email domains for an organization are the authoritative domains. In Exchange 2013, an accepted domain is considered authoritative when the Exchange organization hosts mailboxes for recipients in this SMTP domain.

By default, when the first Exchange 2013 Mailbox server is installed, one accepted domain is configured as authoritative for the Exchange organization. The default accepted domain is the fully qualified domain name (FQDN) for your forest root domain. Frequently, the internal domain name differs from the external domain name. For example, your internal domain name may be contoso.local, although your external domain name is contoso.com. The DNS mail exchanger (MX) record for your organization references contoso.com. Contoso.com is the SMTP namespace that you assign to users when you create an email address policy. You need to create an accepted domain to match your external domain name.

To learn more, see:

  - [Configure an accepted domain within your Exchange organization as authoritative](configure-an-accepted-domain-within-your-exchange-organization-as-authoritative-exchange-2013-help.md)

  - [Configure Exchange to accept mail for multiple authoritative domains](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)

## Relay domains

Typically, most Internet-facing messaging servers are configured to not allow for other domains to be relayed through them. However, there are scenarios where you may want to let partners or subsidiaries relay email through your Exchange servers. In Exchange 2013, you can configure accepted domains as relay domains. Your organization receives the email messages and then relays the messages to another email server.

You can configure a relay domain as an internal relay domain or as an external relay domain. These two relay domain types are described in the following sections.

## Internal relay domain

When you configure an internal relay domain, some or all of the recipients in this domain don't have mailboxes in this Exchange organization. Mail from the Internet is relayed for this domain through Transport servers in this Exchange organization. This configuration is used in the scenarios that are described in this section.

An organization may have to share the same SMTP address space between two or more different messaging systems. For example, you may have to share the SMTP address space between Exchange and a third-party messaging system, or between Exchange environments that are configured in different Active Directory forests. In these scenarios, users in each email system have the same domain suffix as part of their email addresses.

To support these scenarios, you need to create an accepted domain that's configured as an internal relay domain. You also need to add a Send connector that's sourced on a Mailbox server and configured to send email to the shared address space. If an accepted domain is configured as authoritative and a recipient isn't found in Active Directory, a non-delivery report (NDR) is returned to the sender. The accepted domain that's configured as an internal relay domain first tries to deliver to a recipient in the Exchange organization. If the recipient isn't found, the message is routed to the Send connector that has the closest address space match.

If an organization contains more than one forest and has configured global address list (GAL) synchronization, the SMTP domain for one forest may be configured as an internal relay domain in a second forest. Messages from the Internet that are addressed to recipients in internal relay domains are relayed to the Mailbox servers in the same organization. The receiving Mailbox servers then route the messages to the Mailbox servers in the recipient forest. You configure the SMTP domain as an internal relay domain to make sure that email that's addressed to that domain is accepted by the Exchange organization. The connector configuration of your organization determines how messages are routed.

To learn more, see [Configure an accepted domain for a business unit with mailboxes outside your Exchange organization](configure-an-accepted-domain-for-a-business-unit-with-mailboxes-outside-your-exchange-organization-exchange-2013-help.md).

## External relay domain

When you configure an external relay domain, messages are relayed to an email server that's outside your Exchange organization and outside the organization's network perimeter.

For more information, see [Configure an accepted domain for an independent business unit](configure-an-accepted-domain-for-an-independent-business-unit-exchange-2013-help.md).

## Accepted domains and email address policies

You need to configure an accepted domain before that SMTP address space can be used in an email address policy. When you create an accepted domain, you can use a wildcard character (\*) in the address space to indicate that all subdomains of the SMTP address space are also accepted by the Exchange organization. For example, to configure contoso.com and all its subdomains as accepted domains, enter **\*.contoso.com** as the SMTP address space. The accepted domain entries are automatically available for use in an email address policy.

If you delete an accepted domain that's used in an email address policy, the policy is no longer valid, and recipients with email addresses in that SMTP domain will be unable to send or receive email.

