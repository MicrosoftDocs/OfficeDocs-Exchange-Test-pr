---
title: 'Exchange Remote Connectivity Analyzer: Exchange 2013 Help'
TOCTitle: Exchange Remote Connectivity Analyzer
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 49289433
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# Exchange Remote Connectivity Analyzer

 

_**Applies to:** Exchange Server 2013_


The Microsoft Exchange Remote Connectivity Analyzer (ExRCA) helps you make sure that connectivity for your Exchange servers is set up correctly. If you’re having problems, it can also help you find and fix these problems. The ExRCA website can run tests to check for Microsoft Exchange ActiveSync, Exchange Web Services, Microsoft Outlook, and Internet email connectivity.

## Remote Connectivity Analyzer tests

You can perform several tests with the ExRCA. The following tests work on Exchange 2007 and later versions:

  - Exchange ActiveSync

  - Exchange Web Services

  - Outlook

  - Internet email

## Exchange ActiveSync tests

You can run the following tests for Exchange ActiveSync:

  - **Exchange ActiveSync:** This test simulates the steps that a mobile device uses to connect to an Exchange server using Exchange ActiveSync.

  - **Exchange ActiveSync Autodiscover:** This walks through the steps an Exchange ActiveSync device uses to obtain settings from the Autodiscover service.

## Exchange Web Services connectivity tests

The Exchange Web Services tests check the settings for many of the Exchange Web Services. You can run the following tests for Exchange Web Services:

  - **Synchronization, Notification, Availability, and Automatic Replies:** These tests walk through many basic Exchange Web Services tasks to confirm that they’re working. This is useful for IT administrators who want to troubleshoot external access using Entourage EWS or other Web Services clients.

  - **Service Account Access (Developers):** This test verifies a service account’s ability to access a specified mailbox, create and delete items in it, and access it via Exchange impersonation. This test is primarily used by application developers to test the ability to access mailboxes with alternate credentials.

## Microsoft Office Outlook Connectivity tests

You can run the following tests for Outlook connectivity:

  - **Outlook Anywhere (RPC over HTTP):** This test walks through the steps Outlook uses to connect via Outlook Anywhere (RPC over HTTP).

  - **Outlook Autodiscover:** This test walks through the steps Outlook uses to obtain settings from the Autodiscover service. This test doesn't actually connect to a mailbox.

## Internet email tests

You can run the following tests for Internet email:

  - **Inbound SMTP** **E-Mail:** This test walks through the steps an Internet email server uses to send inbound SMTP email to your domain.

  - **Outbound SMTP E-Mail:** This test checks your outbound IP address for certain requirements. This includes Reverse DNS, Sender ID, and RBL checks.

  - **POP Email:** This test walks through the steps an email client uses to connect to a mailbox using POP3.

  - **IMAP Email:** This test walks through the steps an email client uses to connect to a mailbox using IMAP.

