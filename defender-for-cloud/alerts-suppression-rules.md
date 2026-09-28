---
layout: Conceptual
title: Suppress alerts from Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-suppression-rules
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
description: Learn how to create alert suppression rules in Microsoft Defender for Cloud to automatically dismiss false positives and reduce alert noise.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 9990ba3b-191c-25a7-8242-1c3b76b74e48
document_version_independent_id: 927c2da6-180d-ad73-01fe-5a9f1f60a9d6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-suppression-rules.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-suppression-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-suppression-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 7db1574f-19ea-1dd7-be40-e8706d121750
---

# Suppress alerts from Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud generates security alerts when it detects threats in your environment. Some alerts might be expected or not relevant for your environment. You can create suppression rules to automatically dismiss alerts that match predefined conditions.

When an alert matches an active suppression rule, its status changes to **Dismissed**. The alert still appears in the security alerts list, but it no longer triggers notifications or appears in active alert views.

## Prerequisites

Required roles and permissions:

- **Security admin** or **Owner** can create and delete suppression rules.
- **Security reader** or **Reader** can view suppression rules.

For cloud availability, see the [Defender for Cloud support matrices for Azure commercial/other clouds](support-matrix-defender-for-cloud).

## Create a suppression rule

You can create a suppression rule for one or more alert types, or start from an existing alert to suppress similar alerts.

You can apply suppression rules to management groups or to subscriptions.

- To suppress alerts for a management group, use [Azure Policy](/en-us/azure/governance/policy/overview).
- To suppress alerts for subscriptions, use the Azure portal or the REST API.

A suppression rule applies only to alert types that have already been triggered at least once.

### Create a suppression rule for one or more alert types

To create a suppression rule for one or more alert types:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Security alerts**.
3. Select **Suppression rules**.

    [![Screenshot of the Security alerts page with the Suppression rules button highlighted.](media/alerts-suppression-rules/security-alerts-suppression-rules-button.png)](media/alerts-suppression-rules/security-alerts-suppression-rules-button.png#lightbox)
4. Select **Create new suppression rule**.

    [![Screenshot of the Suppression rules page with the Create new suppression rule button highlighted.](media/alerts-suppression-rules/create-new-suppression-rule-all-alerts.png)](media/alerts-suppression-rules/create-new-suppression-rule-all-alerts.png#lightbox)
5. Select the subscriptions that the rule applies to.
6. Under **Alerts**, select **Custom** to choose specific alert types, or select **All** to apply the rule to all alert types.
7. If you selected **Custom**, select the alert types that the rule applies to.
8. If needed, add entity conditions to limit the rule to specific resources or entity values.
9. Enter a rule name.

    Rule names must begin with a letter or a number, be between 2 and 50 characters, and contain no symbols other than dashes (-) or underscores (\_).
10. Select whether the rule is enabled or disabled.
11. Select a reason for suppressing the alert.
12. If needed, add a comment.
13. Select when the rule expires:

    - Select **Custom** to set an end date and time.
    - Select **None** to run the rule indefinitely.
14. If needed, select **Simulate** to test the rule.
15. Select **Apply**.

The rule is created and listed on the **Suppression rules** page.

### Create a suppression rule from a specific alert

To create a suppression rule from an alert that already exists:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Security alerts**.
3. Select an alert.
4. Select **Take action**.
5. In the **Take action** tab, expand **Suppress similar alerts**.
6. Select **Create suppression rule**.

    [![Screenshot of an alert details page with the Create suppression rule button highlighted under Suppress similar alerts.](media/alerts-suppression-rules/create-suppression-rule-one-alert.png)](media/alerts-suppression-rules/create-suppression-rule-one-alert.png#lightbox)
7. Review the selected alert type.
8. If needed, add entity conditions to limit the rule to specific resources or entity values.
9. Enter a rule name.

    Rule names must begin with a letter or a number, be between 2 and 50 characters, and contain no symbols other than dashes (-) or underscores (\_).
10. Select whether the rule is enabled or disabled.
11. Select a reason for suppressing the alert.
12. If needed, add a comment.
13. Select when the rule expires:

    - Select **Custom** to set an end date and time.
    - Select **None** to run the rule indefinitely.
14. If needed, select **Simulate** to test the rule.
15. Select **Apply**.

The rule is created and listed on the **Suppression rules** page.

## Edit or delete a suppression rule

To edit or delete a suppression rule:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Security alerts**.
3. Select **Suppression rules**.
4. Select the rule that you want to update.
5. To edit the rule, select **Edit**, update the rule details, and then select **Apply**.
6. To delete the rule, select **Remove**.

Deleting a suppression rule doesn't change the status of alerts that the rule already dismissed.

## Create and manage suppression rules with the API

You can create, view, and delete alert suppression rules by using the Defender for Cloud REST API.

To create a suppression rule for a specific alert type, first use the [Alerts REST API](/en-us/rest/api/defenderforcloud-composite/alerts?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true) to retrieve the alert that you want to suppress. Then use the [Alerts Suppression Rules REST API](/en-us/rest/api/defenderforcloud-composite/alerts-suppression-rules?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true) to create the rule.

The relevant methods for suppression rules in the [Alerts Suppression Rules REST API](/en-us/rest/api/defenderforcloud-composite/alerts-suppression-rules?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true) are:

- **UPDATE** - Create or update a suppression rule in a specified subscription.
- **GET** - Get the details of a specific suppression rule in a specified subscription.
- **LIST** - List all suppression rules configured for a specified subscription.
- **DELETE** - Deleting a suppression rule doesn't change the status of alerts that the rule already dismissed. Use this method to remove an existing suppression rule.

For details and usage examples, see the [Defender for Cloud operation groups API reference](/en-us/rest/api/defenderforcloud-composite/operation-groups?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).