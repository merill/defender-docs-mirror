---
layout: Conceptual
title: Identify and remediate attack paths in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/how-to-manage-attack-path
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
description: Learn how to identify and remediate attack paths in Microsoft Defender for Cloud and enhance the security of your environment.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
zone_pivot_groups: defender-portal-experience
ai-usage: ai-assisted
locale: en-us
document_id: 22a7db7a-66ff-2717-a4b1-7854ccb14fd0
document_version_independent_id: f1e068f4-e9a2-d1ce-9fd2-c8f6316e6413
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/how-to-manage-attack-path.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/how-to-manage-attack-path
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/how-to-manage-attack-path.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: d311f393-19e6-b07a-1b2e-005f3d1e4e1b
---

# Identify and remediate attack paths in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud uses a [proprietary algorithm to locate potential attack paths](concept-attack-path#what-is-an-attack-path) in your multicloud environment. It focuses on real, external threats that attackers can exploit, not broad scenarios. The algorithm finds attack paths that start outside your organization and lead to critical targets. This helps you cut through the noise and act faster.

You can use attack path analysis to find and fix the security issues that pose the biggest risk. Defender for Cloud shows which issues are part of exposed attack paths that attackers could use to breach your environment. Defender for Cloud also highlights the recommendations you need to resolve.

By default, attack paths are sorted by risk level. A risk engine reviews the risk factors of each resource to set its priority. For details on how Defender for Cloud ranks recommendations, see [Risk prioritization](risk-prioritization).

## Prerequisites

Before you begin, make sure your environment meets these requirements:

- [Enable Defender Cloud Security Posture Management (CSPM)](connect-azure-subscription) and turn on [agentless scanning](enable-agentless-scanning-vms).
- **Required roles and permissions**: Security Reader, Security Admin, Reader, Contributor, or Owner.

Note

You might see an empty Attack Path page. Attack paths now focus on real, external threats that can be exploited. This focus helps reduce noise and highlight urgent risks.

**To view attack paths related to containers**:

To see container-related attack paths, complete one of the following setup options: - [Enable agentless container posture extension](tutorial-enable-cspm-plan) in Defender CSPM. - [Enable Defender for Containers](defender-for-containers-enable-plan) and install the relevant agents. This option also lets you [query container data plane workloads in cloud security explorer](how-to-manage-cloud-security-explorer#build-a-query).

- **Required roles and permissions**: Security Reader, Security Admin, Reader, Contributor, or Owner.

## Identify attack paths

You can use Attack path analysis to locate the biggest risks to your environment and to remediate them.

::: zone pivot="azure-portal"

The attack path page shows you an overview of all of your attack paths. You can also see your affected resources and a list of active attack paths.

[![Screenshot of a sample attack path homepage.](media/concept-cloud-map/attack-path-homepage.png)](media/concept-cloud-map/attack-path-homepage.png#lightbox)

**To identify attack paths in the Azure portal**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Attack path analysis**.

    [![Screenshot that shows the attack path analysis page on the main screen.](media/how-to-manage-attack-path/attack-path-blade.png)](media/how-to-manage-attack-path/attack-path-blade.png#lightbox)
3. Select an attack path.
4. Select a node.

    [![Screenshot of the attack path screen that shows you where the nodes are located for selection.](media/how-to-manage-attack-path/node-select.png)](media/how-to-manage-attack-path/node-select.png#lightbox)

    Note

    If you have limited permissions—especially across subscriptions—you might not see full attack path details. This is expected behavior designed to protect sensitive data. To view all details, make sure you have the necessary permissions.
5. Select **Insight** to view the associated insights for that node.

    [![Screenshot of the insights tab for a specific node.](media/how-to-manage-attack-path/insights.png)](media/how-to-manage-attack-path/insights.png#lightbox)
6. Select **Recommendations**.

    [![Screenshot that shows you where to select recommendations on the screen.](media/how-to-manage-attack-path/attack-path-recommendations.png)](media/how-to-manage-attack-path/attack-path-recommendations.png#lightbox)
7. Select a recommendation.
8. [Remediate the recommendation](implement-security-recommendations).

::: zone-end

::: zone pivot="defender-portal"

**To identify attack paths in the Defender portal**:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Navigate to **Exposure Management** &gt; **Attack surface** &gt; **Attack paths**. You will see an overview of your attack paths.

    The attack paths experience provides multiple views:

    - **Overview tab**: View attack paths over time, top 5 choke points, top 5 attack path scenarios, top targets, and top entry points
    - **Attack paths list**: Dynamic, filterable view of all attack paths with advanced filtering capabilities
    - **Choke points**: List of nodes where multiple attack paths converge, flagged as high-risk bottlenecks

    [![Screenshot showing attack path overview in the Defender portal.](media/how-to-manage-attack-path/attack-path-overview-defender-portal.png)](media/how-to-manage-attack-path/attack-path-overview-defender-portal.png#lightbox)

    Note

    In the Defender portal, attack path analysis is part of the broader Exposure Management capabilities, providing enhanced integration with other Microsoft security solutions and unified incident correlation.
3. Select the **Attack paths** tab.

    [![Screenshot that shows the attack path page in the Defender portal.](media/how-to-manage-attack-path/defender-portal/attack-paths-main.png)](media/how-to-manage-attack-path/defender-portal/attack-paths-main.png#lightbox)
4. Use advanced filtering in the Attack paths list to focus on specific attack paths:

    - **Risk level**: Filter by High, Medium, or Low risk attack paths
    - **Asset type**: Focus on specific resource types
    - **Remediation status**: View resolved, in-progress, or pending attack paths
    - **Time frame**: Filter by specific time periods (for example, last 30 days)
5. Select an attack path to view the Attack Path Map, a graph-based view highlighting:

    - **Vulnerable nodes**: Resources with security issues
    - **Entry points**: External access points where attacks could begin
    - **Target assets**: Critical resources attackers are trying to reach
    - **Choke points**: Convergence points where multiple attack paths intersect
6. Select a node to investigate detailed information:

    [![Screenshot of the attack path screen in the Defender portal showing node selection.](media/how-to-manage-attack-path/attack-path-node-defender-portal.png)](media/how-to-manage-attack-path/attack-path-node-defender-portal.png#lightbox)

    Note

    If you have limited permissions—especially across subscriptions—you might not see full attack path details. This is expected behavior designed to protect sensitive data. To view all details, make sure you have the necessary permissions.
7. Review node details including:

    - **MITRE ATT&CK tactics and techniques**: Understanding the attack methodology
    - **Risk factors**: Environmental factors contributing to risk
    - **Associated recommendations**: Security improvements to mitigate the issue
8. Select **Insight** to view the associated insights for that node.
9. Select **Recommendations** to see actionable guidance with remediation status tracking.

    [![Screenshot that shows where to select recommendations in the Defender portal.](media/how-to-manage-attack-path/attack-path-recommendations-defender-portal.png)](media/how-to-manage-attack-path/attack-path-recommendations-defender-portal.png#lightbox)
10. Select a recommendation.
11. [Remediate the recommendation](implement-security-recommendations).

Once an attack path is resolved, it can take up to 24 hours for an attack path to be removed from the list.

::: zone-end

::: zone pivot="azure-portal"

## Remediate attack paths

After you investigate an attack path and review its findings and recommendations, you can start to fix it.

**To remediate an attack path in the Azure portal**:

1. Navigate to **Microsoft Defender for Cloud** &gt; **Attack path analysis**.
2. Select an attack path.
3. Select **Remediation**.

    [![Screenshot of the attack path that shows you where to select remediation.](media/how-to-manage-attack-path/recommendations-tab.png)](media/how-to-manage-attack-path/recommendations-tab.png#lightbox)
4. Select a recommendation.
5. [Remediate the recommendation](implement-security-recommendations).

Once an attack path is resolved, it can take up to 24 hours for an attack path to be removed from the list.

::: zone-end

## Remediate all recommendations for an attack path

Attack path analysis lets you see all recommendations for an attack path in one place. You don't need to check each node one by one.

There are two types of recommendations:

- **Recommendations** - Steps that fix the attack path.
- **Additional recommendations** - Steps that lower risk but don't fully fix the attack path.

::: zone pivot="azure-portal"

**To resolve all recommendations in the Azure portal**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Attack path analysis**.
3. Select an attack path.
4. Select **Remediation**.

    [![Screenshot that shows where to select on the screen to see the attack paths full list of recommendations.](media/how-to-manage-attack-path/bulk-recommendations.png)](media/how-to-manage-attack-path/bulk-recommendations.png#lightbox)
5. Expand **Additional recommendations**.
6. Select a recommendation.
7. [Remediate the recommendation](implement-security-recommendations).

Once an attack path is resolved, it can take up to 24 hours for an attack path to be removed from the list.

::: zone-end

::: zone pivot="defender-portal"

**To resolve all recommendations in the Defender portal**:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Navigate to **Exposure Management** &gt; **Attack path analysis**.
3. Select an attack path.
4. Select **Remediation**.

    Note

    The Defender portal provides enhanced tracking of remediation progress and can correlate remediation activities with broader security operations and incident management workflows.
5. Expand **Additional recommendations**.
6. Select a recommendation.
7. [Remediate the recommendation](implement-security-recommendations).

Once an attack path is resolved, it can take up to 24 hours for an attack path to be removed from the list.

::: zone-end

::: zone pivot="defender-portal"

## Enhanced exposure management capabilities

The Defender portal provides additional capabilities for attack path analysis through its integrated Exposure Management framework:

- **Unified incident correlation**: Attack paths are automatically correlated with security incidents across your Microsoft security ecosystem.
- **Cross-product insights**: Attack path data is integrated with findings from Microsoft Defender for Endpoint, Microsoft Sentinel, and other Microsoft security solutions.
- **Advanced threat intelligence**: Enhanced context from Microsoft threat intelligence feeds to better understand attack patterns and actor behaviors.
- **Integrated remediation workflows**: Streamlined remediation processes that can trigger automated responses across multiple security tools.
- **Executive reporting**: Enhanced reporting capabilities for security leadership with business impact assessments.

These capabilities provide a more comprehensive view of your security posture and enable more effective response to potential threats identified through attack path analysis.

Learn more about [attack paths](concept-attack-path) in Defender for Cloud.

::: zone-end