---
layout: Conceptual
title: Review Security Recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/review-security-recommendations
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
zone_pivot_group_filename: defender-for-cloud/zone-pivots/zone-pivot-groups.json
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to review security recommendations in Microsoft Defender for Cloud to improve the security posture of your environments.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
zone_pivot_groups: defender-portal-experience
ai-usage: ai-assisted
locale: en-us
document_id: 44b3f613-c20a-0354-0ef1-6b23f2c0de7e
document_version_independent_id: b59e04ac-3f13-db8f-7862-8363cdebf1c2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/review-security-recommendations.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/review-security-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/review-security-recommendations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: ea5a7c1f-5f7a-cd9d-d9f2-9daeed52d406
---

# Review Security Recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

In Microsoft Defender for Cloud, resources and workloads are assessed against built-in and custom security policies and regulatory compliance frameworks. You apply policies and compliance in your cloud environments, such as Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP). Based on those assessments, security recommendations provide practical steps to remediate security problems and improve your security posture.

For more information about security recommendations, risk factors, prioritization, and classification, see [Security recommendations](security-recommendations).

Note

In the portal, some recommendations that previously appeared as a single aggregated item now display as multiple individual recommendations. This change reflects a shift from grouping related findings under one recommendation to listing each recommendation separately.

- You might see a longer list of recommendations compared to before. Combined findings, such as vulnerabilities, exposed secrets, or misconfigurations, now appear as individual recommendations rather than nested under a parent recommendation.
- The old grouped recommendations still appear side by side with the new format for now. They will be deprecated.
- These recommendations are marked as **Preview**. This tag indicates that the recommendation is in an early state and doesn't affect Secure Score yet.
- Secure Score currently applies to the parent recommendation only, not to each individual item.

Seeing both formats or recommendations with a **Preview** tag is expected during the transition. This transition aims to improve clarity and allow you to act on specific recommendations more easily. For more information, see [Transition from grouped to individual recommendations](transition-grouped-individual-recommendations).

## Prerequisites

Recommendations are included with Defender for Cloud, but you can't see [risk prioritization](risk-prioritization) unless you enable Microsoft Defender Cloud Security Posture Management on your environment.

## Review the recommendations page

::: zone pivot="azure-portal"

Review recommendations and make sure all the details are correct before you resolve them.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Recommendations**.
3. Apply filters such as:

    - **Exposed asset**: Filter by assets with exposure to threats.
    - **Asset risk factors**: Filter by specific risk conditions.
    - **Environment**: Filter by Azure, AWS, or GCP.
    - **Workload**: Filter by specific workload types.
    - **Recommendation maturity**: Filter by recommendation readiness level.
4. On the left side of the page, you can choose to view recommendations by security category:

    - **All recommendations**: Complete list of security recommendations.
    - **Misconfigurations**: Configuration-related security issues.
    - **Vulnerabilities**: Software vulnerabilities requiring patches.
    - **Exposed Secrets**: Credentials and secrets that might be compromised.

    The **All recommendations**, **Misconfigurations**, **Vulnerabilities**, and **Exposed Secrets** tabs can help you focus your view by security category so that you can choose to see everything at once or drill down into specific areas.

    Note

    When you select a security category filter, both the recommendations list and the summary cards update to reflect only the recommendations in that category.
5. Select a recommendation.

### Identify new recommendations

To help you stay aware of changes that might affect your environment and Secure Score, Defender for Cloud provides several indicators for recently introduced recommendations:

- **New tag**: Recommendations introduced in the last 30 days are marked with a **New** tag in the recommendations list. Use this tag to quickly identify findings that are new to your environment and prioritize review.
- **Change log**: Select **View updates** on the Secure Score card to open the change log, which shows which recommendations were recently added and how they affect your score.
- **Portal banner**: When new GA recommendations are added that affect Secure Score, a banner appears on the Secure Score page to notify you of the change and link to the change log.

If you notice a Secure Score change after a large release of new recommendations, the change reflects the broader scope of your evaluated estate, not a degradation of your environment's security. Use the change log and **New** tag to identify which recommendations are driving the change.

### Recommendation views

The Azure portal provides three distinct ways to view and interact with recommendations.

- Flat list view
- Resource views
- Recommendation title view

#### Flat list view

The flat list view displays all recommendations organized by individual assets, ordered by risk level. Each row represents a single recommendation affecting a specific resource.

[![Screenshot of Azure portal Flat list view showing a list of critical storage account recommendations by resource.](media/review-security-recommendations/review-by-findings.png)](media/review-security-recommendations/review-by-findings.png#lightbox)

When you select a recommendation row, a side panel opens displaying:

- **Overview**: General information about the recommendation, including its description, details of the exposed asset, and other relevant recommendation specifics.
- **Remediation steps**: Actionable guidance to resolve the security issue.
- **Map preview**: Displays all related attack paths passing through the asset, aggregated by target node type. You can:

    - Select an aggregated path to reveal all associated attack and additional paths
    - Select a specific path to view its detailed visualization
- **Related initiatives**: Security initiatives and compliance frameworks associated with the recommendation
- Additional tabs might appear for specific recommendations with relevant contextual information

#### Resource views

In addition to **Group by title**, the Azure portal supports **Group by resource**. Grouping by resource puts all findings for the same asset in one place. This approach is helpful when a single owner is responsible for an asset and should receive all of its findings together.

[![Screenshot of Azure security portal grouped by resource, showing critical findings, risk levels, recommendations, and owner columns.](media/review-security-recommendations/review-by-resource.png)](media/review-security-recommendations/review-by-resource.png#lightbox)

#### Recommendation title view

The recommendation title view aggregates recommendations by title, showing a consolidated list ordered by risk level. Each row represents all instances of a particular recommendation across your environment.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Recommendations**.
3. Select **Group by title**.

    [![Screenshot of the recommendations page that shows the location of the Group by title toggle.](media/review-security-recommendations/group-by-title.png)](media/review-security-recommendations/group-by-title.png#lightbox)

When you select an aggregated recommendation row, a side panel displays the following information:

- **Overview**: General information including the recommendation description, risk level distribution across affected resources, governance status, and other relevant details
- **Remediation steps**: Actionable guidance to resolve the security issue
- **Exposed assets**: A list of all resources affected by this recommendation
- **Related initiatives**: Security initiatives and compliance frameworks associated with the recommendation
- Additional tabs might appear for specific recommendations with relevant contextual information

::: zone-end

::: zone pivot="defender-portal"

The **Recommendations** page in Exposure Management provides a prioritized list of security actions designed to improve your cloud security posture by addressing vulnerabilities, misconfigurations, and exposed secrets. The page ranks these recommendations by effective risk to help security teams focus on the most critical threats first.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Exposure Management** &gt; **Recommendations** &gt; **Cloud**.

    [![Screenshot of Recommendations page in Defender Portal.](media/defender-portal-recommendations.png)](media/defender-portal-recommendations.png#lightbox)
3. Apply filters such as:

    - **Exposed asset**: Filter by assets with exposure to threats.
    - **Asset risk factors**: Filter by specific risk conditions.
    - **Environment**: Filter by Azure, AWS, or GCP.
    - **Workload**: Filter by specific workload types.
    - **Recommendation maturity**: Filter by recommendation readiness level.
4. In the left-hand side of the page, you can choose to view recommendations by security category:

    - **All recommendations**: Complete list of security recommendations.
    - **Misconfigurations**: Configuration-related security issues.
    - **Vulnerabilities**: Software vulnerabilities requiring patches.
    - **Exposed Secrets**: Credentials and secrets that might be compromised.

    Note

    When you select a security category filter, both the recommendations list and the summary cards update to reflect only the recommendations in that category.

### Identify new recommendations

To help you stay aware of changes that might affect your environment and Secure Score, Defender for Cloud provides several indicators for recently introduced recommendations:

- **New tag**: Recommendations introduced in the last 30 days are marked with a **New** tag in the recommendations list. Use this tag to quickly identify findings that are new to your environment and prioritize review.
- **Change log**: Select **View updates** on the Secure Score card to open the change log, which shows which recommendations were recently added and how they affect your score.
- **Portal banner**: When new GA recommendations are added that affect Secure Score, a banner appears on the Secure Score page to notify you of the change and link to the change log.

If you notice a Secure Score change after a large release of new recommendations, the change reflects the broader scope of your evaluated estate — not a degradation of your environment's security. Use the change log and **New** tag to identify which recommendations are driving the change.

### Recommendations summary cards

For each view, the page displays summary cards that provide an at-a-glance overview of your cloud security posture:

- **Cloud secure score**: Shows your overall cloud security health based on the security recommendations in your environment.
- **Score history**: Tracks your Secure Score changes over the last seven days, helping you identify trends and measure improvement.
- **Recommendations by risk level**: Summarizes the number of active security recommendations, categorized by severity (Critical, High, Medium, Low).
- **How risk level is calculated**: Explains how severity ratings and asset-specific risk factors are combined to determine the overall risk level for each recommendation.

### Recommendation views

The Defender portal provides two distinct ways to view and interact with recommendations:

- Recommendation per asset view
- Recommendation title view

#### Recommendation per asset view

The recommendation per asset view displays all recommendations organized by individual assets, ordered by risk level. Each row represents a single recommendation affecting a specific resource.

When you select a recommendation row, a side panel displays:

- **Overview**: General information about the recommendation, including its description, details of the exposed asset, and other relevant recommendation specifics
- **Remediation steps**: Actionable guidance to resolve the security issue
- **Map preview**: Displays all related attack paths passing through the asset, aggregated by target node type. You can:

    - Select an aggregated path to reveal all associated attack and additional paths
    - Select a specific path to view its detailed visualization
- **Related initiatives**: Security initiatives and compliance frameworks associated with the recommendation
- Additional tabs might appear for specific recommendations with relevant contextual information

#### Recommendation title view

The recommendation title view aggregates recommendations by title, showing a consolidated list ordered by risk level. Each row represents all instances of a particular recommendation across your environment.

When you select an aggregated recommendation row, a side panel opens displaying:

- **Overview**: General information including the recommendation description, risk level distribution across affected resources, governance status, and other relevant details
- **Remediation steps**: Actionable guidance to resolve the security issue
- **Exposed assets**: A list of all resources affected by this recommendation
- **Related initiatives**: Security initiatives and compliance frameworks associated with the recommendation
- Additional tabs might appear for specific recommendations with relevant contextual information

#### Recommendation per resource view

In addition to Group by title, the portal supports Group by resource. Grouping by resource puts all findings for the same asset in one place. This approach is helpful when a single owner is responsible for an asset and should receive all of its findings together.

[![Screenshot of recommendations side pane.](media/review-security-recommendations/defender-portal-recommendation-side-pane.png)](media/review-security-recommendations/defender-portal-recommendation-side-pane.png#lightbox)

Alternative access paths to recommendations:

- **Cloud infrastructure** &gt; **Overview** &gt; **Security posture** &gt; **Security recommendations** &gt; **View recommendations**
- **Exposure Management** &gt; **Initiatives** &gt; **Cloud Security** &gt; **Open initiative page** &gt; **Security Recommendations**

Note

You might see different resources between the Azure portal and Defender portal.

- You might notice deleted resources that still show up in the Azure portal. Deleted resources can still appear because the Azure portal currently shows the last known state of resources. The product team is working to fix this condition so that deleted resources no longer appear.
- Some resources that come from Azure Policy might not show up in the Defender portal. During preview, the portal only displays resources that have security context and contribute to meaningful security insights.
- Resources tied to free subscriptions don't currently appear in the Defender portal.

::: zone-end

## Explore a recommendation

::: zone pivot="azure-portal"

You can interact with recommendations in multiple ways. If an option isn't available, that option isn't relevant to the selected recommendation.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Recommendations**.
3. Select a recommendation.
4. In **Take action**:

    - **Remediate**: A description of the manual steps required to resolve the security problem on the affected resources. For recommendations with the **Fix** option, you can select **View remediation logic** before applying the suggested fix to your resources.
    - **Recommendation owner and set due date**: If you enable a [governance rule](governance-rules) for the recommendation, you can assign an owner and due date.
    - **Exempt**: You can exempt resources from the recommendation. Disable rules, which were previously used to suppress specific findings, are being deprecated. Use [exemptions](exempt-resource) instead. For migration guidance, see [Transition from disable rules to exemptions](transition-disable-rules-exemptions).
    - **Workflow automation**: Set a logic app to trigger with the recommendation.

    Note

    With the new individual recommendation format, governance works at the finding level. You can assign owners and due dates to specific findings, and you can use governance rules with resource tags, for example, `Team: DataPlatform`, to automatically route recommendations to the correct owner or queue.

    [![Screenshot showing the Take action tab with options for Remediate, Assign owner and due date, Exempt, and Workflow automation.](media/review-security-recommendations/take-action.png)](media/review-security-recommendations/take-action.png#lightbox)
5. In **Graph**, view and investigate all the context that's used for risk prioritization, including [attack paths](how-to-manage-attack-path). You can select a node in an attack path to view the details of the selected node.

    [![Screenshot that shows the Graph tab in a recommendation, including all the attack paths for that recommendation.](media/review-security-recommendations/recommendation-graph.png)](media/review-security-recommendations/recommendation-graph.png#lightbox)
6. To view more details, select a node.

    [![Screenshot that shows the Graph tab with a node selected, displaying additional details.](media/review-security-recommendations/select-node.png)](media/review-security-recommendations/select-node.png#lightbox)
7. Select **Insights**.
8. To view details, select a vulnerability from the dropdown menu.

    [![Screenshot of the Insights tab for a node.](media/review-security-recommendations/insights.png)](media/review-security-recommendations/insights.png#lightbox)
9. (Optional) To view the associated recommendation page, select **Open the vulnerability page**.
10. [Remediate the recommendation](implement-security-recommendations).

::: zone-end

::: zone pivot="defender-portal"

In the Defender portal, you can interact with recommendations in multiple ways through the Exposure Management experience. When you select a recommendation from the **Exposure Management** &gt; **Recommendations** &gt; **Cloud** tab, you can explore detailed information and take action.

Apply filters and filter sets such as **Exposed asset**, **Asset risk factors**, **Environment**, **Workload**, and **Recommendation maturity**.

On the left navigation pane, you can choose to either view all recommendations or view by a specific category.

Separate views exist for issue types:

- **Misconfigurations**
- **Vulnerabilities**
- **Exposed Secrets**

For each view, you see the **Cloud Secure Score**, **Score history**, **Recommendation by risk level**, and how the risk is calculated.

By integrating Defender for Cloud in the Defender portal, you can also access enhanced cloud recommendations through the unified interface.

Key improvements in the cloud recommendations experience include:

- **Risk factors per asset**: Assess the broader exposure context of each recommendation for informed decisions.
- **Risk-based scoring**: New scoring that weighs recommendations based on severity, asset context, and potential impact.
- **Enhanced data**: Core recommendation data from Azure Recommendations enriched with additional fields and capabilities from Exposure Management.
- **Prioritized by criticality**: Greater emphasis on critical issues that pose the highest risk to your organization.

The unified experience ensures that cloud security recommendations are contextualized within the broader security landscape, enabling more informed decision-making and efficient remediation workflows.

::: zone-end

For more information about understanding risk levels, recommendation classification, and detailed explanations of recommendation dashboard fields, see [Security recommendations](security-recommendations).

::: zone pivot="azure-portal"

## Manage your assigned recommendations

Defender for Cloud supports governance rules for recommendations. You can assign a recommendation owner or a due date. You can help ensure accountability by using governance rules, which also support a service-level agreement (SLA) for recommendations.

- Recommendations appear as **On time** until their due date passes. Then they change to **Overdue**.
- When a recommendation isn't classified as **Overdue**, it doesn't affect your Microsoft Secure Score.
- You can also apply a grace period so that overdue recommendations don't affect your Secure Score.

Note

During the preview period, new individual recommendations are marked **Preview** and don't affect risk based Secure Score until the format reaches GA. Legacy GA items continue to impact score as before.

Learn more about how to configure [governance rules](governance-rules).

To see all of your assigned recommendations:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Recommendations**.
3. Select **Add filter** &gt; **Owner**.
4. Select your user entry.
5. Select **Apply**.
6. In the recommendation results, review the recommendations, including affected resources, risk factors, attack paths, due dates, and status.
7. Select a recommendation to review it further.

To make changes to an assignment, complete the following steps:

1. Go to **Take action** &gt; **Change owner & due date**.
2. Select **Edit assignment** to change the recommendation owner or due date.
3. If you select a new remediation date, specify why remediation should be completed by that date in **Justification**.
4. Select **Save**.

    Note

    When you change the expected completion date, the due date for the recommendation doesn't change, but security partners can see that you plan to update the resources by the specified date.

By default, the owner of the resource receives a weekly email that shows all the recommendations assigned to them.

Use the **Set email notifications** option to:

- Override the default weekly email to the owner.
- Notify owners weekly with a list of open or overdue tasks.
- Notify the owner's direct manager with an open task list.

## Review recommendations in Azure Resource Graph

You can use [Azure Resource Graph](/en-us/azure/governance/resource-graph/) to write a [Kusto Query Language (KQL)](/en-us/azure/data-explorer/kusto/query/) query to query Defender for Cloud security posture data across multiple subscriptions. By using Azure Resource Graph, you can efficiently query at scale across cloud environments by viewing, filtering, grouping, and sorting data.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Recommendations**.
3. Select a recommendation.
4. Select **Open query**.
5. You can open the query in one of two ways:

    - **Query returning affected resource**: Returns a list of all of the resources that the recommendation affects.
    - **Query returning security findings**: Returns a list of all security issues that the recommendation found.
6. Select **run query**.

    [![Screenshot of Azure Resource Graph Explorer that shows the results for the recommendation from the previous screenshot.](media/review-security-recommendations/run-query.png)](media/review-security-recommendations/run-query.png#lightbox)
7. Review the results.

Note

The `properties.status.firstEvaluationDate` field indicates when the security assessment was first evaluated for the resource. This value is different from **First seen at** in software inventory, which indicates when the software was first seen on the asset.

Note

If your dashboards or automations currently rely on Sub Assessment APIs or queries, plan to migrate to the Assessment APIs or securityFindings equivalents for the individual recommendation format. During the side by side period, you might see duplicate data, with both legacy grouped and new individual assessments. Use **Preview/New** version UI tags or API filters to focus on one format and avoid double counting. The Open query entry point can help you generate updated queries from the portal.

::: zone-end