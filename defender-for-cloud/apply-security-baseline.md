---
layout: Conceptual
title: Review and remediate OS misconfigurations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/apply-security-baseline
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
description: Learn how Microsoft Defender for Cloud uses the guest configuration to compare machine OS settings with baselines in Microsoft Cloud Security Benchmark.
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: bedd594a-9080-35e6-6daf-3f28d0aa61e0
document_version_independent_id: 9261b75f-108d-272b-c2b9-686d6f1d224f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/apply-security-baseline.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/apply-security-baseline
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/apply-security-baseline.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 2955b4d6-f1e2-b06a-71fe-55ecc6c3a494
---

# Review and remediate OS misconfigurations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud provides security recommendations to improve organizational security posture and reduce risk. An important element in risk reduction is machine hardening.

Defender for Cloud assesses operating system settings against compute security baselines provided by the [Microsoft Cloud Security Benchmark (MCSB)](/en-us/security/benchmark/azure/introduction). Machine information is gathered for assessment by using the Azure Policy machine configuration extension (formerly known as guest configuration) on the machine. For more information, see [Operating system misconfigurations in Defender for Cloud](operating-system-misconfiguration).

This article explains how to review and remediate recommendations from the OS baseline assessment.

## Prerequisites

Before you review and remediate OS baseline recommendations, make sure the following prerequisites are met.

| **Requirements** | **Details** |
| --- | --- |
| **Plan** | [Defender for Servers Plan 2 must be enabled](tutorial-enable-servers-plan) |
| **Extension** | The [Azure Policy machine configuration must be installed on machines](security-baseline-guest-configuration). |

This feature previously used the Microsoft Monitoring Agent (MMA) to collect data. If MMA is still in use, you might see duplicate recommendations. To avoid duplicates, [disable the MMA on the machine](prepare-deprecation-log-analytics-mma-agent#duplicate-recommendations).

## Review and remediate OS baseline recommendations

To review and remediate OS baseline recommendations:

1. In Defender for Cloud, open the **Recommendations** page.
2. Select the relevant recommendation.

    - For **Windows** machines, [Vulnerabilities in security configuration on your Windows machines should be remediated (powered by Guest Configuration)](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/8c3d9ad0-3639-4686-9cd2-2b2ab2609bda).
    - For **Linux** machines, [Vulnerabilities in security configuration on your Linux machines should be remediated (powered by Guest Configuration)](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/1f655fb7-63ca-4980-91a3-56dbc2b715c6)

        [![The two recommendations for comparing the OS configuration of machines with the relevant Azure security baseline.](media/apply-security-baseline/recommendations-baseline.png)](media/apply-security-baseline/recommendations-baseline.png#lightbox)
3. On the recommendation details page, review the affected resources and specific security findings.
4. To complete the fix, see [How to remediate security recommendations](implement-security-recommendations).

## Query recommendations

Defender for Cloud uses [Azure Resource Graph](/en-us/azure/governance/resource-graph/overview?branch=main) for application programming interface (API) and portal queries. You can use Azure Resource Graph and its query interfaces to create your own queries and retrieve recommendation information.

You can learn how to [review recommendations in Azure Resource Graph](review-security-recommendations#review-recommendations-in-azure-resource-graph).

Here are two sample queries you can use:

- **Query all unhealthy rules for a specific resource**

    ```rest
    Securityresources 
    | where type == "microsoft.security/assessments/subassessments" 
    | extend assessmentKey=extract(@"(?i)providers/Microsoft.Security/assessments/([^/]*)", 1, id) 
    | where assessmentKey == '1f655fb7-63ca-4980-91a3-56dbc2b715c6' or assessmentKey ==  '8c3d9ad0-3639-4686-9cd2-2b2ab2609bda' 
    | parse-where id with machineId:string '/providers/Microsoft.Security/' * 
    | where machineId  == '{machineId}'
    ```
- **All Unhealthy Rules and the amount if Unhealthy machines for each**

    ```rest
    securityresources 
    | where type == "microsoft.security/assessments/subassessments" 
    | extend assessmentKey=extract(@"(?i)providers/Microsoft.Security/assessments/([^/]*)", 1, id) 
    | where assessmentKey == '1f655fb7-63ca-4980-91a3-56dbc2b715c6' or assessmentKey ==  '8c3d9ad0-3639-4686-9cd2-2b2ab2609bda' 
    | parse-where id with * '/subassessments/' subAssessmentId:string 
    | parse-where id with machineId:string '/providers/Microsoft.Security/' * 
    | extend status = tostring(properties.status.code) 
    | summarize count() by subAssessmentId, status
    ```