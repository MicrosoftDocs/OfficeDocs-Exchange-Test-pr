---
title: 'Voice mail preview enhancements: Exchange 2013 Help'
TOCTitle: Voice mail preview enhancements
ms:assetid: 1fcccec1-4edc-40b8-948c-111647d7d770
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ150501(v=EXCHG.150)
ms:contentKeyID: 47559971
ms.date: 05/13/2016
mtps_version: v=EXCHG.150
---

# Voice mail preview enhancements

 

_**Applies to:** Exchange Server 2013_


Voice Mail Preview is a feature that's available to users who receive their voice mail messages using Microsoft Exchange Server 2010 or Exchange Server 2013 Unified Messaging (UM). Voice Mail Preview enhances UM voice mail functionality by providing a text version of audio recordings. The voice mail text is displayed in an email message within Microsoft Office Outlook Web App, Outlook 2010, and other email programs.

## Voice Mail Preview enhancements

In Exchange 2013, UM includes several enhancements to the user interface for Outlook Web App and Outlook clients and improvements to increase confidence and accuracy for Voice Mail Preview. Also, some enhancements to the speech-related services are offered through the Microsoft Speech Platform (Version 11.0) and Unified Communications Managed API (UCMA) 4.0 to enhance grammar generation and language support.

Unified Messaging introduced the Voice Mail Preview feature in Exchange 2010. Voice Mail Preview uses automatic speech recognition (ASR) to add a text version of a voice mail audio file to a voice message. ASR isn't entirely accurate, especially when it's used to record audio over a phone that includes unknown voices and noises.

Some organizations require consistently error-free or near-error-free transcripts of voice mail messages for some, if not all, of their users. The Voice Mail Preview Partner Program helps such organizations meet those requirements. The Voice Mail Preview Partner Program was designed for Exchange 2010 to improve Voice Mail Preview results, but it wasn’t used by Exchange 2010 customers because of the overhead and cost. To address these issues, Exchange 2013 includes the following enhancements for Voice Mail Preview:

  - **Improved audio normalization**   Audio normalization is the process of uniformly increasing (or decreasing) the amplitude of an entire audio signal so that the resulting peak amplitude matches a specified target or the norm. UM normalizes the audio recording before compressing it and sending to the user.

  - **Enhanced speech recognition**   By collecting voice mail messages (only if the Exchange customer chooses to share this information), the results of the voice mail previews can be used to add words and phrases to the speech engine. This is done by setting the *VoiceMailAnalysisEnabled* parameter to `$true` using the **Set-UMMailbox** cmdlet or by setting the *AllowVoiceMailAnalysis* parameter to `$true` on the **Set-UMMailboxPolicy** cmdlet. Also, Exchange 2013 UM uses information more efficiently from email threads created by a user using Outlook Voice Access. This includes information about the participant’s (Active Directory or personal contact) information (country, city, company), and the phone number of the Outlook Voice Access user.

  - **Voice Mail Preview confidence**   The confidence score is the number assigned by Unified Messaging that is directly related to the overall accuracy of the transcription. The confidence calculations that are used by UM have been adjusted to be more accurate and represent the actual accuracy of a transcribed message.

  - **Filtering** Offensive words are detected and filtered and the results are cached and stored in the user’s mailbox.

  - **Hiding the text preview**   If the confidence score of a voice mail preview is below a given threshold, the Voice Mail Preview text will be hidden. If the text is hidden, the voice message will include text stating that the confidence of the voice mail was too low for results to be displayed.

  - **Transcription performance**   Voice Mail Preview is a CPU-intensive operation that requires roughly twice the time it takes to process an audio file. If generating the voice mail preview text takes too long, CPU throttling stops processing the preview. In Exchange 2010, UM didn’t try to transcribe any voice message that was longer than 75 seconds. In Exchange 2013, the entire voice message is transcribed, but the text for the message isn't included if it extends past 75 seconds.

  - **Color schemes**   Because of the confusion over the colors that were used to distinguish between low, medium, and high confidence for a voice mail preview, the color scheme has been removed in Exchange 2013 for Outlook Web App and Outlook.

