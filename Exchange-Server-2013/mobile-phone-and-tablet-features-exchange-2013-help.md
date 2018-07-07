---
title: 'Mobile phone and tablet features: Exchange 2013 Help'
TOCTitle: Mobile phone and tablet features
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50396326
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Mobile phone and tablet features

 

_**Applies to:** Exchange Server 2013_


Users can access their email, calendar, contacts, and task information on mobile phones, tablets, and other portable devices through Microsoft Exchange ActiveSync. They can also use it to set up their signature and automatic replies. A wide variety of mobile phones and devices work with Exchange ActiveSync.


> [!NOTE]
> Although we consistently refer to devices that access Exchange Server 2013 as mobile phones, there are many devices that can access Exchange 2013 but don't have cellular phone functionality. The term "mobile phone" in this documentation refers to those devices, as well.



## Exchange ActiveSync-compatible devices

Users can take advantage of the rich features of Exchange ActiveSync by selecting mobile phones that are compatible with Exchange ActiveSync. These mobile phones are available from many manufacturers and on many carriers. For more information, see the specific mobile phone documentation.

Mobile phones that are compatible with Microsoft Exchange include the following:

  - **Apple**   The Apple iPhone, iPod Touch, and iPad all support Exchange ActiveSync.

  - **Windows Phone**   Windows Phone 8, Windows Phone 7, and previous versions all support Exchange ActiveSync.

  - **Android**   Many mobile phones and tablets with the Android operating system support Exchange ActiveSync. However, these mobile devices may not support all available mobile device mailbox policies. For more information, see [Mobile device mailbox policies](mobile-device-mailbox-policies-exchange-2013-help.md).

## Windows Phone software features

Mobile phones that have a version of Windows Phone software as their operating system offer the greatest functionality when synchronizing with Exchange 2013. The following table lists the mobile device mailbox policies that are available with Windows Phone 8 and Windows Phone 7.

### Windows Phone 7 and 8 features

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Operating system</th>
<th>Features</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8 supports the following mobile device mailbox policies:</p>
<ul>
<li><p>Allow simple device password</p></li>
<li><p>Alphanumeric password required</p></li>
<li><p>Device password enabled</p></li>
<li><p>Device password expiration</p></li>
<li><p>IRM enabled</p></li>
<li><p>Maximum device password failed attempts</p></li>
<li><p>Maximum inactivity device time lock</p></li>
<li><p>Minimum device password complex characters</p></li>
<li><p>Minimum device password length</p></li>
<li><p>Require device encryption</p></li>
<li><p>Remote wipe</p></li>
</ul>

> [!WARNING]
> If your organization uses other mobile device mailbox policy settings, you’ll need to set the <STRONG>Allow non-provisionable devices</STRONG> policy to true. This can have security implications for your organization, because other mobile phones and devices that don’t meet all the requirements of your mobile device policy settings will be allowed to synchronize. For more information, see <A href="mobile-device-mailbox-policies-exchange-2013-help.md">Mobile device mailbox policies</A>.


</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Windows Phone 7 mobile phones support only a subset of all Exchange ActiveSync mailbox policy settings:</p>
<ul>
<li><p>Password required</p></li>
<li><p>Minimum password length</p></li>
<li><p>Maximum inactivity time lock</p></li>
<li><p>Maximum device password failed attempts</p></li>
<li><p>Allow simple password</p></li>
<li><p>Password expiration</p></li>
<li><p>Password history</p></li>
<li><p>Disable removable storage</p></li>
<li><p>Disable IrDA</p></li>
<li><p>Disable desktop sync</p></li>
<li><p>Block remote desktop</p></li>
<li><p>Block Internet sharing</p></li>
</ul></td>
</tr>
</tbody>
</table>

