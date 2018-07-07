---
title: 'Client Access role not detected in local site_ClientAccessRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: Client Access role not detected in local site_ClientAccessRoleNotPresentInSite
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 46629089
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Client Access role not detected in local site\_ClientAccessRoleNotPresentInSite

 

_**Applies to:** Exchange Server_


The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup displayed this warning because an existing Client Access role could not be detected in the local Active Directory® directory service site.

You have chosen to install the Mailbox Server role before an instance of the Client Access role is installed in the Active Directory site.

The Client Access server role accepts connections to your Exchange 2007 server from a variety of different clients. Software clients such as Microsoft Outlook Express and Eudora use POP3 or IMAP4 connections to communicate with the Exchange server. Hardware clients, such as mobile devices, use ActiveSync, POP3, or IMAP4 to communicate with the Exchange server.

If users access their Inbox by using any client other than Microsoft Office Outlook®, you must install the Client Access server role in your Exchange organization.

Users will be able to logon to their mailboxes with Outlook but will not be able to use Outlook Web Access or mobile devices against the same mailbox until a Client Access role is present in the local Active Directory site.

