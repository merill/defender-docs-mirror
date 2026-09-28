---
layout: Conceptual
title: Connect your Azure Subscriptions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/connect-azure-subscription
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
description: Learn how to connect your Azure subscriptions to Microsoft Defender for Cloud and protect your cloud-based applications.
ms.topic: install-set-up-deploy
ms.date: 2025-10-23T00:00:00.0000000Z
ms.custom: mode-other
ai-usage: ai-assisted
locale: en-us
document_id: 08cb13c3-e2c4-ef01-a6b4-77316b6a9e72
document_version_independent_id: bba6ed63-c94b-c545-7762-7ac0c732d5a8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/connect-azure-subscription.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/connect-azure-subscription
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/connect-azure-subscription.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 2e607d03-c195-499e-910b-bb5e829b6782
---

# Connect your Azure Subscriptions - Microsoft Defender for Cloud | Microsoft Learn

In this guide, you learn how to enable Microsoft Defender for Cloud on your Azure subscription.

Microsoft Defender for Cloud is a cloud-native application protection platform (CNAPP) with a set of security measures and practices designed to protect your cloud-based applications end-to-end by combining these capabilities:

- A development security operations (DevSecOps) solution that unifies security management at the code level across multicloud and multiple-pipeline environments.
- A cloud security posture management (CSPM) solution that surfaces actions you can take to prevent breaches.
- A cloud workload protection platform (CWPP) with specific protections for servers, containers, storage, databases, and other workloads.

Defender for Cloud includes foundational CSPM capabilities and access to [Microsoft Defender XDR](/en-us/microsoft-365/security/defender/microsoft-365-defender) for free. You can add other paid plans to secure all aspects of your cloud resources. You can try Defender for Cloud for free for the first 30 days, or until the usage limit for certain plans is reached, whichever comes first. After [reaching the usage limit or once the 30-day trial ends](free-trial), charges begin based on the plans enabled in your environment. To learn more about these plans, their usage limits, and associated costs, see the Defender for Cloud [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

Important

Malware scanning in Defender for Storage isn't included for free in the first 30-day trial and is charged from the first day in accordance with the pricing scheme available on the Defender for Cloud [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/).

Defender for Cloud helps you find and fix security vulnerabilities. It also applies access and application controls to block malicious activity, detects threats using analytics and intelligence, and responds quickly when under attack.

## Prerequisites

- To view information related to a resource in Defender for Cloud, you must be assigned the Owner, Contributor, or Reader role for the subscription or the resource group where the resource is located.

## Enable Defender for Cloud on your Azure subscription

Tip

To enable Defender for Cloud on all subscriptions within a management group, see [Enable Defender for Cloud on multiple Azure subscriptions](onboard-management-group).

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.

    [![Screenshot of the Azure portal with Microsoft Defender for Cloud selected.](media/get-started/defender-for-cloud-search.png)](media/get-started/defender-for-cloud-search.png#lightbox)

    The Defender for Cloud overview page opens.

    [![Screenshot of the Defender for Cloud overview dashboard.](media/overview-page/overview.png)](media/overview-page/overview.png#lightbox)

Defender for Cloud is now enabled on your subscription, and you have access to the basic features provided by Defender for Cloud. These features include:

- The [Foundational Cloud Security Posture Management (CSPM)](concept-cloud-security-posture-management) plan.
- [Recommendations](security-policy-concept).
- Access to the [Asset inventory](asset-inventory).
- [Workbooks](custom-dashboards-azure-workbooks).
- [Secure score](secure-score-security-controls).
- [Regulatory compliance](assign-regulatory-compliance-standards) with the [Microsoft cloud security benchmark](concept-regulatory-compliance).

The Defender for Cloud overview page provides a unified view into the security posture of your hybrid cloud workloads. It helps you discover and assess the security of your workloads and identify and mitigate risks. For more information, see [Microsoft Defender for Cloud's overview page](overview-page).

You can view and filter your list of subscriptions from the subscriptions menu. Defender for Cloud adjusts the overview page display to reflect the security posture of the selected subscriptions.

Within minutes of launching Defender for Cloud for the first time, you might see:

- **Recommendations** for ways to improve the security of your connected resources.
- An inventory of your resources that Defender for Cloud assesses along with the security posture of each.

## Enable all paid plans on your subscription

To enable all of Defender for Cloud's protections, you need to enable the plans for the workloads you want to protect.

Note

- You can enable **Microsoft Defender for Storage accounts**, **Microsoft Defender for SQL**, and **Microsoft Defender for open-source relational databases** at either the subscription level or resource level.
- The Microsoft Defender for Cloud plans available at the workspace level are: **Microsoft Defender for Servers** and **Microsoft Defender for SQL servers on machines**.

Important

Microsoft Defender for SQL is a subscription-level bundle that uses either a default or custom workspace.

When you enable Defender plans on an entire Azure subscription, the protections apply to all other resources in the subscription.

**To enable additional paid plans on a subscription**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.

    ![Screenshot that shows where to navigate to, to select environmental settings from.](media/get-started/environmental-settings.png)
4. Select the subscription or workspace that you want to protect.
5. Select **Enable all** to enable all of the plans for Defender for Cloud.

    [![Screenshot that shows where the enable button is located on the plans page.](media/get-started/enable-all-plans.png)](media/get-started/enable-all-plans.png#lightbox)
6. Select **Save**.

All of the plans are turned on, and the monitoring components required by each plan are deployed to the protected resources.

If you want to disable any of the plans, toggle the individual plan to **off**. The extensions used by the plan aren't uninstalled, but after a short time, the extensions stop collecting data.

Tip

To enable Defender for Cloud on all subscriptions within a management group, see [Enable Defender for Cloud on multiple Azure subscriptions](onboard-management-group).

## View your current coverage

Defender for Cloud provides access to [workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that provide insights into your security posture.

The [coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) helps you understand your current coverage by showing which plans are enabled on your subscriptions and resources.

## Integrate with Microsoft Defender XDR

When you enable Defender for Cloud, its alerts automatically integrate into the Microsoft Defender Portal.

The integration between Microsoft Defender for Cloud and Microsoft Defender XDR brings your cloud environments into Microsoft Defender XDR. With Defender for Cloud's alerts and cloud correlations integrated into Microsoft Defender XDR, SOC teams can now access all security information from a single interface.

Learn more about Defender for Cloud's [alerts in Microsoft Defender XDR](concept-integration-365).