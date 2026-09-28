---
layout: Conceptual
title: Drive Recommendation Remediation by Using Governance Rules - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/governance-rules
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
description: Learn how to drive remediation of security recommendations by using governance rules in Microsoft Defender for Cloud.
services: defender-for-cloud
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: bf34e6d7-7748-4500-651a-3d2b3228f5e0
document_version_independent_id: c734173b-81c5-83cb-85fd-a735bd1fc369
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/governance-rules.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/governance-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/governance-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: b144f1f3-82a7-6d08-4b4a-e65d2eecb9f7
---

# Drive Recommendation Remediation by Using Governance Rules - Microsoft Defender for Cloud | Microsoft Learn

Security teams are responsible for improving their organization's security posture, but team members might not always follow through to implement security recommendations. Security teams can set governance rules to help drive accountability and create a service-level agreement (SLA) around the remediation process.

For an in-depth discussion about why governance rules are helpful, watch [Episode 15 - Governance rules in Defender for Cloud](episode-fifteen) in the *Defender for Cloud in the field* video series.

## How governance rules work

You can define rules that automatically assign an owner and a due date to address recommendations for specific resources. Governance rules provide resource owners with a clear set of tasks and deadlines to remediate recommendations.

Governance rules support tracking, assignments, due dates, owners, notifications, and conflict resolution.

### Track remediation progress

Track the progress of remediation tasks by sorting by subscription, recommendation, or owner. You can easily find tasks that need more attention so that you can follow up.

### Assign recommendations to owners

Governance rules can identify resources that require remediation according to specific recommendations or severities. The rule assigns an owner and due date to ensure the recommendations are handled. Many governance rules can apply to the same recommendations, so the rule with the highest priority assigns the owner and due date.

### Set due dates for remediation

The due date for remediation of a recommendation is based on a time frame of 7, 14, 30, or 90 days after the rule triggers the recommendation. For example, if the rule identifies the resource on March 1 and the remediation time frame is 14 days, March 15 is the due date. You can apply a grace period so that resources that need remediation don't affect your Microsoft Secure Score.

### Assign owners to recommendations

You can also set resource owners, which helps you find the right person to handle a recommendation.

In organizations that use resource tags to associate resources with an owner, you can specify the tag key. The governance rule reads the name of the resource owner from the tag.

When an owner isn't found on a resource, associated resource group, or associated subscription based on the tag, the owner is shown as unspecified.

### Configure governance rule notifications

By default, email notifications are sent weekly to resource owners. Emails include a list of on-time and overdue tasks.

By default, the resource owner's manager receives an email that shows overdue recommendations, if the manager's email is found in the organizational Microsoft Entra ID.

### Resolve conflicts between governance rules

Conflicting rules are applied in scope order. For example, rules on a management scope for Azure management groups, Amazon Web Services (AWS) accounts, and Google Cloud Platform (GCP) organizations take effect before rules on scopes, like Azure subscriptions, AWS accounts, or GCP projects.

## Prerequisites

Before you define a governance rule, make sure the following prerequisites are met:

- The [Defender Cloud Security Posture Management (Defender CSPM) plan](concept-cloud-security-posture-management) must be enabled.
- You need **Contributor**, **Security Admin**, or **Owner** permissions on the Azure subscriptions.
- For AWS accounts and GCP projects, you need **Contributor**, **Security Admin**, or **Owner** permissions on the Defender for Cloud AWS or GCP connectors.

## Define a governance rule

To create a governance rule in Microsoft Defender for Cloud, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Management** &gt; **Environment settings** &gt; **Governance rules**.
3. Select **Create governance rule**.

    [![Screenshot that shows the page where you add a governance rule.](media/governance-rules/add-rule.png)](media/governance-rules/add-rule.png#lightbox)
4. Specify a rule name and scope in which to apply the rule. Rules for management scope (Azure management groups, AWS master accounts, and GCP organizations) are applied before the rules on a single scope.

    Note

    Exclusions can't be created by using the portal wizard. To define exclusions, use the API.
5. Set a priority level. Rules are run in priority order from the highest (1) to the lowest (1000).
6. Specify a description to help you identify the rule.
7. Select **Next**.
8. Specify how the rule affects recommendations.

    - **By severity**: The rule assigns the owner and due date to any recommendation in the subscription that has no owner or due date and that matches the specified severity levels.
    - **By risk level**: The rule assigns an owner and due date to any recommendations that match the specified risk levels.
    - **By recommendation category**: The rule assigns an owner and due date to any recommendations that match the specified recommendation category. 
        Note

        The recommendations category to implement governance rules is for use with the new individual recommendation format. [![Screenshot of the list of recommendation categories.](media/governance-rules/recommendation-categories.png)](media/governance-rules/recommendation-categories.png#lightbox)
    - **By specific recommendations**: Select the specific built-in or custom recommendations that the rule applies to.

    To apply the rule to already-generated recommendations, you can rerun the rule using the UI or API.

    [![Screenshot that shows the page where you add conditions for a governance rule.](media/governance-rules/create-rule-conditions.png)](media/governance-rules/create-rule-conditions.png#lightbox)
9. To specify who's responsible for fixing recommendations covered by the rule, set the owner.

    - **By resource tag**: On your resources, enter the resource tag for the resource owner.
    - **By email address**: Enter the owner's email address.
10. Specify a remediation time frame that spans from when remediation recommendations are identified to when the remediation is due. If recommendations were issued according to the Microsoft cloud security benchmark, and you don't want the resources to affect your Secure Score until they're overdue, select **Apply grace period**.
11. (Optional) By default, owners and their managers are notified weekly about open and overdue tasks. If you don't want them to receive these weekly emails, clear the notification options.
12. Select **Create**.

If there are existing recommendations that match the definition of the governance rule, you can either:

- Assign an owner and due date to recommendations that don't already have an owner or due date.
- Overwrite the owner and due date of existing recommendations.

When you delete or disable a rule, all existing assignments and notifications remain.

## See the effects of rules

You can view the effect that governance rules have in your environment.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Management** &gt; **Environment settings** &gt; **Governance rules**.
3. Review the governance rules. The default list shows all the governance rules that are applicable in your environment.
4. You can search for rules or filter rules. There are several different ways to filter rules.

    - Filter on **Environment** to identify rules for Azure, AWS, and GCP.
    - Filter on rule name, owner, or the time between when the recommendation was issued and the due date.
    - Filter on **Grace period** to find Microsoft cloud security benchmark recommendations that don't affect your Secure Score.
    - Identify by status.

    [![Screenshot that shows the page where you can view and filter rules.](media/governance-rules/view-filter-rules.png)](media/governance-rules/view-filter-rules.png#lightbox)

## Review the Governance report

You can use a Governance report to see recommendations by rule and owner that are completed on time, overdue, or unassigned. You can use this feature for any subscription that has governance rules.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Management** &gt; **Environment settings** &gt; **Governance rules** &gt; **Governance report**.

    [![Screenshot that shows the Governance rules page where the Governance report button is located.](media/governance-rules/governance-report.png)](media/governance-rules/governance-report.png#lightbox)
3. Select a subscription.

    [![Screenshot that shows governance status by rule and owner in the governance workbook.](media/governance-rules/governance-in-workbook.png)](media/governance-rules/governance-in-workbook.png#lightbox)

From the Governance report, you can drill down into recommendations by the following categories:

- Scope
- Display name
- Priority
- Remediation time frame
- Owner type
- Owner details
- Grace period
- Cloud