---
layout: Conceptual
title: Integrate with Menlo Security - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/menlo-integration
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
description: This article describes how to integrate Microsoft Defender for Cloud Apps with Menlo Security for seamless cloud discovery and automated block of unsanctioned apps.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
locale: en-us
document_id: 3cda12a9-bf16-16bf-8398-e49835df2708
document_version_independent_id: 3cda12a9-bf16-16bf-8398-e49835df2708
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/menlo-integration.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: menlo-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/menlo-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: dabbac8f-27b0-ecfc-3e65-466250e15b5e
---

# Integrate with Menlo Security - Microsoft Defender for Cloud Apps | Microsoft Learn

If you work with both Defender for Cloud Apps and Menlo Security, you can integrate the two products to enhance your security cloud discovery experience. Menlo Security, as a standalone Secure Web Gateway, monitors your organization's traffic enabling you to set policies for blocking transactions. Together, Defender for Cloud Apps and Menlo Security provide the following capabilities:

- Seamless deployment of cloud discovery - Use Menlo Security to proxy your traffic and send it to Defender for Cloud Apps. This eliminates the need for installation of log collectors on your network endpoints to enable cloud discovery.
- Menlo Security's block capabilities are automatically applied on apps you set as unsanctioned in Defender for Cloud Apps.

## Prerequisites

- A valid license for Microsoft Defender for Cloud Apps, or a valid license for Microsoft Entra ID P1
- A valid license for Menlo Security

## Deployment

1. Log into your Menlo Admin portal and use the [Menlo Security Integration with Microsoft Cloud Access Security Setup Guide](https://admin.menlosecurity.com/docs/guides/web_admin_settings_casb.html?highlight=microsoft) to integrate the products.
2. Investigate cloud apps discovered on your network. For more information and investigation steps, see [Working with cloud discovery](working-with-cloud-discovery-data).
3. Any app that you set as unsanctioned in Defender for Cloud Apps will be pinged by Menlo Security every two hours, and then automatically blocked by Menlo Security. For more information about unsanctioning apps, see [Sanctioning/unsanctioning an app](governance-discovery#sanctioningunsanctioning-an-app).