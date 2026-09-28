---
layout: Conceptual
title: Alerts for Azure App Service - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-azure-app-service
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: This article lists the security alerts for Azure App Service visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 0dbd857e-88d2-6aea-2a74-e08f583f6e8b
document_version_independent_id: 0abed294-5a43-edb2-08f6-b2b654023b53
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-azure-app-service.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-azure-app-service
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-azure-app-service.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 844727f2-381a-e329-858a-07050ff14c5d
---

# Alerts for Azure App Service - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for Azure App Service from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

## Azure App Service alerts

[Further details and notes](defender-for-app-service-introduction)

## Cloud native detection

App Services operate at the application layer, enabling web apps to process user interactions and manage request flows. Defender for App Services analyzes patterns in these requests to identify behaviors that may indicate security threats. Critical events in web request logs are captured that indicate potential security threats, such as attempts to execute unauthorized code or manipulate application logic.

Examples of suspicious operations captured by Defender for App Services include:

- **Remote code execution** can allow an adversary to run arbitrary commands, potentially gaining control over the application environment.
- **Injection attempts** can manipulate application logic or access sensitive data, leading to data breaches or unauthorized actions.
- **Compromise indicators** can indicate the application is already compromised and may be leveraged to launch attacks against other systems or services.

## Workload runtime detection

Defender for App Services monitors the workload runtime activity to detect suspicious operations, including process creation events.

Examples of suspicious workload runtime activity include:

- **Web shell activity** - Defender for App Services monitors the activity on the running containers to identify behaviors that resemble web shell invocations.
- **Crypto mining activity** - Defender for App Services uses several heuristics to identify crypto mining activity on the running containers, including suspicious download activity, CPU optimization, suspicious process execution, and more.
- **Reconnaissance tools** – Defender for App Services identifies usage of reconnaissance tools that have been used for malicious activities.

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.