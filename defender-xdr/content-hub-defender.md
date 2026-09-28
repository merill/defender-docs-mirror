---
layout: Conceptual
title: Use Content hub with ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/content-hub-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use Content hub with ISOC in Microsoft Defender to discover and install supported Microsoft Sentinel data connectors.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- m365solution-getstarted
- highpri
- tier1
- usx-security
- msftsolution-secops
ms.topic: how-to
ms.service: microsoft-sentinel
ai-usage: ai-assisted
ms.date: 2026-09-06T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: b928f9f2-8671-fbd9-9014-17102a75a1dd
document_version_independent_id: b928f9f2-8671-fbd9-9014-17102a75a1dd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/content-hub-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: content-hub-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/content-hub-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 8f0ab109-61d6-f5a5-918e-5d417041de60
---

# Use Content hub with ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Use Content hub with Integrated Security Operations Center (ISOC) in Microsoft Defender to discover and install supported Microsoft Sentinel content for your ISOC workspace.

Note

During this preview, Content hub supports data connectors. If a solution includes multiple content types, only its data connectors are available for installation.

## Prerequisites

Before you begin, make sure the following requirements are met:

- Your tenant is [eligible for ISOC](isoc-overview).
- You have an [ISOC workspace](onboard-isoc-workspace).
- You have the following permissions:
    - In Unified RBAC:
        - **Content hub read**
        - **Content hub manage**
    - In Azure, **Deploy** permission on the resource group to install solutions.

## Discover content

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **SIEM** &gt; **Content management** &gt; **Content hub**.
3. Search for a solution or use the available filters to find content.
4. Select a solution to view its details and available data connectors.

## Install data connectors

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **SIEM** &gt; **Content management** &gt; **Content hub**.
3. Search for and select the solution that contains the data connector you want to install.
4. Select **View details**.
5. Select **Create**.
6. On the **Basics** tab, select the subscription, resource group, and workspace where you want to deploy the solution.
7. Select **Next** to review the available configuration.
8. On the **Review + create** tab, wait for validation to complete.
9. Select **Create**.

Only supported data connectors from the solution are available for installation. Other content types included in the solution aren't installed during the ISOC preview.

After installation, configure the data connector to start ingesting data into your ISOC workspace.

## Update an installed solution

If an installed solution has an available update, you can update it from Content hub.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **SIEM** &gt; **Content management** &gt; **Content hub**.
3. Search for and select the installed solution.
4. Select **View details**.
5. Select **Update**.
6. Review the solution configuration.
7. Select **Review + create**.
8. Wait for validation to complete.
9. Select **Update**.

Note

During this preview, updates apply only to supported data connector content.