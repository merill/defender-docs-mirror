---
layout: Conceptual
title: Protect your APIs with Defender for APIs - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-apis-deploy
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
description: Learn how to enable and deploy the Defender for APIs plan in the Microsoft Defender for Cloud portal.
ms.topic: concept-article
ms.date: 2025-09-28T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 43e07493-dc8d-f6d0-3408-90ed69643cb6
document_version_independent_id: c56ad6c7-7c25-2ec9-6d55-09148da08edc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-apis-deploy.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-apis-deploy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-apis-deploy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/bf4dbf7f-261c-4ae9-9fee-5989668a780a
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/1c4b5d48-3f26-4bd8-9592-816d9c1a3420
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: a29253e2-c6ff-7a2a-4445-e52bfad39e53
---

# Protect your APIs with Defender for APIs - Microsoft Defender for Cloud | Microsoft Learn

Defender for APIs in Microsoft Defender for Cloud offers full lifecycle protection, detection, and response coverage for APIs.

Defender for APIs helps you to gain visibility into business-critical APIs. You can investigate and improve your API security posture, prioritize vulnerability fixes, and quickly detect active real-time threats.

This article describes how to enable and onboard the Defender for APIs plan in the Defender for Cloud portal. Alternately, you can [enable Defender for APIs within an API Management instance](/en-us/azure/api-management/protect-with-defender-for-apis) in the Azure portal.

Learn more about the [Microsoft Defender for APIs](defender-for-apis-introduction) plan in the Microsoft Defender for Cloud. Learn more about [Defender for APIs](defender-for-apis-introduction).

## Prerequisites

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- Review [Defender for APIs support, permissions, and requirements](defender-for-apis-prepare) before you begin deployment.
- You enable Defender for APIs at the subscription level.
- Ensure that APIs you want to secure are published in [Azure API management](/en-us/azure/api-management/api-management-key-concepts). Follow [these instructions](/en-us/azure/api-management/get-started-create-service-instance) to set up Azure API Management.
- You must select a plan that grants entitlement appropriate for the API traffic volume in your subscription to receive the most optimal pricing. By default, subscriptions are opted into "Plan 1", which can lead to unexpected overages if your subscription has API traffic higher than the [one million API calls entitlement](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/18).

## Enable the Defender for APIs plan

When selecting a plan, consider these points:

- Defender for APIs protects only those APIs that are onboarded to Defender for APIs. This means you can activate the plan at the subscription level, and complete the second step of onboarding by fixing the onboarding recommendation.
- Defender for APIs has five pricing plans, each with a different entitlement limit and monthly fee. The billing is done at the subscription level.
- Billing is applied to the entire subscription based on the total amount of API traffic monitored over the month for the subscription.
- The API traffic counted towards the billing is reset to 0 at the start of each month (every billing cycle).
- The overages are computed on API traffic exceeding the entitlement limit per plan selection during the month for your entire subscription.

To select the best plan for your subscription from the Microsoft Defender for Cloud [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator). Follow these steps to choose the plan that matches your subscriptions’ API traffic requirements:

1. Sign into the [portal](https://portal.azure.com/), and in Defender for Cloud, select **Environment settings**.
2. Select the subscription that contains the managed APIs that you want to protect.

    [![Screenshot that shows where to select Environment settings.](media/defender-for-apis-entitlement-plans/select-environment-settings.png)](media/defender-for-apis-entitlement-plans/select-environment-settings.png#lightbox)
3. Select **Details** under the pricing column for the APIs plan.

    [![Screenshot that shows where to select API details.](media/defender-for-apis-entitlement-plans/select-api-details.png)](media/defender-for-apis-entitlement-plans/select-api-details.png#lightbox)
4. Select the plan that is suitable for your subscription.
5. Select **Save**.

## Select the optimal plan based on historical Azure API Management API traffic usage

You must select a plan that grants entitlement appropriate for the API traffic volume in your subscription to receive the most optimal pricing. By default, subscriptions are opted into **Plan 1**, which can lead to unexpected overages if your subscription has API traffic higher than the [one million API calls entitlement](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/18).

**To estimate the monthly API traffic in Azure API Management:**

1. Navigate to the Azure API Management portal and select **Metrics** under the Monitoring menu bar item.

    [![Screenshot that shows where to select metrics.](media/defender-for-apis-entitlement-plans/select-metrics.png)](media/defender-for-apis-entitlement-plans/select-metrics.png#lightbox)
2. Select the time range as **Last 30 days**.
3. Select and set the following parameters:

    1. Scope: **Azure API Management Service Name**
    2. Metric Namespace: **API Management service standard metrics**
    3. Metric = **Requests**
    4. Aggregation = **Sum**
4. After setting the above parameters, the query will automatically run, and the total number of requests for the past 30 days appears at the bottom of the screen. In the screenshot example, the query results in 414 total number of requests.

    [![Screenshot that shows metrics results.](media/defender-for-apis-entitlement-plans/metrics-results.png)](media/defender-for-apis-entitlement-plans/metrics-results.png#lightbox)

    Note

    These instructions are for calculating the usage per Azure API management service. To calculate the estimated traffic usage for *all* API management services within the Azure subscription, change the **Scope** parameter to each Azure API management service within the Azure subscription, re-run the query, and sum the query results.

If you don't have access to run the metrics query, reach out to your internal Azure API Management administrator or your Microsoft account manager.

Note

After enabling Defender for APIs, onboarded APIs take up to 50 minutes to appear in the **Recommendations** tab. Security insights are available in the **Workload protections** &gt; **API security** dashboard within 40 minutes of onboarding.

## Onboard APIs

1. In the Defender for Cloud portal, select **Recommendations**.
2. Search for *Defender for APIs*.
3. Under **Enable enhanced security features** select the security recommendation **Azure API Management APIs should be onboarded to Defender for APIs**:

    [![Screenshot that shows how to turn on the Defender for APIs plan from the recommendation.](media/defender-for-apis-deploy/api-recommendations.png)](media/defender-for-apis-deploy/api-recommendations.png#lightbox)
4. In the recommendation page you can review the recommendation severity, update interval, description, and remediation steps.
5. Review the resources in scope for the recommendations:

    - **Unhealthy resources**: Resources that aren't onboarded to Defender for APIs.
    - **Healthy resources**: API resources that are onboarded to Defender for APIs.
    - **Not applicable resources**: API resources that aren't applicable for protection.
6. In **Unhealthy resources** select the APIs that you want to protect with Defender for APIs.
7. Select **Fix**:

    [![Screenshot that shows the recommendation details for turning on the plan.](media/defender-for-apis-deploy/api-recommendation-details.png)](media/defender-for-apis-deploy/api-recommendation-details.png#lightbox)
8. In **Fixing resources** review the selected APIs and select **Fix resources**:

    [![Screenshot that shows how to fix unhealthy resources.](media/defender-for-apis-deploy/fix-resources.png)](media/defender-for-apis-deploy/fix-resources.png#lightbox)
9. Verify that remediation was successful:

    [![Screenshot that confirms that remediation was successful.](media/defender-for-apis-deploy/fix-resources-confirm.png)](media/defender-for-apis-deploy/fix-resources-confirm.png#lightbox)

## Track onboarded API resources

After onboarding the API resources, you can track their status in the Defender for Cloud portal &gt; **Workload protections** &gt; **API security**:

[![Screenshot that shows how to track onboarded API resources.](media/defender-for-apis-deploy/track-resources.png)](media/defender-for-apis-deploy/track-resources.png#lightbox)

You can also navigate to other collections to learn about what types of insights or risks might exist in the inventory:

[![Screenshot showing the overview of API collections.](media/defender-for-apis-deploy/collection-overview.png)](media/defender-for-apis-deploy/collection-overview.png#lightbox)

## View your current coverage

Defender for Cloud provides access to [workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that provide insights into your security posture.

The [coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) helps you understand your current coverage by showing which plans are enabled on your subscriptions and resources.