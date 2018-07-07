---
title: 'Checklist: Deploy Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 'Checklist: Deploy Exchange 2013 UM'
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 49315398
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Checklist: Deploy Exchange 2013 UM

 

_**Applies to:** Exchange Server 2013_


Use this checklist to help you install and deploy Unified Messaging (UM) in your organization.

Before you start working with this checklist, make sure you're familiar with the concepts in:

  - [Unified Messaging](unified-messaging-exchange-2013-help.md)

  - [New voice mail features](new-voice-mail-features-exchange-2013-help.md)

  - [Planning for Unified Messaging](planning-for-unified-messaging-exchange-2013-help.md)

For step-by-step guidance about how to deploy UM and Microsoft Lync Server, see [Checklist: Integrate Exchange 2013 UM with Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).

## Checklist for deploying Unified Messaging


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Done?</th>
<th>Tasks</th>
<th>Topic</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Deploy and configure telephony components.</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">Connect UM to your telephone system</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Review the system requirements before installing Exchange 2013.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 system requirements</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Verify that you meet the prerequisites for installation.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 prerequisites</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Install the required Client Access and Mailbox servers.</p>

> [!WARNING]
> You must deploy at least one Exchange 2013 Mailbox server in your organization before you configure the VoIP gateways or IP PBXs to send UM SIP and RTP traffic to the Exchange 2013 Client Access servers.


</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Install Exchange 2013 using the Setup wizard</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verify the installation and review the server setup logs.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verify an Exchange 2013 installation</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>If required, install the required UM language packs.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Install a UM language pack</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Create the number of dial plans required for your organization.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Create a UM dial plan</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure the dial plan security setting.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">Configure the VoIP security setting</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Configure the UM startup mode for each Client Access and Mailbox server.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configure the startup mode on a Mailbox server</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configure the startup mode on a Client Access server</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure the number of concurrent calls on your Mailbox servers.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configure the number of incoming calls on a Mailbox server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure Outlook Voice Access numbers and other settings.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Manage a UM dial plan</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure outbound dialing for Unified Messaging.</p></td>
<td><p><a href="authorize-calls-using-dialing-rules-exchange-2013-help.md">Authorize calls using dialing rules</a></p>
<p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Authorize calls for users in a dial plan</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Authorize calls for a group of users</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Create the required number of auto attendants.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">Create a UM auto attendant</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Set up and configure each of the UM auto attendants.</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">Set up a UM auto attendant</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Create, import, and enable a new Exchange certificate for UM or enable a mutually-trusted third-party certificate. Also, import the certificate on all VoIP gateways, IP PBXs, and SBCs.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Add Mailbox and Client Access servers to a SIP URI dial plan</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Restart the Microsoft Exchange Unified Messaging service and the Unified Messaging Call Router service on all Exchange servers to load the required certificates.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Stop the Microsoft Exchange Unified Messaging service</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Start the Microsoft Exchange Unified Messaging service</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Stop the Microsoft Exchange Unified Messaging Call Router service</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Start the Microsoft Exchange Unified Messaging Call Router service</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Create a UM mailbox policy or configure the default UM mailbox policy.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Create a UM mailbox policy</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Manage a UM mailbox policy</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Enable users for Unified Messaging with an extension number and an E.164 number, if required.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Enable a user for voice mail</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Enable incoming faxing (Optional).</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">Enable voice mail users to receive faxes</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Set up Protected Voice Mail (Optional).</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Protect voice mail</a></p></td>
</tr>
</tbody>
</table>


Return to top

