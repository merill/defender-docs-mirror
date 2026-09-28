---
layout: Conceptual
title: Connect Microsoft Sentinel to Azure, Windows, and Microsoft services | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-azure-windows-microsoft-services
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
description: Learn how to connect Microsoft Sentinel to Azure and Microsoft 365 cloud services and to Windows Server event logs.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: overview
ms.date: 2023-02-24T00:00:00.0000000Z
locale: en-us
document_id: a98f3ade-b0c8-bf74-a474-6f5a8606a2f6
document_version_independent_id: 00dcc529-9eb9-ed9f-3fa8-758163b665e0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-azure-windows-microsoft-services.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-azure-windows-microsoft-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-azure-windows-microsoft-services.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 01cf59a1-947d-6baf-8584-2f49494b3a89
---

# Connect Microsoft Sentinel to Azure, Windows, and Microsoft services | Microsoft Learn

Microsoft Sentinel uses the Azure foundation to provide built-in, service-to-service support for data ingestion from many Azure and Microsoft 365 services, Amazon Web Services, and various Windows Server services. There are a few different methods through which these connections are made.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

## Types of connections

Data connectors for Microsoft Sentinel are grouped into the following types of connectors:

- **API-based** connections
- **Diagnostic settings** connections, some of which are managed by Azure Policy
- **Windows agent**-based connections

See the [data connector reference](data-connectors-reference) to find available data connectors and their related information page. You'll find information that's unique to each connector like Log Analytics tables for data storage and a link to the installation instructions.

The following articles present information that is common to each group of connectors for Microsoft services.

- [API-based data connections](connect-services-api-based)
- [Diagnostic settings-based data connections](connect-services-diagnostic-setting-based)
- [Windows agent-based connections](connect-services-windows-based)

The following integrations are both more unique and popular, and are treated individually, with their own articles:

- [Amazon Web Services (AWS) CloudTrail](connect-aws)
- [Microsoft Entra ID](connect-azure-active-directory)
- [Azure Virtual Desktop](connect-azure-virtual-desktop)
- [Microsoft Defender XDR](connect-microsoft-365-defender)
- [Microsoft Defender for Cloud](connect-defender-for-cloud)
- [Microsoft Purview Information Protection](connect-microsoft-purview)
- [Windows DNS](connect-dns-ama)
- [Windows Security Events](connect-windows-security-events)