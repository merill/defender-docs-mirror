---
layout: Conceptual
title: SSL/TLS certificate file requirements - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/best-practices/certificate-requirements
breadcrumb_path: ../../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Learn about requirements for SSL/TLS certificates used with Microsoft Defender for IOT OT sensors.
ms.date: 2023-01-17T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: 02bee75d-83ef-0468-d0f6-9d69e6ac137c
document_version_independent_id: 80027d3b-1324-ff65-2a73-589f6e91c617
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/best-practices/certificate-requirements.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/best-practices/certificate-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/best-practices/certificate-requirements.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 7c436ce3-2582-ba4e-1ebc-f72ad50b9c26
---

# SSL/TLS certificate file requirements - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

Use the content below to learn about the requirements for [creating SSL/TLS certificates](../ot-deploy/create-ssl-certificates) for use with Microsoft Defender for IoT appliances.

[![Diagram of a progress bar with Plan and prepare highlighted.](../media/deployment-paths/progress-plan-and-prepare.png)](../media/deployment-paths/progress-plan-and-prepare.png#lightbox)

Defender for IoT uses SSL/TLS certificates to secure communication between the following system components:

- Between users and the OT sensor
- Between an OT sensor and a high availability (HA) server, if configured
- Between OT sensors and partners servers defined in [alert forwarding rules](../how-to-forward-alert-information-to-partners)

Some organizations also validate their certificates against a Certificate Revocation List (CRL) and the certificate expiration date, and the certificate trust chain. Invalid certificates can't be uploaded to OT sensors, and will block encrypted communication between Defender for IoT components.

Important

You must create a unique certificate for each OT sensor, and high availability server, where each certificate meets required criteria.

## Supported file types

When preparing SSL/TLS certificates for use with Microsoft Defender for IoT, make sure to create the following file types:

| File type | Description |
| --- | --- |
| **.crt – certificate container file** | A `.pem`, or `.der` file, with a different extension for support in Windows Explorer. |
| **.key – Private key file** | A key file is in the same format as a `.pem` file, with a different extension for support in Windows Explorer. |
| **.pem – certificate container file (optional)** | Optional. A text file with a Base64-encoding of the certificate text, and a plain-text header and footer to mark the beginning and end of the certificate. |

## CRT file requirements

Make sure that your certificates include the following CRT parameter details:

| Field | Requirement |
| --- | --- |
| **Signature Algorithm** | SHA256RSA |
| **Signature Hash Algorithm** | SHA256 |
| **Valid from** | A valid past date |
| **Valid To** | A valid future date |
| **Public Key** | RSA 2048 bits (Minimum) or 4096 bits |
| **CRL Distribution Point** | URL to a CRL server. If your organization doesn't [validate certificates against a CRL server](../ot-deploy/create-ssl-certificates#verify-crl-server-access), remove this line from the certificate. |
| **Subject CN (Common Name)** | domain name of the appliance, such as *sensor.contoso.com*, or *.contosocom* |
| **Subject (C)ountry** | Certificate country code, such as `US` |
| **Subject (OU) Org Unit** | The organization's unit name, such as *Contoso Labs* |
| **Subject (O)rganization** | The organization's name, such as *Contoso Inc.* |

Important

While certificates with other parameters might work, they aren't supported by Defender for IoT. Additionally, wildcard SSL certificates, which are public key certificates that can be used on multiple subdomains such as *.contoso.com*, are insecure and aren't supported. Each appliance must use a unique CN.

## Key file requirements

Make sure that your certificate key files use either RSA 2048 bits or 4096 bits. Using a key length of 4096 bits slows down the SSL handshake at the start of each connection, and increases the CPU usage during handshakes.

### Supported characters for keys and passphrases

The following characters are supported for creating a key or certificate with a passphrase:

- ASCII characters, including **a-z**, **A-Z**, **0-9**
- The following special characters: **! # % ( ) + , - . / : = ? @ [ \ ] ^ \_ { } ~**