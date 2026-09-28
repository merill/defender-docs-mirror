---
layout: Conceptual
title: Support for Microsoft Defender XDR connector data types in Microsoft Sentinel for different clouds (GCC environments) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/microsoft-365-defender-cloud-support
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
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
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: This article describes support for different Microsoft Defender XDR connector data types in Microsoft Sentinel across different clouds, including Commercial, GCC, GCC-High, and DoD.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: reference
ms.date: 2023-02-01T00:00:00.0000000Z
locale: en-us
document_id: b97ca925-b842-1f72-0508-6ebe3e544826
document_version_independent_id: 6e1518eb-ec72-20c4-f8da-0994420ab964
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/microsoft-365-defender-cloud-support.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/microsoft-365-defender-cloud-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/microsoft-365-defender-cloud-support.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 6d6ddf3d-c265-a486-a3cc-ceaea9947962
---

# Support for Microsoft Defender XDR connector data types in Microsoft Sentinel for different clouds (GCC environments) | Microsoft Learn

The type of cloud your environment uses affects Microsoft Sentinel's ability to ingest and display data from these connectors, like logs, alerts, device events, and more. This article describes support for different Microsoft Defender XDR connector data types in Microsoft Sentinel across different clouds, including Commercial, GCC, GCC-High, and DoD.

Read more about [data type support for different clouds in Microsoft Sentinel](data-type-cloud-support).

## Connector data

### Incidents

| Data type | Commercial / GCC(Azure Commercial) | GCC-High / DoD(Azure Government) |
| --- | --- | --- |
| **Incidents** | Generally available | Generally available |

### Alerts

#### From Microsoft Defender XDR

| Data type | Commercial / GCC(Azure Commercial) | GCC-High / DoD(Azure Government) |
| --- | --- | --- |
| **Microsoft Defender XDR alerts: *SecurityAlert*** | Generally available | Public preview |

#### From standalone component connectors

| Data type | Commercial | GCC | GCC-High / DoD |
| --- | --- | --- | --- |
| **Microsoft Defender for Endpoint: *SecurityAlert (MDATP)*** | Generally available | Generally available | Generally available |
| **Microsoft Defender for Office 365: *SecurityAlert (OATP)*** | Public preview | Public preview | Public preview |
| **Microsoft Defender for Identity: *SecurityAlert (AATP)*** | Generally available | Generally available | Unsupported |
| **Microsoft Defender for Cloud Apps: *SecurityAlert (MCAS)*** | Generally available | Generally available | Unsupported |
| **Microsoft Defender for Cloud Apps: *McasShadowItReporting*** | Generally available | Generally available | Unsupported |

## Raw event data

### Microsoft Defender for Endpoint

| Data type | Commercial / GCC(Azure Commercial) | GCC-High / DoD(Azure Government) |
| --- | --- | --- |
| **DeviceInfo** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceNetworkInfo** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceProcessEvents** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceNetworkEvents** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceFileEvents** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceRegistryEvents** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceLogonEvents** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceImageLoadEvents** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceEvents** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |
| **DeviceFileCertificateInfo** | Generally available | Microsoft Defender XDR: Generally availableMicrosoft Sentinel: Public preview |

### Microsoft Defender for Identity

| Data type | Commercial / GCC(Azure Commercial) | GCC-High / DoD(Azure Government) |
| --- | --- | --- |
| **IdentityDirectoryEvents** | Generally available | Unsupported |
| **IdentityLogonEvents** | Generally available | Unsupported |
| **IdentityQueryEvents** | Generally available | Unsupported |

### Microsoft Defender for Cloud Apps

| Data type | Commercial / GCC(Azure Commercial) | GCC-High / DoD(Azure Government) |
| --- | --- | --- |
| **CloudAppEvents** | Generally available | Unsupported |

### Microsoft Defender for Office 365

| Data type | Commercial / GCC(Azure Commercial) | GCC-High / DoD(Azure Government) |
| --- | --- | --- |
| **EmailEvents** | Generally available | Public preview |
| **EmailAttachmentInfo** | Generally available | Public preview |
| **EmailUrlInfo** | Generally available | Public preview |
| **EmailPostDeliveryEvents** | Generally available | Public preview |
| **UrlClickEvents** | Generally available | Public preview |

### Alerts

| Data type | Commercial / GCC(Azure Commercial) | GCC-High / DoD(Azure Government) |
| --- | --- | --- |
| **AlertInfo** | Generally available | Public preview |
| **AlertEvidence** | Generally available | Public preview |