---
layout: Conceptual
title: Transition from Disable Rules to Exemptions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/transition-disable-rules-exemptions
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to migrate from disable rules to exemptions in Microsoft Defender for Cloud. Grouped recommendations are deprecated in favor of individual recommendations.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 0e832857-4dca-2532-e601-095a6035011e
document_version_independent_id: f744a74d-2365-180c-3e1a-79ec883d5e7a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/transition-disable-rules-exemptions.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/transition-disable-rules-exemptions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/transition-disable-rules-exemptions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 287371a4-5c99-ddd9-110b-1c250ab0bd22
---

# Transition from Disable Rules to Exemptions - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud is changing its recommendation model from grouped recommendations to individual recommendations. Use this guidance to migrate your existing disable rules to the new exemption model. It maps each disable rule type to its exemption equivalent and outlines the steps to complete the migration before grouped recommendations are deprecated.

Important

Grouped recommendations are deprecated on **July 31, 2026**. We recommend completing your migration to exemptions before that date.

As part of this change:

- Grouped recommendations are being deprecated and replaced with individual recommendations. For more information, see [transition from grouped to individual recommendations](transition-grouped-individual-recommendations).
- Disable rules, which are used with grouped recommendations, are being deprecated.
- Exemption rules are the new approach for individual and risk-based recommendations.

## What's changing

In the old model, grouped recommendations use **disable rules** to suppress findings.

[![Screenshot showing the disable rules interface for sub-assessment recommendations.](media/transition-disable-rules-exemptions/disable-rules.png)](media/transition-disable-rules-exemptions/disable-rules.png#lightbox)

In the new model, individual and risk-based recommendations use **exemption rules**. For more information, see [Exempt resources at scale](exempt-resources-at-scale) and [Exempt resources from recommendations](exempt-resource).

Disable rules that you created for grouped recommendations aren't supported in the new model.

## Why use exemptions?

Exemptions give you a more scalable, flexible, and centralized way to manage exceptions.

- **Centralized management for recommendations**: Disable rules apply per recommendation. If you wanted to disable the same Common Vulnerabilities and Exposures (CVE) for multiple recommendations, you had to create a separate rule for each one. With exemptions, you apply a rule once and it affects all relevant recommendations.
- **Resource-level granularity**: Disable rules don't support fine-grained control for a specific resource. Exemptions let you apply rules at the individual resource level, such as a virtual machine or container.
- **Central visibility and tracking**: With disable rules, you had to open each recommendation to view its rules. With exemptions, you can view and manage all rules in one centralized experience.
- **Exemption lifecycle with expiry dates**: Disable rules remain in effect until you remove them manually. Exemptions support expiry dates, which helps you reduce long-lived risk and review accepted vulnerabilities regularly.

## Migration guidance

There's no automatic migration from disable rules to exemptions. You can recreate your existing rules by using exemption conditions.

### Map disable rules to exemption conditions

Use this table to translate your existing disable rules into exemption conditions.

| Disable rule action | Exemption condition |
| --- | --- |
| IDs | Use the **Selected recommendations** condition and search for the relevant recommendation. |
| Categories | Use **Recommendation category**. For example, use categories such as *System updates* or *Service upgrade*. |
| Security checks | Use the **Selected recommendations** condition and search for the relevant recommendation. |
| CVEs | Use the **Vulnerabilities** condition and enter the CVE value in the **CVE** property. |
| CVSS | Use the **Vulnerabilities** condition and enter the CVSS value in the **CVSS** property. |
| Minimum severity | Use the **Vulnerabilities** condition and enter the severity value in the **Minimum severity** property. |
| Non-patchable | Use the **Vulnerabilities** condition and select **Non-patchable**. |

[![Screenshot showing the exemption conditions available when creating an exemption rule.](media/transition-disable-rules-exemptions/exemption-conditions.png)](media/transition-disable-rules-exemptions/exemption-conditions.png#lightbox)

### Recommended migration steps

Use the following steps to migrate your existing disable rules to exemptions.

1. **Identify existing disable rules**: Review the rules configured for each recommendation and note the conditions you use, such as CVE and severity. Alternatively, you can use the following Azure Resource Graph (ARG) query to retrieve all existing disabled rules:

    ```kusto
    policyresources
    | where type =~ "microsoft.authorization/policyassignments"
    | extend filters = todynamic(properties).metadata.subAssessmentSettings.filters
    | where filters != ""
    ```
2. **Translate to exemption conditions**: Use the preceding mapping table to convert each rule to its exemption equivalent.
3. **Create the exemptions**: To create and manage exemptions, see [Exempt resources at scale](exempt-resources-at-scale) and [Exempt resources from recommendations](exempt-resource).

    [![Screenshot showing how to create a new exemption in Defender for Cloud.](media/transition-disable-rules-exemptions/create-new-exemption.png)](media/transition-disable-rules-exemptions/create-new-exemption.png#lightbox)
4. **Prefer reusable rules**: Where possible, use broader exemption conditions that apply across multiple recommendations to reduce duplication.

#### Recreate a vulnerability-based exemption by using the REST API

When you migrate vulnerability assessment disable rules, you can use the Standard Assignments REST API to create an equivalent vulnerability-based exemption.

The following example exempts vulnerability findings that match all the specified conditions: CVE ID, severity, and CVSS score.

Replace `{subscriptionId}` with your Azure subscription ID and `{standardAssignmentName}` with a unique GUID for the exemption.

```http
PUT https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Security/standardAssignments/{standardAssignmentName}?api-version=2024-08-01
```

Use the following request body:

```json
{
  "properties": {
    "description": "Exempts vulnerability findings that match the specified conditions.",
    "displayName": "Vulnerability assessment exemption",
    "excludedScopes": [],
    "effect": "Exempt",
    "assignedStandard": null,
    "exemptionData": {
      "exemptionCategory": "Waiver",
      "assignedAssessment": {
        "assessmentKey": "122e0164-4019-4126-8c64-b0816b49505f"
      },
      "subAssessmentExemptionRule": {
        "if": {
          "allOf": [
            {
              "field": "va.cve.cveId",
              "operationType": "ContainedInOperation",
              "operation": {
                "values": [
                  {
                    "title": "CVE-2020-1347"
                  }
                ]
              }
            },
            {
              "field": "va.cve.severity",
              "operationType": "LessThanFilterOperation",
              "operation": {
                "value": "Low"
              }
            },
            {
              "field": "va.cve.cvss",
              "operationType": "LessThanFilterOperation",
              "operation": {
                "value": "8.0"
              }
            }
          ]
        }
      }
    }
  }
}
```

The `allOf` operator applies the exemption only to vulnerability findings that match all three conditions. Change the assessment key and condition values to match the disable rule that you're recreating.

For more information, see [Standard Assignments - Create](/en-us/rest/api/defenderforcloud/standard-assignments/create).