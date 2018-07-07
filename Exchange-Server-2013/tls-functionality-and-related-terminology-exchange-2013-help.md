---
title: 'TLS functionality and related terminology: Exchange 2013 Help'
TOCTitle: TLS functionality and related terminology
ms:assetid: 294ba2a9-892d-4a90-beec-9d298426b5f4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Bb430753(v=EXCHG.150)
ms:contentKeyID: 50934214
ms.date: 06/02/2016
mtps_version: v=EXCHG.150
---

# TLS functionality and related terminology

 

_**Applies to:** Exchange Online, Exchange Server 2013_


Microsoft Exchange Server 2013 provides administrative functionality and other enhancements that improve the overall management of Transport Layer Security (TLS). As you work with this functionality, you need to learn about some TLS-related features and functionality. Some terms and concepts apply to more than one TLS-related feature. In this topic, a brief explanation of each feature is provided, which is intended to help you understand some differences and general terminology related to TLS and the Domain Security feature set:

  - **Transport Layer Security   **TLS is a standard protocol that's used to provide secure Web communications on the Internet or intranets. It enables clients to authenticate servers or, optionally, servers to authenticate clients. It also provides a secure channel by encrypting communications. TLS is the latest version of the Secure Sockets Layer (SSL) protocol.

  - **Mutual TLS**   Mutual TLS authentication differs from TLS as TLS is usually deployed. Typically, when TLS is deployed, it's used only to provide confidentiality in the form of encryption. No authentication occurs between the sender and receiver. Additionally, sometimes when TLS is deployed, only the receiving server is authenticated. This deployment of TLS is typical of the HTTP implementation of TLS. This implementation, where only the receiving server is authenticated, is SSL.
    
    With mutual TLS authentication, each server verifies the identity of the other server by validating a certificate that's provided by that other server. In this scenario, where messages are received from external domains over verified connections in an Exchange 2013 environment, Microsoft Outlook displays a **Domain Secured** icon.

  - **Domain Security**   Domain Security is the set of features, such as certificate management, connector functionality, and Outlook client behavior that enables mutual TLS as a manageable and useful technology. Domain Security isn't supported when outbound email is routed through an Exchange 2013 Client Access server.

  - **Opportunistic TLS**   In Exchange 2013, Setup creates a self-signed certificate. By default, TLS is enabled. This enables any sending system to encrypt the inbound SMTP session to Exchange. By default, Exchange 2013 also attempts TLS for all remote connections.

  - **Direct trust**   By default, all traffic between Edge Transport servers and Mailbox servers is authenticated and encrypted. Again, the underlying mechanism for authentication and encryption is mutual TLS. Instead of using X.509 validation, Exchange 2013 uses direct trust to authenticate the certificates. Direct trust means that the presence of the certificate in Active Directory or Active Directory Lightweight Directory Services (AD LDS) validates the certificate. Active Directory is considered a trusted storage mechanism. When direct trust is used, it doesn't matter if the certificate is self-signed or signed by a certification authority. When you subscribe an Edge Transport server to the Exchange organization, the Edge Subscription publishes the Edge Transport server certificate in Active Directory for the Mailbox servers to validate. The Microsoft Exchange EdgeSync service updates AD LDS with the set of Mailbox server certificates for the Edge Transport server to validate.

