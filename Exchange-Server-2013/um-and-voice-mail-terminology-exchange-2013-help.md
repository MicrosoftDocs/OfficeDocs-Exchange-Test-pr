---
title: 'UM and voice mail terminology: Exchange 2013 Help'
TOCTitle: UM and voice mail terminology
ms:assetid: 3a6d93f2-1802-4aed-8b83-35c7fd004d0c
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Ee633462(v=EXCHG.150)
ms:contentKeyID: 53908372
ms.date: 12/10/2017
mtps_version: v=EXCHG.150
---

# UM and voice mail terminology

 

_**Applies to:** Exchange Online, Exchange Server 2013, Exchange Server 2016_


This topic contains the terms and definitions that are used with Unified Messaging.

  - audio codec  
    A digital encoding of an analog voice signal. Most audio codecs provide compression of the data, at the cost of some loss of fidelity when the data is recovered. Audio codecs vary in their perceived sound quality, the bandwidth that is required to use them, and the system requirements that are needed to do the encoding.

<!-- end list -->

  - audio notes  
    Text-based notes that can be added to a voice mail message that has been received in Outlook or Outlook Web App.

<!-- end list -->

  - auto attendant  
    A software system that answers calls, plays prompts or instructions, and then collects input from the caller as touchtones or speech. Auto attendants can direct a call to telephone numbers or named users or to entities (for example, departments) that the caller specifies, without intervention from a human operator.

<!-- end list -->

  - Automatic Speech Recognition (ASR)  
    A technology that enables a computer to match human speech to a predefined set of words or phrases.

<!-- end list -->

  - call answering  
    The process by which a caller interacts with a voice mail system if the number they originally called isn't answered. Typically, the system will play a greeting or other prompt, and allow the caller to record a voice message.

<!-- end list -->

  - Call Answering Rules  
    A form of call answering in which the user for whom the call is being answered can specify rules to determine the behavior callers experience. The user can specify conditions to be evaluated, greetings, and choices to be provided to the caller, and actions (for example, transfer or leave a message) to be taken as a result of the caller's choice.

<!-- end list -->

  - circuit-switched network  
    A network in which there exists a dedicated connection. A dedicated connection is a circuit or channel set up between two nodes so that they can communicate.

<!-- end list -->

  - conditional call forwarding  
    A set of conditions that are chosen by a user to be used when they receive an incoming call. The call is redirected based on the conditions that are set.

<!-- end list -->

  - Dial by Name  
    A feature that enables a caller to spell a person’s name using the keys on a telephone (ABC=2, DEF=3, etc.).

<!-- end list -->

  - dial plan  
    For Unified Messaging, this is a set of telephony-capable endpoints that share a common numbering plan. The details of the plan are determined by the telephone system to which UM is connected. In the simplest case, this can be a private branch exchange (PBX) with its extensions, each with a unique, fixed-length number.

<!-- end list -->

  - dialing rule group  
    Dialing rule groups are created to enable telephone numbers to be modified before they're sent to a traditional or SIP-enabled PBX or IP PBX for outgoing calls. Dialing rule groups may remove digits from or add digits to telephone numbers that are being used to place calls by a Unified Messaging server.
    
    Each dialing rule group contains dialing rule entries that determine the types of in-country/region and international calls that users within a dialing rule group can make. Each dialing rule group must contain at least one dialing rule entry.

<!-- end list -->

  - fax partner  
    UM fax partners provide applications or services that can accept calls handed off by UM when a fax tone is detected. The partner's product or service then receives the fax data, creates a message, and delivers it to the UM-enabled user as an email message with a .tif attachment. These messages will appear in the Fax search folder in Outlook and Outlook Web App.

<!-- end list -->

  - hunt group  
    A set of extensions that are organized into a group, over which a traditional or SIP-enabled PBX or IP PBX “hunts” to find an available extension. A hunt group is used to direct calls to identically capable endpoints or to an application, such as voice mail.

<!-- end list -->

  - in-country/region number format  
    The in-country/region number format specifies how a user's telephone number should be dialed by Unified Messaging from one dial plan to a different dial plan that has the same country code. This is used by an auto attendant and when an Outlook Voice Access user searches and tries to call the user in the directory.
    
    This entry consists of a number prefix and a variable number of characters (for example, 020xxxxxxx).

<!-- end list -->

  - informational announcement  
    An audio message that is played when a caller first dials in to a voice mail system, which may describe some item of interest.

<!-- end list -->

  - international access code  
    The prefix that is used to direct a call internationally. The international access code is 011 in the United States and 00 in much of the rest of the world.

<!-- end list -->

  - international number format  
    The string of digits that is used to define how to dial someone from outside a specific country.

<!-- end list -->

  - Internet Protocol Private Branch eXchange (IP PBX)  
    A telephone switch that natively supports voice over IP (VoIP). An IP PBX uses VoIP-based protocols to communicate with IP-based hosts such as VoIP telephones over a packet-switched network. Some IP PBXs can also support the use of traditional analog and digital phones.

<!-- end list -->

  - matched name selection method  
    The mechanism used to help a caller differentiate between users with names that match the touchtone or speech input.

<!-- end list -->

  - message waiting indicator  
    A signal that indicates the presence of one or more unread voice messages. For voice mail systems, this is often a lamp on the phone or a stutter dial tone.

<!-- end list -->

  - Microsoft Exchange Unified Messaging Call Router service  
    A service that directs incoming calls for UM-enabled users to the Microsoft Exchange Unified Messaging service.

<!-- end list -->

  - Microsoft Exchange Unified Messaging service  
    A service that implements Unified Messaging capabilities for UM-enabled users.

<!-- end list -->

  - missed call notification  
    An email message that is sent to a UM-enabled user that indicates that someone called but did not leave a voice message.

<!-- end list -->

  - national number prefix  
    A prefix that is used to direct a call as an in-country call. In the United States, this prefix is 1. In the United Kingdom and most of the rest of the world, this prefix is 0.

<!-- end list -->

  - number mask  
    A set of numbers and wildcard characters that is used to determine the telephone number that the Mailbox server will dial. An “X” represents a single digit (0 … 9). An asterisk (\*) represents any number of such digits.

<!-- end list -->

  - numeric extension  
    A string of digits that doesn’t contain a “+” or a country/region code. In dial plans, extensions are required to have a specified length.

<!-- end list -->

  - outdialing  
    A process in which Unified Messaging (UM) dials or transfers calls. UM generally receives calls, but sometimes dials calls. For example, outdialing occurs when a UM auto attendant transfers a call to a user's extension, or when a UM-enabled user uses Play on Phone from Outlook.

<!-- end list -->

  - Outlook Voice Access  
    A series of voice prompts that allows authenticated callers to access their email, voice mail, calendar, and contact information using a standard analog, digital, or mobile telephone. Outlook Voice Access also enables authenticated callers to navigate their personal information in their mailbox, place calls, locate users, and navigate the system prompts and menus using DTMF, also known as touchtone, or voice inputs.

<!-- end list -->

  - outside line access code  
    The prefix that is used by UM (or a person using an internal extension on the PBX or IP PBX) to access an outside line. This prefix is typically 9.

<!-- end list -->

  - packet switching  
    A technique that divides a data message into smaller units called packets. Packets are sent to their destination by the best route available, and then they are reassembled at the receiving end.

<!-- end list -->

  - pilot identifier  
    A telephone number that points to a hunt group and is the access number for calls that are routed to Unified Messaging. This is also sometimes called a pilot number.

<!-- end list -->

  - PIN  
    A passcode that a user enters on the telephone to access their mailbox.

<!-- end list -->

  - Play on Phone  
    A Unified Messaging feature that users can use to play their voice messages or play and record personalized voice mail greetings over a telephone.

<!-- end list -->

  - Private Branch eXchange (PBX)  
    A private telephone network in an organization. Individual telephone numbers or extension numbers are supported, and calls are automatically routed to them. Users can call each other using extensions, even across distributed locations.

<!-- end list -->

  - prompt  
    An audio message played over the telephone to explain valid options to users.

<!-- end list -->

  - Protected Voice Mail  
    A UM feature that uses information rights management to encrypt the contents of voice messages and specify the operations permitted on them. Protection can be caused by caller action (marking the message as private), or by system policy.

<!-- end list -->

  - public switched telephone network (PSTN)  
    PSTN is a grouping of the world's public circuit-switched telephone networks. This grouping resembles the way that the Internet is a grouping of the world's public IP-based packet-switched networks.

<!-- end list -->

  - reset  
    When a PIN or a password is reset, the system randomly chooses a new, temporary PIN or password. The user is required to change the temporary PIN the next time that they sign in to Outlook Voice Access.

<!-- end list -->

  - reverse number lookup (RNL)  
    A method used to try to locate the name of a person, from a directory or other information store, based on a telephone number.

<!-- end list -->

  - RTAudio codec  
    An advanced speech codec that is designed for real-time two-way VoIP applications such as gaming, audio conferencing, and wireless applications over IP. RTAudio is the preferred Microsoft audio codec and is the default codec for Microsoft Lync Server platforms.

<!-- end list -->

  - SIP-enabled PBX  
    A SIP-enabled PBX is a telephony device that acts as a networking switch for switching calls in a telephony or circuit-switched network. However, the difference between a SIP-enabled PBX and a traditional PBX is that the SIP-enabled PBX can connect to the Internet and use the SIP protocol to make calls over the Internet.

<!-- end list -->

  - SIP notification  
    A SIP notification is a SIP message sent from one SIP peer to another to advise it of a change.

<!-- end list -->

  - SIP peer  
    A SIP-enabled device that provides telephony communications between a VoIP gateway, IP PBX, SIP-enabled PBX, Microsoft Lync servers, or VoIP phones and Unified Messaging services.

<!-- end list -->

  - star out  
    An action a caller can perform when they are dialed in to a Unified Messaging auto attendant but they want to be able to get to Outlook Voice Access to get their email and voice mail. To do this, they press the star (\*) key while the auto attendant prompts are being played.

<!-- end list -->

  - subscriber access number (Outlook Voice Access number)  
    A number that is configured in a traditional or SIP-enabled PBX or IP PBX and on a UM dial plan that allows users to access their mailbox using Outlook Voice Access. In some cases, this may be configured to be the same number as the subscriber access number or pilot number (also called a pilot identifier) on the traditional or SIP-enabled PBX or IP PBX and the UM hunt group.

<!-- end list -->

  - system prompt  
    A short audio recording for Unified Messaging, which is played to callers by the server. System prompts are used to welcome callers and to inform them of their options when they use the voice mail system.

<!-- end list -->

  - telephone user interface (TUI)  
    An interface that is used to navigate the menus of a voice mail system using DTMF, also known as touchtone, inputs.

<!-- end list -->

  - Text-to-Speech (TTS)  
    Technologies for translating or converting typewritten text into speech.

<!-- end list -->

  - UM IP gateway  
    (See IP gateway.) A UM IP gateway is the Exchange Unified Messaging representation of any SIP peer with which it can communicate using VoIP protocols. It may represent a device that interfaces with a traditional or SIP-enabled PBX, an IP PBX, or Microsoft Lync Server.

<!-- end list -->

  - UM worker process  
    A process that's created during the startup of the Microsoft Exchange Unified Messaging service. The UM service, on receiving a request to handle an incoming call, immediately redirects the request to a UM worker process, which carries out all subsequent interactions with the caller.

<!-- end list -->

  - UM Worker Process Manager  
    A component that handles the creation and monitoring of all the UM worker processes that are created.

<!-- end list -->

  - Unified Messaging  
    An application that consolidates a user’s voice mail and email into one mailbox, so that the user only needs to check a single location for messages, regardless of type. The email server is used as the platform for all types of messages, making it unnecessary to maintain separate voice mail and email infrastructures.

<!-- end list -->

  - voice mail  
    A system that records and stores telephone messages in a user mailbox.

<!-- end list -->

  - Voice Mail Preview  
    A feature that provides text, transcribed from the audio recording, on a voice message when it is delivered.

<!-- end list -->

  - voice message  
    An electronic message with a primary content of digitized audio.

<!-- end list -->

  - Voice over IP (VoIP)  
    The practice of using an IP data network to transmit voice calls.

<!-- end list -->

  - voice user interface (VUI)  
    An interface that is used to navigate the menus of a voice mail system using speech inputs.

<!-- end list -->

  - VoIP gateway
    
    1.  A third-party hardware device or product that connects a legacy PBX to a LAN. A VoIP gateway translates or converts TDM or telephony circuit-switched protocols to packet-switched protocols that can be used on a VoIP-based network.
    
    2.  The Exchange Unified Messaging representation of any SIP peer with which it can communicate using VoIP protocols. It may represent a device that interfaces with a legacy PBX, an IP PBX, or Microsoft Lync Server.

<!-- end list -->

  - welcome greeting  
    A greeting that is played when an external caller calls in to a UM auto attendant or when an Outlook Voice Access user or another caller calls a subscriber access number that is configured on a UM dial plan. The default welcome greetings can be changed by a customer to make them specific to an organization or location.

