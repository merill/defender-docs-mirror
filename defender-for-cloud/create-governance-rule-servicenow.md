---
layout: Conceptual
title: Create automatic tickets with governance rules - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/create-governance-rule-servicenow
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
description: Create Defender for Cloud governance rules that automatically open ServiceNow ITSM tickets for selected recommendations or severity levels.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: ce23d196-dec7-bae1-5a89-48b6b465dafa
document_version_independent_id: 644f94eb-105c-e761-7e3d-7fb5df43c1c8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/create-governance-rule-servicenow.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/create-governance-rule-servicenow
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/create-governance-rule-servicenow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 018941fd-450c-ddcd-326a-5e1f5a4b2506
---

# Create automatic tickets with governance rules - Microsoft Defender for Cloud | Microsoft Learn

The integration of ServiceNow's IT Service Management (ITSM) module and Defender for Cloud allow you to create governance rules that automatically open tickets in ServiceNow for specific recommendations or severity levels. ServiceNow tickets can be created, viewed, and linked to recommendations directly from Defender for Cloud, enabling seamless collaboration between the two platforms and facilitating efficient incident management.

## Prerequisites

Before you create governance rules, make sure you meet the following requirements:

- Have an [application registry in ServiceNow](https://www.opslogix.com/knowledgebase/servicenow/kb-create-a-servicenow-api-key-and-secret-for-the-scom-servicenow-incident-connector).
- Enable [Defender Cloud Security Posture Management (CSPM)](tutorial-enable-cspm-plan) on your Azure subscription.
- Admin permissions to ServiceNow to create an assignment.

## Assign an owner with a governance rule

You can create a governance rule to automatically assign an owner to a recommendation in Defender for Cloud. The rule can be based on either the recommendation's severity or a specific recommendation.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Governance rules**.

    ![Screenshot of the environment settings page that shows where the governance rules button is located.](media/integration-servicenow/governance-rules.png)
4. Select **Create governance rule**.
5. Enter a rule name and select a scope.
6. Select **ServiceNow** In the Type field.
7. Enter a priority.
8. Select and integration instance.
9. Select a ServiceNow ticket type.
10. Select **Next**.
11. Select either:

    - **By Severity** and the severity level.
    - **By recommendation** and the recommendation.
12. Select an owner.
13. Select a remediation timeframe.
14. (Optional) Toggle the switch to apply a grace period.
15. (Optional) Set email notifications.
16. Select **Create**.