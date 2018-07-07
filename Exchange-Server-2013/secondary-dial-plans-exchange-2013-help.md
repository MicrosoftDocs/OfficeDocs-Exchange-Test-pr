---
title: 'Secondary dial plans: Exchange 2013 Help'
TOCTitle: Secondary dial plans
ms:assetid: ecf474c2-042d-4aaf-9f5b-d5138c56ef39
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff629383(v=EXCHG.150)
ms:contentKeyID: 54817012
ms.date: 07/14/2016
mtps_version: v=EXCHG.150
---

# Secondary dial plans

 

_**Applies to:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_


When you enable a user for Unified Messaging (UM), you're required to assign one extension number and a UM mailbox policy that will link the user to a UM dial plan. After the user is enabled for UM, you can assign additional extension numbers for that user within the same dial plan but the extension numbers within that dial plan must be unique. In some deployments, a user may need to be assigned the same extension number in two separate dial plans. If this is the case, you can link the user to a secondary UM dial plan. This can be useful, for example, if the user has two physical phones or travels between locations.

**Contents**

Overview

Use of secondary extensions

UM features that operate differently for secondary dial plans

## Overview

When you enable a user for Unified Messaging, you must define one extension number and one UM mailbox policy that links the user to a single UM dial plan. When you enable the user for UM and they’re linked to a UM mailbox policy that’s linked to a SIP URI or E.164 dial plan, you must also provide either a SIP address or E.164 number with the user’s extension number. UM uses the dial plan and extension, along with the SIP address or E.164 number, to locate the user when a voice mail message is submitted to the user's mailbox.

If you’re using telephone extension dial plans and need to provide the same extension number for a user, you’ll need to create a secondary dial plan, enable the user for UM and provide the same extension number for the user. This is because the extension number must be unique within a dial plan,


> [!NOTE]
> There's no limit to the number of secondary extension numbers that you can add for a UM-enabled user.



There may be times when a user travels between locations, has two or more phones, or wants to receive voice mail on one Direct Inward Dial (DID) extension number and receive faxes on a different DID extension number. To achieve this, you must add an additional DID extension to the user's mailbox and, in some cases, add a secondary dial plan.

In some configurations, after you add a second extension on a primary dial plan or add a single or multiple extension numbers to a secondary dial plan, the user can receive voice messages or faxes using one or more of the extension numbers. If you want UM to answer these fax calls and send them to the second DID extension number, you must configure the telephony equipment in your organization to forward the fax calls to the second DID extension number.

The mailbox of a UM-enabled user can be assigned the following:

  - A single extension number, Session Initiation Protocol (SIP) address, or E.164 address on a single dial plan

  - Multiple extension numbers on a single dial plan

  - Multiple extension numbers on two separate dial plans

When a user is enabled for UM, you must specify an extension number and a UM mailbox policy. UM requires the extension number to identify the user when they sign in to Outlook Voice Access to retrieve messages. The UM mailbox policy contains a collection of configuration properties, with values that UM applies to any user who is UM-enabled under that policy. The UM mailbox policy is similar to the “class of service” found in other systems (for example, voice mail or PBX), in the sense that a change to a UM mailbox policy value can affect the behavior for a large number of associated users.

One property on a UM mailbox policy refers to a UM dial plan. This represents a set of telephony-capable extensions. This set has a numbering plan in which duplicate extension numbers aren't allowed.

Therefore, a user’s extension number is unique within the UM dial plan in which they're UM-enabled. In fact, the UM dial plan and extension number pair must be unique within the organization. This is one way that UM uniquely identifies a UM-enabled user in an organization. Using a secondary dial plan makes it easier to keep the dial plan and extension number unique within an organization. For example, imagine an organization has two UM dial plans: Dial Plan A and Dial Plan B. A user's extension number in Dial Plan A is 55555 and, in Dial Plan B, it's 66666. When a secondary dial plan is used, the user's extension for Dial Plan A can be 55555 and their extension in Dial Plan B can also be 55555. In both cases, the user's extension within the dial plan that's used is unique.

The following table defines terms that are used when discussing primary and secondary extensions, Outlook Voice Access numbers, and UM dial plans.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Term</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>primary extension</p></td>
<td><p>The extension number that's specified when the user is UM enabled.</p></td>
</tr>
<tr class="even">
<td><p>primary dial plan</p></td>
<td><p>The UM dial plan that's specified when the user is UM enabled. The UM-enabled user is associated with the dial plan when the user is linked to the UM mailbox policy.</p></td>
</tr>
<tr class="odd">
<td><p>primary Outlook Voice Access number</p></td>
<td><p>The Outlook Voice Access number for the user’s primary dial plan. The user's calls are forwarded to this number if there's no answer or their line is busy. It's also the number that the user calls when they want to sign in to Outlook Voice Access.</p></td>
</tr>
<tr class="even">
<td><p>secondary extension</p></td>
<td><p>One or more extension numbers that may be added to a UM-enabled user’s configuration.</p></td>
</tr>
<tr class="odd">
<td><p>secondary dial plan</p></td>
<td><p>A UM dial plan other than the primary dial plan in which one or more secondary extensions can be configured.</p></td>
</tr>
<tr class="even">
<td><p>secondary Outlook Voice Access number</p></td>
<td><p>The Outlook Voice Access number of a user’s secondary dial plan. A user can call this number from their secondary extension number when they want to sign in to Outlook Voice Access.</p></td>
</tr>
</tbody>
</table>


Return to top

## Use of secondary extensions

In most deployments, only one extension is configured per UM-enabled user. However, there are some more advanced deployments that require you to add secondary extensions for your users.

When Microsoft Lync Server is used for Enterprise Voice, Unified Messaging can provide the voice mail system. However, the UM dial plan used for Enterprise Voice must be a SIP URI dial plan that's specific to UM configurations with Lync Server. In these deployments, the user’s extension is provided by a Microsoft Unified Communications endpoint, such as Microsoft Office Communicator, running on the user’s computer, or Office Communicator Phone Edition, running on a supported IP phone device. Thus, in most cases, the user’s primary dial plan must be the same SIP URI dial plan used with Lync Server. But if the user requires more extension numbers, you shouldn't add another secondary extension to the primary dial plan. You must add a secondary dial plan and then add the secondary extension or EUM proxy address to the UM-enabled user.

For more information about adding, removing, or changing extensions, see one of the following:

  - [Change an extension number](change-an-extension-number-exchange-2013-help.md)

  - [Add an extension number](add-an-extension-number-exchange-2013-help.md)

  - [Remove an extension number](remove-an-extension-number-exchange-2013-help.md)

If you need to change SIP addresses or E.164 numbers for UM-enabled users, see:

  - [Add a SIP address](add-a-sip-address-exchange-2013-help.md)

  - [Change a SIP address](change-a-sip-address-exchange-2013-help.md)

  - [Remove a SIP address](remove-a-sip-address-exchange-2013-help.md)

  - [Add an E.164 number](add-an-e-164-number-exchange-2013-help.md)

  - [Change an E.164 number](change-an-e-164-number-exchange-2013-help.md)

  - [Remove an E.164 number](remove-an-e-164-number-exchange-2013-help.md)

## Call answering

Unified Messaging provides both of the following:

  - **Call answering**   Occurs when a user doesn't answer their phone and UM takes the call.

  - **Outlook Voice Access**   Used by users when they dial in to the voice mail system to access their mailbox.

Two configurations are used frequently:

  - A UM-enabled user has two extension numbers (one primary, one secondary) in the primary dial plan. These extensions correspond to different phones on the user's desk and are connected to the same PBX. These different numbers are available to two separate audiences. In this configuration, the primary extension is the “general” work number and the secondary extension is the “task-specific” number, possibly a helpdesk line, or a dedicated fax number.

  - A UM-enabled user spends a certain length of time, perhaps three weeks out of four, in their company’s main office and the rest of the time in another office at one of the company's remote locations. The two offices have different PBXs, and the extension numbers are unique to each PBX. In this example, the user is configured to have a primary extension in their primary dial plan on the main office PBX and a secondary extension in a secondary dial plan on the PBX of the other office.

In either configuration, voice messages or missed call notification messages that are generated by unanswered calls to either extension will be sent to the user’s Inbox.

## Outlook Voice Access

You may want UM-enabled users to be able to sign in to Outlook Voice Access from any extension, primary or secondary. While this is possible, there may be some architectural restrictions that keep this from working identically from all extensions. To sign in to Outlook Voice Access, UM-enabled users must perform the following steps:

1.  Call an Outlook Voice Access number.

2.  Key in their extension number if they're calling from another phone number.

3.  Key in their PIN if they aren't enabled for Enterprise Voice and are calling from a Unified Communications phone, Office Communicator, or Lync Server.

**Usage scenarios**

  - **Single extension with Outlook Voice Access**   If the user has a single primary extension, they must always call the Outlook Voice Access number for their primary UM dial plan. If they call from their extension number, they won't be prompted to enter the extension number, and step 2 of the preceding steps will be skipped.

  - **Two extensions in the primary dial plan with Outlook Voice Access**   If the user has only two extensions, primary and secondary, and both the primary and secondary extension are in the same UM dial plan, they must always call the Outlook Voice Access number of the dial plan. If they call from either the primary or secondary extension, they won't be prompted to enter the extension number, and step 2 of the preceding steps will be skipped. Outlook Voice Access features will work the same way, whichever extension is used to sign in.

  - **Extensions in the primary dial plan and in a secondary dial plan with Outlook Voice Access**   If the user has only two extensions, primary and secondary, and the primary and secondary extensions are in different UM dial plans (primary and secondary); they should call the Outlook Voice Access number appropriate to their dial plan. From their primary extension, they should call the Outlook Voice Access number of the primary dial plan, and from their secondary extension, they should call the Outlook Voice Access number of the secondary dial plan. If they do this, they won't be prompted to enter the extension number, and step 2 of the preceding steps will be skipped.
    
    Outlook Voice Access features that don't involve outbound dialing (for example “Call the sender” or “Call the office”) will work the same way, whichever extension is used to sign in. However, Outlook Voice Access features that do require outbound dialing won't work as expected when the user signs in to the secondary dial plan unless the outbound dialing rules are exactly the same in both dial plans. For the behavior of outbound dialing to be exactly the same, you must ensure that the following properties are configured identically on the primary and secondary dial plans:
    
      - Dialing codes (trunk access, national, and international)
    
      - In-country or region dialing codes
    
      - Dialing rules
    
      - Dialing rule group names

A UM-enabled user is associated with a UM mailbox policy, and this UM mailbox policy is linked with the user's primary dial plan. The UM mailbox policy settings that are associated with the UM-enabled user's primary dial plan will be applied to the user. If a user is associated with a secondary dial plan with a second extension number in the secondary dial plan, the UM mailbox policy settings associated with the primary dial plan will still be applied. In Outlook Voice Access, the same UM mailbox policy settings associated with the primary dial plan are applied whether the user calls in to the primary dial plan or to a secondary dial plan.

The **AllowedInCountryOrRegionGroups** and **AllowedInternationalGroups** properties on the UM mailbox policy contain the names of groups of dialing rules that are configured on the **ConfiguredInCountryOrRegionGroups** and **ConfiguredInternationalGroups** properties of a UM dial plan. When a UM-enabled user calls in to Outlook Voice Access, the outbound calling rules from the UM mailbox policy associated with the primary or secondary dial plan will apply to calls the user makes, depending on whether the UM-enabled user has called in to the primary or secondary dial plan's Outlook Voice Access number.

For example, if a primary dial plan named “Contoso Dial Plan 1” has a dialing rule named “US and Canada” in its **ConfiguredInCountryOrRegionGroups** property, the UM mailbox policy “Contoso UM Policy 1” might also have “US and Canada” in its **AllowedInCountryOrRegionGroups** property. If you want to add a secondary extension in “Contoso Dial Plan 2” for a user in “Contoso UM Policy 2”, you would have to ensure that the **ConfiguredInCountryOrRegionGroups** property of “Contoso Dial Plan 2” also contains a rule named “US and Canada”. Otherwise, if the user signs in to Outlook Voice Access from their secondary extension, UM won't be able to find a rule on the secondary dial plan named “US and Canada”. If this happens, UM will only allow the user to call numbers allowed to any caller to the secondary dial plan, which could be more restrictive.

Return to top

## UM features that operate differently for secondary dial plans

There's a set of UM features that can use secondary dial plans but may not work correctly in certain situations. It's important that you understand how each of these features is affected when you configure UM-enabled users to use a secondary dial plan.

## Play on Phone

In Outlook Web App, Play on Phone uses the VoIP gateway that's associated with the user’s primary dial plan to make the outbound call. It applies dialing rules from the primary dial plan and the UM mailbox policy that's associated with the user's mailbox.

## Directory search (Outlook Voice Access)

A search of the directory for a user who's been authenticated will follow these rules:

  - The ability to search for a user and then leave a voice message or call a user will be available only if the user conducting the search is UM enabled and has a primary extension on the same dial plan as the user that's being called. If so, a search by name, alias, and primary extension will locate the user. However, searching by using the secondary extension won't locate the user.

  - If the user being searched for is UM enabled and has a secondary extension on the called dial plan, then a search by name, alias, and secondary extension will find the user. However, although options to leave a voice message and call the contact will be offered, the call contact option won't succeed. In this case, a search by primary extension won't find the user.

  - To find and be able to either call or leave a voice message for the user they're searching for, the UM-enabled user should use Outlook Voice Access through their primary dial plan's Outlook Voice Access number and search by name, alias, or primary extension. If the searched-for user is called using the secondary dial plan's Outlook Voice Access number, the user will only be found if the search is made by name, alias, or secondary extension. If the primary extension is used, the only option that will be available is for the user to leave a voice mail.

## Directory search (Outlook Voice Access)

A search of the directory for a user who hasn't been authenticated will follow these rules:

  - The user being searched for will be found and the option to leave a voice message or call the user will be offered only if the user is UM enabled and has a primary extension on the called dial plan. If so, a search by name, alias, and primary extension will find the user. However, a search by secondary extension won't find the user.

  - If the user being searched for is UM enabled, has a secondary extension on the called dial plan, and the option **Transfer and search** \> **Allow callers to** \> **Leave voice messages without ringing a user’s phone** is selected on the called dial plan, then a search by name, alias, and secondary extension will find them. However, the option to leave voice mail will be offered to the caller, and there will be no option to call them.

  - To find and be able to either call or leave a voice message for a user, the caller must call the Outlook Voice Access number of the user's primary dial plan and search by name, alias, or the user's secondary extension. If the user's secondary Outlook Voice Access number is called, they will only be found if the **Allow callers to search by name of alias** option is set to **In the entire organization**. In this case, only the option to leave a voice message will be provided.

## Call the Sender (Outlook Voice Access)

When a user calls in to Outlook Voice Access and chooses the option to Call the Sender, they can send either an email message or a voice mail message to a UM-enabled user. The options available depend on whether the caller is associated with the same dial plan as the sender they're calling. Calls to a UM-enabled user when the caller dials in to an Outlook Voice Access number and the caller is authenticated will follow these rules:

  - **Email messages**   If the sender of the email message is a UM-enabled user, choosing the option to call the sender will result in a call to the sender’s primary extension that's configured on the user's primary dial plan. In the case where the sender’s primary extension is on a dial plan that's different from the caller's, the prompt to “Call the Sender” will only be provided if there's a business, home, or mobile phone configured for the sender and the dialing rules are configured to allow the call.

  - **Voice mail messages**   If the caller is a UM-enabled user, the option to call the sender will always result in a call to the extension that the sender uses to leave their voice message. If this extension has a number of digits different from the called dial plan, the prompt to call the sender won't be provided unless there are dialing rules in place that would permit the call. For example:
    
      - The “Call the sender” option will be offered if the sender uses an extension on the dial plan that was used to send the voice message.
    
      - The “Call the sender” option will be played if the sender uses an extension from a different dial plan than the dial plan that's used with Outlook Voice Access to send the voice message and both dial plans have the same number of digits. The success of the call will depend on whether the VoIP gateway and PBX infrastructure permit the call transfer.
    
      - The “Call the sender” option won't be played if the sender uses an extension from a different dial plan than the dial plan that's used with Outlook Voice Access to send the voice message, the dial plans have a different number of digits, and there are no outdialing rules that match the sender's extension.

Return to top

