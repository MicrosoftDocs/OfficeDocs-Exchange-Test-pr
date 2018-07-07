---
title: 'Import and export custom greetings, announcements, menus, and prompts: Exchange 2013 Help'
TOCTitle: Import and export custom greetings, announcements, menus, and prompts
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 53366393
ms.date: 12/09/2016
mtps_version: v=EXCHG.150
---

# Import and export custom greetings, announcements, menus, and prompts

 

_**Applies to:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_


You can import and export the audio files that you’ve recorded to use on Unified Messaging (UM) dial plans and auto attendants. For example, you might want to export and save a copy of an audio file if you’re upgrading from a previous version of Exchange. Or, you might need to import a copy of a recorded audio prompt before configuring a dial plan or auto attendant.

The audio files are used for the following purposes:

  - On UM dial plans, audio files are used for customized welcome greetings and informational announcements. They’re played when Outlook Voice Access users call in to an Outlook Voice Access number.

  - On UM auto attendants, audio files are used for customized non-business and business hours greetings, informational announcements, menu prompts, and navigation menus. They’re played when callers call in to a UM auto attendant.

The following audio file formats are supported for custom greetings, announcements, menus, and prompts:

  - .wma files encoded with Windows Media Audio 9.2 - 96 kbps/44 kHz/stereo 1-pass CBR (Windows Sound Recorder)

  - Windows Media Audio Voice 9 - 8 kbps/8 kHz/Mono, and .wav files encoded with the Linear PCM (16 bit/sample), 8 kilohertz (kHz) audio codec

You import the audio files that are used by UM dial plans and auto attendants into the system mailbox named {e0dc1c29-89c3-4034-b678-e6c29d823ed9} and export the audio files from this system mailbox. The audio files can be imported and exported by using the **Import-UMPrompt** and **Export-UMPrompt** cmdlets.

For additional management tasks related to UM dial plans, see [UM dial plan procedures](um-dial-plan-procedures-exchange-2013-help.md).

For additional management tasks related to UM auto attendants, see [UM auto attendant procedures](um-auto-attendant-procedures-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 3 minutes.

  - You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "UM dial plans" and “UM auto attendants�? entries in the [Unified Messaging permissions](unified-messaging-permissions-exchange-2013-help.md) topic.

  - Before you perform these procedures, confirm that a UM dial plan has been created. For detailed steps, see [Create a UM dial plan](create-a-um-dial-plan-exchange-2013-help.md).

  - Before you perform these procedures, confirm that a UM auto attendant has been created. For detailed steps, see [Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md).

  - You can only use the Shell to perform this procedure.

  - For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, or <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## What do you want to do?

## Use the Shell to import custom greetings, announcements, menus, and prompts for UM dial plans and auto attendants

This example imports the welcome greeting file named welcomegreeting.wav from d:\\UMPrompts into the UM dial plan `MyUMDialPlan`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

This example imports the welcome greeting file named welcomegreeting.wav from d:\\UMPrompts into the UM auto attendant `MyUMAutoAttendant`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## Use the Shell to export custom greetings, announcements, menus, and prompts from UM dial plans and auto attendants

This example exports the welcome greeting for the UM dial plan `MyUMDialPlan` and saves it as the file named welcomegreeting.wav.

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

This example exports the business hours welcome greeting for the UM auto attendant `MYUMAutoAttendant` and saves it as the file named BusinessHoursWelcomeGreeting.wav.

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte

