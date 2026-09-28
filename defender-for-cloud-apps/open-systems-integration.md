---
layout: Conceptual
title: Integrate with Open Systems - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/open-systems-integration
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes how to integrate Microsoft Defender for Cloud Apps with Open Systems for seamless cloud discovery and automated block of unsanctioned apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7f626844-8147-af51-e8e2-503c85bab636
document_version_independent_id: 7f626844-8147-af51-e8e2-503c85bab636
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/open-systems-integration.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: open-systems-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/open-systems-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: b1d2be73-79c7-e558-6258-fd7434e50540
---

# Integrate with Open Systems - Microsoft Defender for Cloud Apps | Microsoft Learn

If you work with both Defender for Cloud Apps and Open Systems, you can integrate the two products to enhance your security cloud discovery experience. Open Systems, as a standalone Secure Web Gateway, monitors your organization's traffic enabling you to set policies for blocking transactions. Together, Defender for Cloud Apps and Open Systems provide the following capabilities:

- Seamless deployment of cloud discovery - Use Open Systems to proxy your traffic and send it to Defender for Cloud Apps. This eliminates the need for installation of log collectors on your network endpoints to enable cloud discovery.
- Open Systems' block capabilities are automatically applied on apps you set as unsanctioned in Defender for Cloud Apps.

## Prerequisites

Before you begin, make sure you have the following licenses:

- A valid license for Microsoft Defender for Cloud Apps
- A valid license for Open Systems Secure Web Gateway

## Deployment

To deploy the integration between Defender for Cloud Apps and Open Systems, follow these steps:

1. Contact your Technical Account Manager in Open Systems to get the *Microsoft Cloud App Security with Secure Web Gateway Configuration Guide* to integrate the products.
2. Investigate cloud apps discovered on your network. For more information and investigation steps, see [Working with cloud discovery](working-with-cloud-discovery-data).
3. Any app that you set as unsanctioned in Defender for Cloud Apps will be retrieved by Open Systems, and then automatically blocked. It can take up to one hour for the app to be blocked on the Open Systems Secure Web Gateway. If you need the app to be blocked immediately after tagging it as **Unsanctioned**, contact Open Systems customer support. For more information about unsanctioning apps, see [Sanctioning/unsanctioning an app](governance-discovery#sanctioningunsanctioning-an-app).