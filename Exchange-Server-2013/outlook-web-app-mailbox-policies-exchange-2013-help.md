---
title: 'Outlook Web App mailbox policies: Exchange 2013 Help'
TOCTitle: Outlook Web App mailbox policies
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 49319904
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Outlook Web App mailbox policies

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Use Microsoft Outlook Web App mailbox policies to create organization-level policies to manage access to features in Outlook Web App.

**Contents**

Outlook Web App mailbox policies

Creating or deleting Outlook Web App mailbox policies

Configuring Outlook Web App mailbox policies

Applying Outlook Web App mailbox policies

## Outlook Web App mailbox policies

In Exchange 2013, you can create multiple Outlook Web App mailbox policies and apply them to individual mailboxes. When an Outlook Web App mailbox policy is applied to a mailbox, it will override the settings of the virtual directory.

Outlook Web App features can also be managed by configuring the Outlook Web App virtual directories. Virtual directory settings will be used for any mailbox that a mailbox policy hasn’t been applied to.

## Creating or deleting Outlook Web App mailbox policies

A default Outlook Web App mailbox policy is created automatically when Exchange is installed. By default, all options are enabled on the default Outlook Web App mailbox policy. You can create as many Outlook Web App mailbox policies as necessary to meet the needs of your organization.


> [!NOTE]
> The default Outlook Web App mailbox policy isn’t automatically applied to any mailboxes.



For information about creating or removing mailbox policies, see [Create an Outlook Web App mailbox policy](create-an-outlook-web-app-mailbox-policy-exchange-2013-help.md) and [Remove an Outlook Web App mailbox policy from Exchange](remove-an-outlook-web-app-mailbox-policy-from-exchange-exchange-2013-help.md).

## Configuring Outlook Web App mailbox policies

The default Outlook Web App mailbox policy has all options enabled by default. For information about configuring Outlook Web App mailbox policies, see [View or configure Outlook Web App mailbox policy properties](view-or-configure-outlook-web-app-mailbox-policy-properties-exchange-2013-help.md).

## Applying Outlook Web App mailbox policies

Only one Outlook Web App mailbox policy can be applied to a mailbox.

If there's no Outlook Web App mailbox policy applied to a mailbox, the settings defined on the virtual directory will be applied.

An Outlook Web App mailbox policy can be applied to a mailbox by using the Exchange Administration Center (EAC) to modify an existing mailbox, or by using the Shell and the [Set-CASMailbox](https://technet.microsoft.com/en-us/library/bb125264\(v=exchg.150\)) cmdlet to apply a mailbox policy. For more information, see [Apply or remove an Outlook Web App mailbox policy on a mailbox](apply-or-remove-an-outlook-web-app-mailbox-policy-on-a-mailbox-exchange-2013-help.md).

