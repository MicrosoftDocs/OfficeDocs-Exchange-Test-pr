---
title: 'Remove a UM language pack: Exchange 2013 Help'
TOCTitle: Remove a UM language pack
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 49315473
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Remove a UM language pack

 

_**Applies to:** Exchange Server 2013_


You can use the EAC or the Shell to manage Unified Messaging (UM) languages on Mailbox servers running the Microsoft Exchange Unified Messaging service. However, to remove a language from the list on a UM dial plan, you must remove the appropriate UM language pack from the Mailbox server by using the **Setup.exe /RemoveUmLanguagePack** command. After you remove the UM language pack from the Mailbox server, the language won't be available when you configure a UM dial plan or a UM auto attendant. You can view the UM language packs that are installed by viewing the properties of the Mailbox server or by using the **Get-UMService** cmdlet.

For additional tasks related to UM languages, see [UM languages, prompts, and greetings procedures](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: Less than 5 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox server (UM service)" entry in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Verify that a UM language pack other than en-US is installed.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Use Setup.exe to remove a UM language pack

At a command prompt, run the following command.

    Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>

In the previous command, *\<UmLanguagePackName\>* is the name of the UM language pack, for example, fr-FR.


> [!WARNING]
> You can't use the Setup.exe file that's located in the \Bin folder to remove a UM language pack after you've installed any updates. You must use the Setup.exe file from the Exchange 2013 DVD or the downloaded source files. If you don't, you'll see the following error: There is a version mismatch between the running application and the installed application.


