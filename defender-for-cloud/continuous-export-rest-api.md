---
layout: Conceptual
title: Set up continuous export with REST API - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/continuous-export-rest-api
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
description: Configure continuous export to Log Analytics or Event Hubs by using the REST API, including destination options and automation parameters.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 846535a1-e81f-983b-ff2a-900360967375
document_version_independent_id: fa9a59cd-a00a-5771-3d02-522c5e63fa65
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/continuous-export-rest-api.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/continuous-export-rest-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/continuous-export-rest-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 96f041ba-47d2-00b7-6057-f4ff4bb0760e
---

# Set up continuous export with REST API - Microsoft Defender for Cloud | Microsoft Learn

Continuous export of Microsoft Defender for Cloud alerts and recommendations helps you analyze data in Log Analytics or Azure Event Hubs. You can set up and manage continuous export in Defender for Cloud by using the REST API.

Tip

Defender for Cloud also supports one-time manual export to a comma-separated values (CSV) file. For instructions, see [Export alerts to CSV](export-alerts-to-csv).

## Prerequisites

Before setting up continuous export with the REST API, make sure you meet the following requirements:

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.

Required roles and permissions:

- Security Admin or Owner for the resource group
- Write permissions for the target resource.
- If you use the [Azure Policy DeployIfNotExist policies](continuous-export-azure-policy), you must have permissions that let you assign policies.
- To export data to Event Hubs, you must have Write permissions on the Event Hubs policy.
- To export to a Log Analytics workspace:

    - If it *has the SecurityCenterFree solution*, you must have a minimum of Read permissions for the workspace solution: `Microsoft.OperationsManagement/solutions/read`.
    - If it *doesn't have the SecurityCenterFree solution*, you must have write permissions for the workspace solution: `Microsoft.OperationsManagement/solutions/action`.

        Learn more about [Azure Monitor and Log Analytics workspace solutions](/en-us/previous-versions/azure/azure-monitor/insights/solutions).

## Set up continuous export by using the REST API

You can set up and manage continuous export by using the Microsoft Defender for Cloud [automations API](/en-us/rest/api/defenderforcloud-composite/automations?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true). Use this API to create or update rules for exporting to any of the following destinations:

- Azure Event Hubs
- Log Analytics workspace
- Azure Logic Apps

You also can send the data to an [event hub or Log Analytics workspace in a different tenant](benefits-of-continuous-export#export-data-to-an-event-hub-or-log-analytics-workspace-in-another-tenant).

Note

If you’re configuring continuous export by using the REST API, always include the parent with the findings.

Here are options available only through the API:

- **Greater volume**: You can create multiple export configurations on a single subscription by using the API. The **Continuous Export** page in the Azure portal supports only one export configuration per subscription.
- **Additional features**: The API offers parameters that aren't shown in the Azure portal. For example, you can add tags to your automation resource and define your export based on a wider set of alert and recommendation properties than the ones that are offered on the **Continuous export** page in the Azure portal.
- **Focused scope**: The API offers you a more granular level for the scope of your export configurations. When you define an export by using the API, you can define it at the resource group level. If you're using the **Continuous export** page in the Azure portal, you must define it at the subscription level.

    Tip

    These API-only options aren't shown in the Azure portal. If you use them, a banner informs you that other configurations exist.