---
title: 'Authorize calls using dialing rules: Exchange 2013 Help'
TOCTitle: Authorize calls using dialing rules
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 50873795
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# Authorize calls using dialing rules

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


By default, users aren’t able to place outgoing calls. To specify the kinds of calls users can make, you first create dialing rules, then authorize groups of these dialing rules on UM dial plans, UM mailbox policies, or UM auto attendants. Before you can authorize dialing rule groups, you have to define dialing rules on a UM dial plan. For details, see [Create dialing rules for users](create-dialing-rules-for-users-exchange-2013-help.md).

Each dialing rule that you create will contain the types of calls or number patterns that you want to give users access to. You can allow different types of users to make different types of calls. The calls you allow can be within a country or region, or they can be international.

To authorize or restrict dialing, the following settings must be configured correctly:

  - **Dialing rules**   Dialing rules define the number that UM-enabled users dial and the number that will be sent from Unified Messaging and dialed by the Private Branch eXchange (PBX) or IP PBX. You create a dialing rule group by adding a dialing rule. After you create a dialing rule group, you add it to the list of authorized calls for an in-country/region or international dialing rule group.

  - **Dialing rule groups**   Dialing rule groups determine the types of calls that users within the dialing group can make.

  - **Dialing authorizations**   Dialing authorizations are used to determine the restrictions that will be applied to prevent users from incurring unnecessary telephone charges or from dialing long-distance calls.

## How do I authorize a dialing rule group?

Where you authorize dialing rule groups depends on the types of callers that you want to allow to make outgoing calls. For example, if you want only Outlook Voice Access users to place outgoing calls, you would create your dialing rules and then authorize those dialing rule groups to the UM mailbox policy that the Outlook Voice Access users are linked to. The following table shows how to authorize calls for different types of callers.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type of caller</th>
<th>Authorize dialing rule groups here</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Unauthenticated callers who call in to an Outlook Voice Access number and don’t enter a PIN</p></td>
<td><p>UM dial plan. For details, see <a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Authorize calls for users in a dial plan</a>.</p></td>
</tr>
<tr class="even">
<td><p>Authenticated callers who call in to an Outlook Voice Access number and enter a PIN</p></td>
<td><p>UM mailbox policy for the caller. For details, see <a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Authorize calls for a group of users</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Unauthenticated callers who call in to a telephone number that’s configured on a UM auto attendant</p></td>
<td><p>UM auto attendant. For details, see <a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">Authorize calls for auto attendant callers</a>.</p></td>
</tr>
</tbody>
</table>


Depending on which users you’re authorizing to make outbound calls, you’ll use the **Dialing authorization** page in the Exchange admin center (EAC) for the dial plan, the auto attendant, or the UM mailbox policy.

