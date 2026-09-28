---
layout: Conceptual
title: Enable API Security Posture with Defender CSPM - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-api-security-posture
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
description: Discover and secure APIs for API Management, Function Apps, and Logic Apps with prioritized risk insights and API security recommendations.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, references_regions, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 12618e11-6b6c-2338-3477-682af89acb11
document_version_independent_id: 44a75966-5c0f-bb9b-1c07-77993a28efe0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-api-security-posture.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-api-security-posture
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-api-security-posture.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/bf4dbf7f-261c-4ae9-9fee-5989668a780a
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/1c4b5d48-3f26-4bd8-9592-816d9c1a3420
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 5b2a9ba4-692c-1319-8586-ffe57fbd8a66
---

# Enable API Security Posture with Defender CSPM - Microsoft Defender for Cloud | Microsoft Learn

Defender Cloud Security Posture Management (Defender CSPM) gives you visibility into APIs for Azure API Management, Function Apps, and Azure Logic Apps. It helps you detect misconfigurations and vulnerabilities. This article shows you how to enable API security posture, review inventory and findings, and prioritize remediation actions.

## Prerequisites

- Read about [Improve your API security posture](api-security-posture-overview).
- You need a Microsoft Azure subscription. If you don't have one, you can [sign up for an Azure free account](https://azure.microsoft.com/pricing/free-trial).
- Enable [Defender for Cloud on your Azure subscription](connect-azure-subscription).
- Enable Defender Cloud Security Posture Management (Defender CSPM) on your Azure subscription. For setup instructions, see [Enable Defender CSPM](tutorial-enable-cspm-plan).
- To scan for sensitive information in APIs onboarded to Defender CSPM, [enable sensitive data discovery](tutorial-enable-cspm-plan#enable-the-components-of-the-defender-cspm-plan).
- The **Subscription Owner** must enable the CSPM plan to access all features.
- Ensure the APIs you want to protect are deployed in [Azure API Management](/en-us/azure/api-management/api-management-key-concepts), [Function Apps](/en-us/azure/azure-functions/functions-overview), or [Logic Apps](/en-us/azure/logic-apps/logic-apps-overview).

## Cloud and region support

API Security Posture Management within Defender CSPM is available in the Azure commercial cloud, in the following regions:

- Asia (Southeast Asia, East Asia)
- Australia (Australia East, Australia Southeast, Australia Central, Australia Central 2)
- Brazil (Brazil South, Brazil Southeast)
- Canada (Canada Central, Canada East)
- Europe (West Europe, North Europe)
- France (France Central, France South)
- Germany (Germany West Central, Germany North)
- India (Central India, South India, West India)
- Italy (Italy North)
- Japan (Japan East, Japan West)
- Korea (Korea Central, Korea South)
- Norway (Norway East, Norway West)
- South Africa (South Africa North, South Africa West)
- Sweden (Sweden Central, Sweden South)
- Switzerland (Switzerland North, Switzerland West)
- UAE (UAE Central, UAE North)
- UK (UK South, UK West)
- US (East US, East US 2, West US, West US 2, West US 3, Central US, North Central US, South Central US, West Central US, East US 2 EUAP, Central US EUAP)

Review the latest cloud support information for Defender for Cloud plans and features in the [cloud support matrix](support-matrix-defender-for-cloud).

## API support

Use the following table to review supported tiers and API types for API security posture management.

| Feature | Supported |
| --- | --- |
| Availability | **Azure API Management:** This feature is available in the Premium, Standard, Basic, and Developer tiers of Azure API Management. It doesn't support APIs that are exposed through the API Management [self-hosted gateway](/en-us/azure/api-management/self-hosted-gateway-overview) or managed through API Management [workspaces](/en-us/azure/api-management/workspaces-overview). **Azure App Services:** Supported Azure Function App hosting tiers include Premium, Elastic Premium, Dedicated (App Service), and App Service Environment (ASE). For Azure Logic Apps, supported tiers include Standard (Single-Tenant) and App Service Environment (ASE). Consumption tier Function Apps, Consumption tier Logic Apps, and Azure Arc-enabled Logic Apps aren't supported. |
| API types | Support only for REST APIs. |

## Enable API security posture management extension

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Locate the Defender CSPM plan and select **Settings**.
5. Enable **API security posture management**.

    [![Screenshot of Enable API security posture management.](media/enable-api-security-posture/enable-api-security-posture-management.png)](media/enable-api-security-posture/enable-api-security-posture-management.png#lightbox)
6. Select **Continue**.
7. Select **Save**.

A notification message confirming that the settings were saved successfully appears. After you enable the feature, APIs start onboarding and appear in your Defender for Cloud Inventory within a few hours.

## View API inventory

APIs onboarded to the Defender CSPM plan appear in the API security dashboard under **Workload protection** and Microsoft Defender for Cloud **Inventory**.

1. Go to the Cloud Security section of the Defender for Cloud menu and select **API security** under **Advanced Workload protections**.

    [![Screenshot of the API security dashboard.](media/enable-api-security-posture/select-api-security.png)](media/enable-api-security-posture/select-api-security.png#lightbox)
2. The dashboard shows the number of onboarded APIs, broken down by API collections, endpoints, and Azure API Management services. It includes a summary of APIs onboarded for threat detection security coverage by using the Defender for APIs workload protections plan.
3. Apply the filter **Defender plan == Defender CSPM** to view the APIs onboarded to the Defender CSPM plan.

    [![Screenshot of filtered APIs for Defender CSPM plan for posture.](media/enable-api-security-posture/filter-defender-cspm.png)](media/enable-api-security-posture/filter-defender-cspm.png#lightbox)
4. Select **OK**.
5. Select an API operation of interest to review the security findings for specific API operations.

    [![Screenshot of API collection details page.](media/enable-api-security-posture/api-collection-details.png)](media/enable-api-security-posture/api-collection-details.png#lightbox)

### API endpoint detailed findings

The API endpoint details page shows the following findings for each operation:

1. **Sensitive Information Type**: Provides details on the sensitive information exposed in API URL paths, query parameters, request bodies, and response bodies based on supported data types, along with the source of the information type found.
2. **Additional Information**: In the case of API response bodies, this field shows which HTTP response codes contained sensitive information (such as 2xx, 3xx, 4xx).

Review API security posture findings along with your API inventory in the Microsoft Defender for Cloud Inventory experience.

## Investigate API security recommendations

Defender for Cloud continuously assesses API endpoints for misconfigurations and vulnerabilities, including authentication flaws and inactive APIs. It generates security recommendations with associated risk factors like external exposure and data sensitivity risks. Defender for Cloud calculates the importance of the security recommendations based on these risk factors. To learn more, see [risk-based security recommendations](security-recommendations#understanding-risk-prioritization).

To investigate your API security posture recommendations:

1. Go to the Defender for Cloud main menu and select **Recommendations**.
2. Select the **Group by Title** toggle to organize recommendations.
3. Filter by **Resource Type**, for example, **API Management Operation** or **API Endpoint**, or filter by **Recommendation Name** to narrow down API-related recommendations to target specific API security problems.

For the full list of API-related recommendations, see the [API security recommendations reference](recommendations-reference-api) in the Defender for Cloud recommendation reference guide.

## Explore API risks and remediate with attack path analysis

The [cloud security explorer](concept-attack-path#what-is-cloud-security-explorer) helps you identify potential security risks in your cloud environment by querying the [cloud security graph](concept-attack-path#what-is-the-cloud-security-graph).

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. Use the built-in query template to quickly identify APIs with security insights.

    [![Screenshot of Cloud Security Explorer with API security insights query template.](media/enable-api-security-posture/cloud-security-explorer.png)](media/enable-api-security-posture/cloud-security-explorer.png#lightbox)
4. Alternatively, [build a custom query with Cloud Security Explorer](how-to-manage-cloud-security-explorer) to find API risks and see API endpoints connected to backend compute or data stores. For example, you can see API endpoints routing traffic to virtual machines with remote code vulnerabilities.

    [![Screenshot of custom query in Cloud Security Explorer.](media/enable-api-security-posture/custom-query.png)](media/enable-api-security-posture/custom-query.png#lightbox)

Attack path analysis in Defender for Cloud addresses security problems that pose immediate threats to your cloud applications and environments. [Identify and remediate API-led attack paths](how-to-manage-attack-path) to address your most critical API risks that can significantly threaten your organization.

1. In the Defender for Cloud menu, go to **Attack path analysis**.
2. Filter by resource type **API Management operation** to investigate API-related attack paths.

    [![Screenshot of Attack path analysis filtered by API Management operation.](media/enable-api-security-posture/filter-resource-type.png)](media/enable-api-security-posture/filter-resource-type.png#lightbox)
3. View the security recommendations for your API endpoints in scope and remediate the recommendations to protect your APIs from high-risk attack surfaces.

    [![Screenshot of API security recommendations in Attack path analysis.](media/enable-api-security-posture/attack-path.png)](media/enable-api-security-posture/attack-path.png#lightbox)

## Offboard API security posture protection

You can't offboard individual APIs that are part of the Defender CSPM plan. To offboard all APIs from the Defender CSPM plan, go to the Defender CSPM Plan Settings page and disable the API posture extension.

[![Screenshot of Disable API security posture management.](media/enable-api-security-posture/offboard-api-security-posture.png)](media/enable-api-security-posture/offboard-api-security-posture.png#lightbox)

Select **Continue** and then **Save** to confirm. Disabling the API posture extension offboards all APIs from the Defender CSPM plan and disables API security posture management.