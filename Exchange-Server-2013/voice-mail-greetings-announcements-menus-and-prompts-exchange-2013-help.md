---
title: 'Voice mail greetings, announcements, menus, and prompts: Exchange 2013 Help'
TOCTitle: Voice mail greetings, announcements, menus, and prompts
ms:assetid: df61105d-c9d8-452c-b028-50cbda47aecf
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb124902(v=EXCHG.150)
ms:contentKeyID: 49315544
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Voice mail greetings, announcements, menus, and prompts

 

_**Applies to:** Exchange Server 2013_


When you install Unified Messaging (UM), a common set of default audio files used for the voice mail system and for menu prompts, greetings, and informational announcements is installed. Although you can create a fully functional UM auto attendant or dial plan that uses only the default audio prompts, these prompts are too generic to serve as an acceptable public interface for many companies. This topic discusses the system and menu prompts, greetings, and informational announcements that are used by UM dial plans and auto attendants and how they're used when callers access the voice mail system.

**Contents**

Overview of audio prompts and greetings

System prompts

UM dial plan greetings and announcements

UM auto attendant greetings, announcements, and menu prompts

Customizing greetings, announcements, and menu prompts

## Overview of audio prompts and greetings

After Unified Messaging is installed, audio files for UM dial plans and auto attendants are copied to the Mailbox server. By default, the installation program copies the audio files to the Program Files\\Microsoft\\Exchange Server\\V15\\Unified Messaging\\Prompts*\\\<language\>* folder. If you've installed the U.S. English version, a folder named \\en is created during installation to hold the U.S. English versions of the system prompts. The Mailbox server plays these system prompts to callers so they can hear greetings, menu prompts, and informational announcements and so they can navigate the UM menus.

These system audio files or prompts should never be replaced. However, UM enables you to customize UM dial plan and auto attendant welcome greetings, main menu prompts, and informational announcements.

The following table summarizes the prompts and greetings used with UM dial plans.

### Audio prompts for UM dial plans

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompts and greetings</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>System prompts</p></td>
<td><p>Must not be modified.</p></td>
</tr>
<tr class="even">
<td><p>Welcome greeting</p></td>
<td><p>The default welcome greeting is a system prompt that is played by default. However, you can use a customized greeting file that you create.</p></td>
</tr>
<tr class="odd">
<td><p>Informational announcement</p></td>
<td><p>By default, informational announcements are disabled. If you enable an informational announcement, you must specify a customized greeting file.</p></td>
</tr>
</tbody>
</table>


The following table summarizes the prompts and greetings used with UM auto attendants.

### Audio prompts for UM auto attendants

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompts and greetings</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>System prompts</p></td>
<td><p>Must not be modified.</p></td>
</tr>
<tr class="even">
<td><p>Business hours menu prompts</p></td>
<td><p>By default, business hours menu prompts are enabled and a system prompt is played. However, you can use a customized greeting file that you create.</p></td>
</tr>
<tr class="odd">
<td><p>Non-business hours menu prompts</p></td>
<td><p>By default, non-business hours menu prompts are enabled and a system prompt is played. However, you can use a customized greeting file that you create.</p></td>
</tr>
<tr class="even">
<td><p>Business hours greeting</p></td>
<td><p>By default, a business hours greeting is enabled and a system prompt is played. However, you can use a customized greeting file that you create. This is also known as a welcome greeting.</p></td>
</tr>
<tr class="odd">
<td><p>Non-business hours greeting</p></td>
<td><p>By default, a non-business hours greeting is enabled and a system prompt is played. However, you can use a customized greeting file that you create. This is also known as a welcome greeting.</p></td>
</tr>
<tr class="even">
<td><p>Informational announcement</p></td>
<td><p>By default, informational announcements are disabled. If you enable an informational announcement, you must specify a customized greeting file.</p></td>
</tr>
</tbody>
</table>



> [!WARNING]
> Modifying the installed system prompts isn't supported.



Return to top

## System prompts

Unified Messaging is installed with a set of default audio prompts for use with Outlook Voice Access, dial plans, and auto attendants. Hundreds of system prompts for each language are installed on a Mailbox server. The Mailbox server plays the audio files for these system prompts to callers when they access the voice mail system. The following are some examples of these system prompts:

  - "Please enter your PIN."

  - "To access your mailbox, enter your extension."

  - "To contact someone, press the \# key."

  - "Spell the name of the person you are calling, last name first."

  - "To reach a specific person, just tell me the name."


> [!WARNING]
> Modifying the installed system prompts isn't supported.




> [!NOTE]
> When the Unified Messaging service starts on the Mailbox server, it will verify that all the system prompts are available. If a system prompt can't be found, Unified Messaging will return an error. To fix the error that is returned, locate the event using Event Viewer and copy the file listed in the <STRONG>Event Properties</STRONG> window from the installation DVD into the appropriate folder on the Mailbox server.



## UM dial plan greetings and announcements

After you install the Mailbox server and create a UM dial plan, you have the option to use the audio files for the default system prompts that are created during installation or to create customized audio files that can be used with UM dial plans.

UM dial plans have a welcome greeting and an optional informational announcement you can modify. The welcome greeting is used when an Outlook Voice Access user or another caller calls the subscriber access number. The callers hear a default welcome greeting that says, "Welcome, you are connected to Microsoft Exchange." You might want to change this default greeting and provide an alternative welcome greeting specific to your company, for example, "Welcome to Outlook Voice Access for Woodgrove Bank." If you customize this greeting, you can record the customized greeting and save it as a .wav file, and then you can configure the dial plan to use this customized greeting.

Unified Messaging allows for an informational announcement to follow the welcome greeting. By default, there is no informational announcement configured. However, you may want to provide one for callers. You can use the informational announcement for general announcements that change more often than the welcome greeting or for announcements required by corporate compliance policies. When it's important that the whole informational announcement is heard, you can configure it to be uninterruptible. This prevents a caller from pressing a key or speaking a command to interrupt and stop the informational announcement.

The following table describes the UM dial plan greetings and informational announcements.

### UM dial plan greetings and informational announcements

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Greeting</th>
<th>Default example</th>
<th>Customized example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Welcome greeting</p></td>
<td><p>&quot;Welcome, you are connected to Microsoft Exchange.&quot;</p></td>
<td><p>&quot;Welcome to Outlook Voice Access for Woodgrove Bank.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Informational announcement</p></td>
<td><p>By default, an informational announcement isn't configured.</p></td>
<td><p>&quot;By using this system you agree to adhere to all corporate policies when you are accessing this system.&quot;</p></td>
</tr>
</tbody>
</table>


When you are customizing and configuring greetings and announcements, make sure the language setting configured on the UM dial plan is the same as the language of the custom prompts you create. If not, a caller may hear a message or greeting in one language and another message or greeting in a different language.

Return to top

## UM auto attendant greetings, announcements, and menu prompts

As with UM dial plans, UM auto attendants have a welcome greeting, an optional informational announcement, and an optional custom menu prompt. You can configure different versions of the welcome greeting and menu prompt for business hours and non-business hours. You can modify all of them.

The welcome greeting is the first thing a caller hears when a UM auto attendant answers the call. By default, this says, "Welcome to the Microsoft Exchange auto attendant." The audio file that is played for the call is the default system prompt for the UM auto attendant. However, you may want to provide an alternative greeting specific to your company, for example, "Thank you for calling Woodgrove Bank." To customize this welcome greeting, record the customized greeting and save it as a .wav file, and then configure the auto attendant to use this customized greeting. As with the welcome greetings, you can also customize the menu prompts.

Unified Messaging also allows for an informational announcement to follow a business hours greeting or a non-business hour greeting. By default, no informational announcement is configured, but you may want to provide one to callers. The informational announcement can announce your company's business hours, for example, "Our business hours are 8:00 A.M. to 5:00 P.M., Monday through Friday, and 8:30 A.M. to 1:00 P.M. on Saturday." The informational announcement can also provide information required for compliance with corporate policies, for example, "Calls may be monitored for training purposes." When it's important that the whole informational announcement is heard, you can configure it to be uninterruptible. This prevents the caller from pressing a key or speaking a command to interrupt and stop the informational announcement.

The following table describes the UM auto attendant greetings and informational announcements.

### UM auto attendant greetings, informational announcement, and menu prompts

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Greeting</th>
<th>Default example</th>
<th>Customized example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Business hours greeting</p></td>
<td><p>&quot;Welcome to the Microsoft Exchange auto attendant.&quot;</p></td>
<td><p>&quot;Thank you for calling Woodgrove Bank.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Non-business hours greeting</p></td>
<td><p>No default non-business hours greeting is played until you configure the business hours for the auto attendant. However, the business hours greeting is played for callers during all times of the day.</p></td>
<td><p>&quot;You have reached Woodgrove Bank after business hours. Our business hours are from 8:00 A.M. until 5:00 P.M., Monday through Friday.&quot;</p></td>
</tr>
<tr class="odd">
<td><p>Informational announcement</p></td>
<td><p>By default, informational announcements aren't configured.</p></td>
<td><p>&quot;Calls may be monitored for training purposes.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Business hours main menu prompt</p></td>
<td><p>No default business hours main menu prompt will be played until you configure key mappings on the auto attendant.</p></td>
<td><p>&quot;For technical support, press or say 1. For corporate offices and administration, press or say 2. For sales, press or say 3.&quot;</p></td>
</tr>
<tr class="odd">
<td><p>Non-business hours main menu prompt</p></td>
<td><p>No default non-business hours main menu prompt will be played until you configure key mappings and the business hours schedule on the auto attendant.</p></td>
<td><p>&quot;Your call is very important to us. However, you have reached Woodgrove Bank after business hours. If you want to leave a message, please press or say 1, and we will return your call as soon as possible.&quot;</p></td>
</tr>
</tbody>
</table>


As with UM dial plans, make sure the language setting configured on the UM auto attendant is the same as the language of the custom greetings you create and is set to the same language as the UM dial plan. If not, a caller may hear a message or greeting in one language and another message or greeting in a different language.

Return to top

## Customizing greetings, announcements, and menu prompts, and navigation menus

Although the system prompts mustn't be replaced or changed, you'll probably want to customize the greetings, informational announcements, menu prompts and navigation menus used with UM dial plans and auto attendants. After installation, you can configure the UM dial plans and auto attendants to use custom audio files (.wav or .wma). You must follow these steps before you can enable custom voice prompts for callers:

1.  Record the custom greetings, announcements, and prompts and save then as .wav files. The Linear PCM (16 bit/sample), 8 kilohertz (kHz) audio codec must be used to encode the .wav files. If you don't use this specific format for the .wav files, an error will be generated stating that the source file is in an unsupported format. Although an error is generated, the error won't appear in Event Viewer.

2.  Configure the UM dial plan or auto attendant to use the customized greetings, announcements, and prompts.

By default, when you create a UM auto attendant, the business and non-business hours greetings or prompts aren't configured and no key mappings are defined for business or non-business hours main menu prompts. To correctly configure customized greetings and prompts for an auto attendant, you must:

  - Configure business and non-business hours on the **Business hours** page.

  - Create the greeting audio (.wav or .wma) files that will be used for the business and non-business hours welcome greetings.

  - Configure the business and non-business hours welcome greetings on the **Greetings** page.

  - Create the greeting files that will be used for the business and non-business hours main menu prompt greetings.

  - Configure the business and non-business hours main menu prompt greetings on the **Greetings** page.

  - Enable and configure the business and non-business hours menu navigation on the **Menu navigation** page.

Return to top

