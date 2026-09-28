---
layout: Conceptual
title: US Government offerings - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/us-govt-gcc-high
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: This article provides an overview of Microsoft Defender for Identity's US Government offerings.
ms.date: 2023-02-14T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: martin77s
locale: en-us
document_id: 6383a76f-2715-513f-0db3-6d77e2d34e08
document_version_independent_id: 6383a76f-2715-513f-0db3-6d77e2d34e08
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/us-govt-gcc-high.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: us-govt-gcc-high
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/us-govt-gcc-high.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 4036977b-ce98-39d9-f5c8-062cc5fe79f3
---

# US Government offerings - Microsoft Defender for Identity | Microsoft Learn

The Microsoft Defender for Identity GCC High offering uses the same underlying technologies and capabilities as the commercial workspace for Defender for Identity.

## Get started with US Government offerings

The Defender for Identity GCC, GCC High, and Department of Defense (DoD) offerings are built on the Microsoft Azure Government Cloud and are designed to inter-operate with Microsoft 365 GCC, GCC High, and DoD. Use Defender for Identity public documentation as a [starting point](deploy-defender-identity) for deploying and operating the service.

## Licensing requirements

Defender for Identity for US Government customers requires one of the following Microsoft volume licensing offers:

| **GCC** | **GCC High** | **DoD** |
| --- | --- | --- |
| Microsoft 365 GCC G5 | Microsoft 365 E5 for GCC High | Microsoft 365 G5 for DOD |
| Microsoft 365 G5 Security GCC | Microsoft 365 G5 Security for GCC High | Microsoft 365 G5 Security for DOD |
| Standalone Defender for Identity licenses | Standalone Defender for Identity licenses | Standalone Defender for Identity licenses |

## URLs

To access Microsoft Defender for Identity for US Government offerings, use the appropriate addresses in this table:

| US Government offering | Microsoft Defender portal | Sensor (agent) endpoint |
| --- | --- | --- |
| DoD | `security.microsoft.us` | `<your-workspace-name>sensorapi.atp.azure.us` |
| GCC-H | `security.microsoft.us` | `<your-workspace-name>sensorapi.atp.azure.us` |
| GCC | `security.microsoft.com` | `<your-workspace-name>sensorapi.atp.gcc.azure.com` |

You can also use the IP address ranges in our Azure service tag (**AzureAdvancedThreatProtection**) to enable access to Defender for Identity. For more information about service tags, see [Virtual network service tags](/en-us/azure/virtual-network/service-tags-overview) or download [the Azure IP Ranges and Service Tags – US Government Cloud file](https://www.microsoft.com/download/details.aspx?id=57063).

## Required connectivity settings

Use [this link](prerequisites#required-ports) to configure the minimum internal ports necessary that the Defender for Identity sensor requires.

## How to migrate from commercial to GCC

Note

The following steps should only be taken after you have initiated the transition of Microsoft Defender for Endpoint and Microsoft Defender for Cloud Apps

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to the Settings -&gt; Identities section to create a new workspace for Defender for Identity
2. Configure a Directory Service account
3. Download the new sensor agent package and copy the workspace key
4. Make sure sensors have access to \*.atp.gcc.azure.com (directly or through proxy)
5. Uninstall existing sensor agents from the domain controllers, AD FS servers, AD CS servers and Entra Connect servers.
6. [Reinstall sensors with the new workspace](deploy-defender-identity)
7. Migrate any settings after the initial sync (use the https://transition.security.microsoft.com portal in a separate browser session to compare)
8. Eventually, delete the previous workspace (historical data will be lost)

Note

No data is migrated from the commercial service.

## Feature parity with the commercial environment

Unless otherwise specified, new feature releases, including preview features, documented in [What's new with Defender for Identity](whats-new), will be available in GCC, GCC High, and DoD environments within 90 days of release in the Defender for Identity commercial environment. Preview features may not be supported in the GCC, GCC High, and DoD environments.