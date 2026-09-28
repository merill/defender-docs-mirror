---
layout: Conceptual
title: Exclude machines from agentless scanning - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/exclude-machines-agentless-scanning
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
description: Learn how to exclude machines from agentless scanning in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-06-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 58041514-e752-4417-aa25-1e1253732906
document_version_independent_id: 7096506e-7769-1e5c-b292-0bc593ca7736
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/exclude-machines-agentless-scanning.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/exclude-machines-agentless-scanning
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/exclude-machines-agentless-scanning.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 32f6d32d-3015-1a6e-0590-b7b686ce092b
---

# Exclude machines from agentless scanning - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud uses agentless machine scanning to improve the security posture of connected machines. For details, see [Agentless machine scanning](concept-agentless-data-collection). Agentless scanning doesn't need installed agents. It also doesn't require network connectivity and doesn't affect machine performance.

By default, agentless scanning is turned on for all supported machines when Defender for Servers Plan 2 or the Defender cloud security posture management (Defender CSPM) plan is enabled.

In some circumstances, you might want to exclude machines from agentless scanning recommendations. You can do this using preexisting environment tags. Excluded machines are skipped during continuous machine discovery.

## Prerequisites

Before you exclude machines from agentless scanning, ensure the following requirements are met:

- Defender for Servers Plan 2 or the Defender cloud security posture management (Defender CSPM) plan is enabled.
- Agentless scanning is enabled in the plan.

## Exclude machines

To exclude machines from agentless scanning by using environment tags:

1. In Defender for Cloud, select **Environment settings**.
2. Select the relevant subscription or multicloud connector.
3. For either the Defender cloud security posture management (Defender CSPM) or Defender for Servers P2 plan, select **Settings**.
4. In **Agentless scanning for machines**, select **Edit configuration**.

    [![Screenshot of the link to edit the agentless scanning configuration.](media/enable-vulnerability-assessment-agentless/agentless-scanning-edit-configuration.png)](media/enable-vulnerability-assessment-agentless/agentless-scanning-edit-configuration.png#lightbox)
5. In **Agentless scanning configuration**, enter the tag name and value for machines that you want to exclude. You can enter multiple `tag:value` pairs.

    ![Screenshot of the tag and value fields for excluding machines from agentless scanning.](media/enable-vulnerability-assessment-agentless/agentless-scanning-exclude-tags.png)
6. Select **Save**.