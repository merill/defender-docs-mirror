---
layout: Conceptual
title: Microsoft Defender XDR for US Government - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/usgov
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about Microsoft Defender XDR for US Government requirements and capabilities available
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security-compliance
- tier3
ms.topic: article
ms.date: 2021-12-07T00:00:00.0000000Z
locale: en-us
document_id: 2ae454c4-ff41-e1c4-11fa-01e158fcb105
document_version_independent_id: 2ae454c4-ff41-e1c4-11fa-01e158fcb105
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/usgov.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: usgov
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/usgov.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 943a311a-06b6-4d45-e043-e3f798a638a5
---

# Microsoft Defender XDR for US Government - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR

Microsoft Defender for US Government customers, built in the Azure US Government environment, uses the same underlying technologies as Microsoft Defender in Azure Commercial.

This offering is available to GCC, GCC High, and DoD customers and is based on the same prevention, detection, investigation, and remediation as the commercial version. However, there are some differences in the availability of capabilities for this offering.

Note

If you are a GCC customer using Defender for Cloud Apps, Defender for Endpoint, or Defender for Identity in Commercial, you need to transition those services to their GCC versions to be eligible for Microsoft Defender GCC.

## Licensing requirements

Microsoft Defender for US Government customers requires one of the following Microsoft volume licensing offers:

### Desktop licensing

| GCC | GCC High | DoD |
| --- | --- | --- |
| Microsoft 365 GCC G5 | Microsoft 365 E5 for GCC High | Microsoft 365 G5 for DOD |
| Microsoft 365 G5 Security GCC | Microsoft 365 G5 Security for GCC High | Microsoft 365 G5 Security for DOD |
| Enterprise Mobility + Security G5 GCC | Enterprise Mobility + Security E5 for GCC High | Enterprise Mobility + Security E5 for DOD |
| Office 365 G5 GCC | Office 365 E5 for GCC High | Office 365 E5 for DOD |
| Microsoft Defender for Cloud Apps GCC | Microsoft Defender for Cloud Apps for GCC High | Microsoft Defender for Cloud Apps for DOD |
| Microsoft Defender for Endpoint - GCC | Microsoft Defender for Endpoint for GCC High | Microsoft Defender for Endpoint for DOD |
| Microsoft Defender for Identity - GCC | Microsoft Defender for Identity for GCC High | Microsoft Defender for Identity for DOD |
| Microsoft Defender for Office 365 (Plan 2) GCC | Microsoft Defender for Office 365 (Plan 2) for GCC High | Microsoft Defender for Office 365 (Plan 2) for DOD |
| Windows 10 Enterprise E5 GCC | Windows 10 Enterprise E5 for GCC High | Windows 10 Enterprise E5 for DOD |

### Server licensing

| GCC | GCC High | DoD |
| --- | --- | --- |
| Microsoft Defender for Endpoint Server GCC | Microsoft Defender for Endpoint Server for GCC High | Microsoft Defender for Endpoint Server for DOD |
| Microsoft Defender for servers | Microsoft Defender for servers - Government | Microsoft Defender for servers - Government |

## Portal URLs

The following are the Microsoft Defender portal URLs for US Government customers:

| Customer type | Portal URL |
| --- | --- |
| GCC | https://security.microsoft.com |
| GCC High | https://security.microsoft.us |
| DoD | https://security.apps.mil |

Note

If you are a GCC customer and in the process of moving from Microsoft Defender for Endpoint commercial to GCC, use https://transition.security.microsoft.com to access your Microsoft Defender for Endpoint commercial data.

## API

Instead of the public URIs listed in our [API documentation](api-overview), you'll need to use the following URIs:

| Endpoint type | GCC | GCC High & DoD |
| --- | --- | --- |
| Login | `https://login.microsoftonline.com` | `https://login.microsoftonline.us` |
| Microsoft Defender XDR API | `https://api-gcc.security.microsoft.us` | `https://api-gov.security.microsoft.us` |

## Feature parity with commercial

Microsoft Defender for US Government customers doesn't have complete parity with the commercial offering. While our goal is to deliver all commercial features and functionality to our US Government customers, there are some capabilities not yet available we want to highlight.

These are the known gaps:

| Feature name | GCC | GCC High | DoD |
| --- | --- | --- | --- |
| Microsoft Threat Experts | ![No](/en-us/defender-endpoint/media/svg/check-no.svg) On engineering backlog | ![No](/en-us/defender-endpoint/media/svg/check-no.svg) On engineering backlog | ![No](/en-us/defender-endpoint/media/svg/check-no.svg) On engineering backlog |
| Microsoft Defender for IoT enterprise IoT security | ![No](/en-us/defender-endpoint/media/svg/check-no.svg) | ![No](/en-us/defender-endpoint/media/svg/check-no.svg) | ![No](/en-us/defender-endpoint/media/svg/check-no.svg) |

For detailed list of Event Streaming API tables, see [Microsoft Defender streaming event types supported in Event Streaming API](supported-event-types).

## More details

For more information, see the individual workloads US Gov pages:

- [Microsoft Defender for Cloud Apps](/en-us/enterprise-mobility-security/solutions/ems-cloud-app-security-govt-service-description).
- [Microsoft Defender for Identity](/en-us/enterprise-mobility-security/solutions/ems-mdi-govt-service-description).
- [Microsoft Defender for Endpoint](/en-us/defender-endpoint/gov).

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).