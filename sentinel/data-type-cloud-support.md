---
layout: Conceptual
title: Support for Microsoft Sentinel connector data types in different clouds | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/data-type-cloud-support
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
description: This article describes the types of clouds that affect data streaming from the different connectors that Microsoft Sentinel supports.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: concept-article
ms.date: 2024-06-09T00:00:00.0000000Z
locale: en-us
document_id: f0edee52-b33a-62ca-dfe3-bb64f1efb3f8
document_version_independent_id: 5c1aad48-9d87-85b9-19fd-c02c1722792b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/data-type-cloud-support.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/data-type-cloud-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/data-type-cloud-support.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: ca583d7e-9c78-b3c7-02bd-c7fa6be66460
---

# Support for Microsoft Sentinel connector data types in different clouds | Microsoft Learn

Microsoft Sentinel data connectors use data stored in various cloud environments, like the Microsoft 365 Commercial cloud or the Government Community Cloud (GCC).

This article describes the types of clouds that affect the supported data types for the different connectors that Microsoft Sentinel supports. Specifically, support varies for different Microsoft Defender XDR connector data types in different GCC environments.

## Microsoft cloud types

| Name | Also named | Description | Learn more |
| --- | --- | --- | --- |
| Azure Commercial | Azure, Azure Public | The standard Microsoft cloud. Most of the enterprises in the private market, academic institutions and home Office 365 tenants reside in a Commercial environment.Different tools help meet the Microsoft 365 Commercial compliance and security needs. For example: Intune, Microsoft Purview compliance portal, Microsoft Purview Information Protection, and more. | [Microsoft 365 integration](/en-us/azure/security/fundamentals/feature-availability#microsoft-365-integration) |
| Government Community Cloud (GCC) | GCC-M, GCC Moderate | A government-focused copy of Microsoft 365 Commercial environment. While GCC contains similar features to the Microsoft 365 Commercial environment, GCC is subject to the FedRAMP Moderate policy. | [Government Community Cloud](/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc) |
| Department of Defense (DoD) |  | Originally created for internal use by the Department of Defense. DoD is the only environment that meets DoD SRG levels 5 and 6. Other clouds described in this article don't support these SRG levels. | [GCC High and DoD](/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc-high-and-dod) |
| GCC-High | GCC High | Technically, GCC High is a copy of a DoD environment, but GCC High exists in its own sovereign environment.GCC High (and above) stores the data in Azure Government, so it is physically segregated from the commercial services. | [GCC High and DoD](/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc-high-and-dod) |

## Microsoft clouds and Microsoft Sentinel

Microsoft Sentinel is built on Microsoft Azure environments—both commercial and government. Office 365 environments, like GCC, GCC-High and DoD, interface at different levels with Azure environments.

This diagram shows the hierarchy of the Office 365 and Microsoft Azure clouds and how they relate to each other and to Microsoft Sentinel.

[![Diagram showing how the Microsoft cloud architecture relates to Microsoft Sentinel data.](media/data-type-cloud-support/cloud-architecture-microsoft-sentinel.png)](media/data-type-cloud-support/cloud-architecture-microsoft-sentinel.png#lightbox)

Because of this complexity, different types of data streaming into Microsoft Sentinel may or may not be fully supported.

## How cloud support affects data from Microsoft Defender XDR connectors

Your environment ingests data from multiple connectors. The type of cloud you use affects Microsoft Sentinel's ability to ingest and display data from these connectors, like logs, alerts, device events, and more.

We have identified support discrepancies between the different clouds for the data streaming from these connectors:

- Microsoft Defender for Endpoint
- Microsoft Defender for Office 365
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps
- Microsoft Entra ID Protection

Read more about [support for Microsoft Defender 365 connector data types in different clouds](microsoft-365-defender-cloud-support).