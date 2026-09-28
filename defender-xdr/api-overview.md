---
layout: Conceptual
title: Overview of Microsoft Defender XDR APIs - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the available APIs in Microsoft Defender XDR
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-04-18T00:00:00.0000000Z
locale: en-us
document_id: e9ff0b96-564d-dc57-356d-91baae65be47
document_version_independent_id: e9ff0b96-564d-dc57-356d-91baae65be47
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: cf680780-fda1-5d47-c8dc-5a9ec5114d22
---

# Overview of Microsoft Defender XDR APIs - Microsoft Defender XDR | Microsoft Learn

Note

The **Microsoft Graph security API** is a unified schema and interface that integrates with various Microsoft security solutions and Microsoft security partners. To get started, see [Use the Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview).

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Microsoft Defender is built on top of an integration-ready platform.

Use the Microsoft Defender APIs to automate workflows based on the shared incident and advanced hunting tables.

- **[Combined incidents queue](api-incident)** - Focus on what's critical by grouping the full attack scope and all impacted assets together under the incident API.
- **[Cross-product threat hunting](api-advanced-hunting)** - Leverage your security team's organizational knowledge to hunt for signs of compromise, by creating your own custom queries to sift over raw data collected from multiple protection products.
- **[Event streaming API](streaming-api)** - Ship real-time events and alerts in a single data stream as they occur.

Along with these Microsoft Defender-specific APIs, each of our other security products expose [additional APIs](api-articles) to help you take advantage of their unique capabilities.

Note

The transition to the unified portal should not affect the PowerBi dashboards based on Microsoft Defender for Endpoint APIs. You can continue to work with the existing APIs regardless of the interactive portal transition.

Watch this short video to learn how you can use Microsoft Defender XDR to automate workflows and integrate apps.

## Learn more

| **Understand how to access the APIs** |
| --- |
| [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview) |
| [Learn about API quotas and licensing](/en-us/legal/microsoft-365/api-terms) |
| [Access the Microsoft Defender XDR APIs](api-access) |
| **Build apps** |
| [Create a 'Hello world' app](api-hello-world) |
| [Create an app to access Microsoft Defender APIs on behalf of a user](api-create-app-user-context) |
| [Create an app to access Microsoft Defender without a user](api-create-app-web) |
| [Create an app with multi-tenant partner access to Microsoft Defender APIs](api-partner-access) |
| **Troubleshoot and maintain your apps** |
| [Understand API error codes](api-error-codes) |
| [Manage secrets in your apps with Azure Key Vault](/en-us/training/modules/manage-secrets-with-azure-key-vault/) |
| [Implement OAuth 2.0 authorization for user sign in](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-code) |

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).