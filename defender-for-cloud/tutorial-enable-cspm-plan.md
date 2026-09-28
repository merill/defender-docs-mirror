---
layout: Conceptual
title: Protect your resources with Defender CSPM - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/tutorial-enable-cspm-plan
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
description: Learn how to enable Defender CSPM on your Azure subscription for Microsoft Defender for Cloud and enhance your security posture.
ms.topic: install-set-up-deploy
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5a47865b-1719-e450-1bfc-c67d8610e23b
document_version_independent_id: 76044edf-7b19-0991-0ed3-a3c8c5d95ceb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/tutorial-enable-cspm-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/tutorial-enable-cspm-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/tutorial-enable-cspm-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 4a7662b5-290d-84dc-2bbb-5c7a66830b97
---

# Protect your resources with Defender CSPM - Microsoft Defender for Cloud | Microsoft Learn

Defender Cloud Security Posture Management (CSPM) in Microsoft Defender for Cloud provides you with hardening guidance that helps you efficiently and effectively improve your security. CSPM also gives you visibility into your current security situation.

Defender for Cloud continually assesses your resources, subscriptions, and organization for security issues. Defender for Cloud shows you your security posture with the secure score. The secure score is an aggregated score of the security findings that tells you about your current security situation. The higher the score, the lower the identified risk level.

Foundational CSPM provides free security posture management capabilities in Defender for Cloud.

Important

Starting October 27, 2026, Foundational CSPM will move to an opt-in model and will no longer be enabled by default for new Azure subscriptions. The free plan will continue to be available at no cost and can be enabled at any time based on your organization's needs. Existing subscriptions that already have Foundational CSPM enabled will remain enabled unless you turn off the plan. For more information, see [Opt in to Foundational CSPM](foundational-cspm-opt-in).

You can enable the **Defender CSPM** plan, which offers extra protections for your environments such as governance, regulatory compliance, cloud security explorer, attack path analysis, and agentless scanning for machines.

Note

Agentless scanning requires the **Subscription Owner** to enable the Defender CSPM plan. Anyone with a lower level of authorization can enable the Defender CSPM plan, but the agentless scanner isn't enabled by default due to a lack of required permissions that are only available to the Subscription Owner. In addition, attack path analysis and security explorer don't populate with vulnerabilities because the agentless scanner is disabled.

For availability and to learn more about the features offered by each plan, see the [Defender CSPM plan options](concept-cloud-security-posture-management).

You can learn more about Defender CSPM's pricing on [the pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/).

## Prerequisites

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- Connect your [non-Azure machines](quickstart-onboard-machines), [AWS accounts](quickstart-onboard-aws), or [GCP projects](quickstart-onboard-gcp).
- To access all of the features available from the CSPM plan, the **Subscription Owner** must enable the plan.

## Enable the Defender CSPM plan

Foundational CSPM provides free posture management capabilities. To access the additional capabilities provided by Defender CSPM, enable the Defender CSPM plan on your subscription.

**To enable the Defender CSPM plan on your subscription**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant Azure subscription, AWS account, or GCP project.
5. On the Defender plans page, toggle the Defender CSPM plan to **On**.
6. Select **Save**.

## Enable the components of the Defender CSPM plan

Once the Defender CSPM plan is enabled on your subscription, you have the ability to enable the individual components of the Defender CSPM plan:

- **[Agentless scanning for machines](concept-agentless-data-collection)**: Scans your machines for installed software and vulnerabilities without relying on agents or impacting machine performance. You can disable the agentless scanner or add exclusion tags to your subscription.
- **[Agentless discovery for Kubernetes](defender-for-containers-architecture#how-does-agentless-discovery-for-kubernetes-in-azure-work)**: API-based discovery of information about Kubernetes cluster architecture, workload objects, and setup. Required for Kubernetes inventory, identity, and network exposure detection, risk hunting as part of the cloud security explorer. This extension is required for attack path analysis (Defender CSPM only).
- **[Agentless container vulnerability assessments](agentless-vulnerability-assessment-azure)**: Provides vulnerability management for images stored in your container registries.
- **[Sensitive data discovery](concept-data-security-posture-prepare)**: Sensitive data discovery automatically discovers managed cloud data resources containing sensitive data at scale. This feature accesses your data, it's agentless, uses smart sampling scanning, and integrates with Microsoft Purview sensitive information types and labels.
- **[Cloud infrastructure entitlement management (CIEM)](permissions-management)** - Insights into Cloud Infrastructure Entitlement Management. CIEM ensures appropriate and secure identities and access rights in cloud environments. It helps understand access permissions to cloud resources and associated risks. Setup and data collection might take up to 24 hours.
- **[Serverless protection](serverless-protection)** - Detects and assesses serverless resources such as Azure Web Apps, Azure Functions, and AWS Lambda for security risks without requiring agents to be installed. It identifies misconfigurations, vulnerabilities, and insecure dependencies, providing remediation guidance to improve security posture.
- **[Serverless Containers](posture-for-serverless-containers)** - Assesses Azure Container Apps, Azure Container Instances, and AWS ECS on Fargate workloads in Defender CSPM experiences such as inventory, recommendations, and attack path analysis. To get full access to all Serverless Containers features, enable **Registry access** in the Defender CSPM plan settings.

**To enable the components of the Defender CSPM plan**:

1. On the Defender plans page, select **Settings**.

    [![Screenshot showing the Defender plans page where you select the Settings option.](media/tutorial-enable-cspm-plan/cspm-settings.png)](media/tutorial-enable-cspm-plan/cspm-settings.png#lightbox)
2. Select **On** for each component to enable it.
3. (Optional) For agentless scanning, select **Edit configuration**.

    [![Screenshot showing where you select Edit configuration.](media/tutorial-enable-cspm-plan/cspm-configuration.png)](media/tutorial-enable-cspm-plan/cspm-configuration.png#lightbox)

    1. Enter a tag name and tag value for any machines to be excluded from scans.
    2. Select **Apply**.
4. Select **Continue**.

For code to cloud contextualization capabilities and automated developer remediation workflows that come with your Defender CSPM plan at no extra cost, [connect your DevOps environments](defender-for-devops-introduction) to Defender for Cloud.

## View your current coverage

Defender for Cloud provides access to [workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that provide insights into your security posture.

The [coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) helps you understand your current coverage by showing which plans are enabled on your subscriptions and resources.