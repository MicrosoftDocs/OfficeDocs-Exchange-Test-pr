---
title: 'Simplify the Outlook Web App URL: Exchange 2013 Help'
TOCTitle: Simplify the Outlook Web App URL
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 53957625
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Simplify the Outlook Web App URL

 

_**Applies to:** Exchange Server 2013_


**Summary:** Use the procedures in this article to simplify the URL that your organization users to access OWA in Exchange 2013.

You can simplify the Microsoft Outlook Web App URL that users use to access their Exchange Server 2013 mailbox.

To simplify access to Outlook Web App for your users, you may want to configure the Outlook Web App Web page, which is usually the default website in IIS, to automatically redirect users to https. The procedure in the “Use IIS Manager to simplify the Outlook Web App URL and force redirection to SSL” section redirects a request for http://*server* to https://*server*/owa. To help secure the information that's sent between the client and the server, the default Web site is set to require Secure Sockets Layer (SSL) at installation.

When you configure redirection from a top-level directory in Windows Server 2008, the settings are propagated to lower-level directories. For example, when you configure redirection on the default website to the /owa virtual directory, the settings that you configure also appear on the HTTP Redirect page of all the virtual directories, such as /Autodiscover, /Exchange, and /Public. Therefore, you must remove redirection from all the virtual directories except the one that you want redirected.

## What do you need to know before you begin?

  - Estimated time to complete: 10 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "IIS Manager" entry in the Outlook Web App Permissions section of the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Step 1: Use IIS Manager to simplify the Outlook Web App URL and force redirection to SSL

1.  Start IIS Manager.

2.  Expand the local computer, expand **Sites**, and then click **Default Web Site**.

3.  At the bottom of the Default Web Site Home pane, click **Features View** if this option isn't already selected.

4.  In the **IIS** section, double-click **HTTP Redirect**.

5.  Select the **Redirect requests to this destination** check box.

6.  Type the absolute path of the /owa virtual directory. For example, type **https://mail.contoso.com/owa**.

7.  Under **Redirect Behavior**, select the **Only redirect requests to content in this directory (not subdirectories)** check box.

8.  In the **Status code** list, click **Found (302)**.

9.  In the Actions pane, click **Apply**.

10. Click **Default Web Site**.

11. In the Default Web Site Home pane, double-click **SSL Settings**.

12. In **SSL Settings**, clear **Require SSL**.
    

    > [!NOTE]
    > If you don’t clear <STRONG>Require SSL</STRONG>, users won’t be redirected when they enter an unsecured URL. Instead, they’ll get an access denied error.



## Step 2: Remove redirection from virtual directories

To remove redirection from a virtual directory, perform the following steps:

1.  Open a Command Prompt window.

2.  Navigate to \<*Window directory*\>\\System32\\Inetsrv.

3.  Run the following commands:
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  Finish by running the command `iisreset/noforce`.

When you configure redirection from a top-level directory, a web.config file may be created under \<*drive*\>\\Program Files\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab. If this has happened and you later remove redirection, Outlook may freeze when users click **Send and Receive**. To avoid this happening after you remove redirection, delete the web.config file from \<*drive*\>\\Program Files\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab.

## How do you know this worked?

To verify that you have successfully simplified the Outlook Web App URL and redirected it to an SSL connection, do the following:

1.  Open a web browser and enter the new URL for Outlook Web App, using the format http://\<*URL*\>.

2.  You should be redirected to the Outlook Web App sign-in page through an SSL connection.

