---
title: 'DSN message identity: Exchange 2013 Help'
TOCTitle: DSN message identity
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 49286847
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# DSN message identity

 

_**Applies to:** Exchange Server 2013_


You can identify a customized delivery status notification (DSN) message based on its syntax. The identity is the customized DSN message's GUID or a string that consists of the following values:

  - **Locale**   This variable specifies the locale of the language that the DSN message is displayed in. For a list of locale codes that you can use with the **New-SystemMessage** command, see [Supported languages for system messages](supported-languages-for-system-messages-exchange-2013-help.md).

  - **Internal or External**   This variable specifies whether the DSN message is sent only to senders who are part of the internal Microsoft Exchange Server 2013 organization or also to senders outside the Exchange organization. You can use the Internal option when you want to include a specific e-mail contact or resolution in DSN messages sent to internal senders, but don't want to expose that information to senders outside your organization.

  - **DSN code**   This variable specifies the DSN code of the customized DSN message.

The syntax of the DSN message identity is `<Locale>\<Internal or External>\<DSN code>`.

For each DSN code, you can create more than one customized DSN message, which can target internal senders or external senders, and different locales. For example, the following table shows some of the possible configurations for the DSN code 5.1.2 and the corresponding DSN message identities.

### Example DSN configurations and identities

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>DSN configuration</th>
<th>DSN identity</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Display DSN messages to internal senders with an English (en) locale</p></td>
<td><p>En\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Display DSN messages to external senders with an English (en) locale</p></td>
<td><p>En\External\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>Display DSN messages to internal senders with a Japanese (ja) locale</p></td>
<td><p>Ja\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Display DSN messages to external senders with a Japanese (ja) locale</p></td>
<td><p>Ja\External\5.1.2</p></td>
</tr>
</tbody>
</table>

