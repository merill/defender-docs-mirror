---
layout: Conceptual
title: Overview of data connectors in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/overview-data-connectors
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn about connecting data sources in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2025-09-21T00:00:00.0000000Z
locale: en-us
document_id: b8d87e48-fd56-22a2-4c1c-486796c6935c
document_version_independent_id: b8d87e48-fd56-22a2-4c1c-486796c6935c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/overview-data-connectors.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: overview-data-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/overview-data-connectors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: cc185686-ab30-a597-6b9e-7f12e294dfed
---

# Overview of data connectors in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

[Microsoft Security Exposure Management](microsoft-security-exposure-management) consolidates security posture data from all your digital assets across endpoints, cloud environments, operational technology (OT) environments, and external attack surfaces, enabling you to map your attack surface and focus your security efforts on areas at greatest risk. Data from Microsoft Security products like Microsoft Defender for Endpoint, Microsoft Defender for Identity, Microsoft Defender for Cloud (including Azure, AWS, and GCP), Microsoft Entra ID, and others are automatically ingested and consolidated within Exposure Management in the unified portal. You can further enrich and extend this data by connecting to a range of external data sources through Exposure Management data connectors.

To provide coverage of your assets and security signals and to help you establish a comprehensive, single source of truth for your assets, Exposure Management provides data connectors. These connectors ingest data from third-party security tools, including CMDB tools such as ServiceNow, vulnerability management tools such as Tenable, Qualys, and Rapid7, cloud security tools such as Wiz and Palo Alto Prisma, and OT tools such as Armis, Dragos, and Forescout.

These third-party vulnerability management connectors also replace the 'bring your own license' scanners previously available in Microsoft Defender for Cloud in Azure, but they offer significantly more capabilities beyond just that functionality.

Benefits include:

- **Unified visibility**: Previously siloed vulnerabilities and asset information from external sources now appear in the unified Defender portal's Exposure Management inventory
- **Normalized within exposure graph**: All external data is integrated into the enterprise exposure graph and can be explored in the Attack Surface Map for comprehensive analysis
- **Enhanced device inventory**: Enriches the unified inventory with assets and findings from third-party tools
- **Improved critical asset identification**: Asset criticality signals discovered via connectors can be used to automatically apply criticality tags in Exposure Management
- **Mapping relationships**: Creates connections between external assets and existing infrastructure
- **Revealing new attack paths**: Enables discovery of attack paths that include external assets and vulnerabilities
- **Comprehensive attack surface visibility**: Provides end-to-end visibility across Microsoft and third-party security tools
- **Enriched context**: Incorporates asset criticality and business application context from external sources
- **Advanced analytics**: External data can be explored using advanced hunting queries via KQL in the unified experience

The support for external solutions helps to further streamline, integrate, and orchestrate defenses from other security vendors with Exposure Management. This enables security teams to effectively manage their posture and exposure across the entire attack surface.

[![Screenshot of data connectors available in MSEM](media/connect-data-sources/data-connectors.png)](media/connect-data-sources/data-connectors.png#lightbox)

OT data connectors are available in the unified connector catalog in the Microsoft Defender portal. OT connectors use a dedicated setup flow under **System** &gt; **Data management** &gt; **Data connectors**.

[![Screenshot of OT data connectors in the unified connector catalog.](media/connect-data-sources/ot-data-connectors.png)](media/connect-data-sources/ot-data-connectors.png#lightbox)

Data Connectors in Microsoft Security Exposure Management is currently in preview.

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Note

During the preview phase, use of the data connectors feature is free. Once data connectors become generally available, there will be a consumption-based charge based on data ingested from each third party product. Pricing will be announced before billing of external connectors starts at GA.