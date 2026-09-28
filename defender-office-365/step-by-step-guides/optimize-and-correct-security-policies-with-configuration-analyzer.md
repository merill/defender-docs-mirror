---
layout: Conceptual
title: Optimize and correct threat policies with configuration analyzer - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/optimize-and-correct-security-policies-with-configuration-analyzer
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Configuration Analyzer to compare your email threat policies with Standard and Strict recommendations, apply suggested changes, and review historical configuration changes.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0bc05260-98f7-abad-c73e-e89a9b358721
document_version_independent_id: 0bc05260-98f7-abad-c73e-e89a9b358721
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/optimize-and-correct-security-policies-with-configuration-analyzer.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/optimize-and-correct-security-policies-with-configuration-analyzer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/optimize-and-correct-security-policies-with-configuration-analyzer.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 8c9740c7-c6a7-68c2-8bc4-7968cb43f05a
---

# Optimize and correct threat policies with configuration analyzer - Microsoft Defender for Office 365 | Microsoft Learn

## Overview

Configuration analyzer is a central location for managing email threat policies in your tenant. Compare your settings with Standard and Strict recommendations. You can also apply changes and review past updates that affected your security posture.

## Prerequisites

- A Microsoft 365 organization with cloud mailboxes.
- Sufficient permissions (Security Administrator role)
- 5 minutes to perform the steps below.

## Compare settings and apply recommendations

Perform the following steps to compare your settings and apply recommended changes:

1. Navigate to [Configuration analyzer in the Microsoft Defender portal](https://security.microsoft.com/configurationAnalyzer).
2. Select **Standard recommendations** or **Strict recommendations** from the top menu.
3. If your settings differ from the chosen baseline, suggested changes appear.
4. Select a recommendation to view the suggested action, affected policy, and current setting.
5. To apply it, select **Apply recommendation**, then select **OK** to confirm.
6. To edit a policy directly, select **View policy** instead. A new tab opens with the policy for the selected recommendation.

## View historical configuration changes

In **Configuration analyzer**, select **Configuration drift analysis and history** from the top menu bar.

This page shows changes made to your threat policies in the selected time range. It also shows whether each change improved or lowered your security posture.

To learn more details about Configuration Analyzer, see [Configuration analyzer](../configuration-analyzer-for-security-policies).