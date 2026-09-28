---
layout: Conceptual
title: Set up continuous export in the Azure portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/continuous-export
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
description: Learn how to set up continuous export of Microsoft Defender for Cloud security alerts and recommendations.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 176c2ed3-b942-1ba5-ce1b-996bebfe3b0e
document_version_independent_id: 4ce99e65-ae8f-f0ce-72d5-561251a76708
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/continuous-export.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/continuous-export
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/continuous-export.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
platformId: f7623d76-1f9e-3c35-1f4f-a8e86f81b4ef
---

# Set up continuous export in the Azure portal - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud generates security alerts and recommendations. You can export this data to Log Analytics in Azure Monitor, to Azure Event Hubs, or to another Security Information and Event Management (SIEM), Security Orchestration Automated Response (SOAR), or IT classic [deployment model solution](export-to-siem). You can stream data as it's generated, or you can send scheduled snapshots of new data.

This article explains how to set up continuous export to a Log Analytics workspace or an event hub in Azure.

Tip

Defender for Cloud also offers a one-time, manual export to a comma-separated values (CSV) file. Learn how to [download a CSV file](export-alerts-to-csv).

## Prerequisites

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
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

## Create a continuous export configuration

You can set up continuous export in the Microsoft Defender for Cloud pages in the Azure portal, by using the REST API, or at scale by using Azure Policy templates.

**To set up a continuous export to Log Analytics or Azure Event Hubs by using the Azure portal**:

1. On the Defender for Cloud resource menu, select **Environment settings**.
2. Select the subscription that you want to configure data export for.
3. In the resource menu under **Settings**, select **Continuous export**.

    [![Screenshot that shows the export options in Microsoft Defender for Cloud.](media/continuous-export/continuous-export-options-page.png)](media/continuous-export/continuous-export-options-page.png#lightbox)

    Export options appear. There's a tab for each target: Event Hubs or Log Analytics workspace.
4. Select the data type that you want to export, and then choose filters for that type. For example, you can export only high-severity alerts.
5. Select the export frequency:

    - **Streaming**. Assessments are sent when a resource’s health state is updated (if no updates occur, no data is sent).
    - **Snapshots**. A snapshot of the current state of the selected data types that are sent once a week per subscription. To identify snapshot data, look for the field **IsSnapshot**.

    If your selection includes one of these recommendations, you can include the vulnerability assessment findings with those recommendations:

    - [SQL databases should have vulnerability findings resolved](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/82e20e14-edc5-4373-bfc4-f13121257c37)
    - [SQL servers on machines should have vulnerability findings resolved](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/f97aa83c-9b63-4f9a-99f6-b22c4398f936)
    - [Container registry images should have vulnerability findings resolved (powered by Qualys)](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/dbd0cb49-b563-45e7-9724-889e799fa648)
    - [Machines should have vulnerability findings resolved](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/1195afff-c881-495e-9bc5-1486211ae03f)
    - [System updates should be installed on your machines](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/4ab6e3c5-74dd-8b35-9ab9-f61b30875b27)

    To include vulnerability assessment findings with the preceding vulnerability-related recommendations, set **Include security findings** to **Yes**.

    ![Screenshot that shows the Include security findings toggle in a continuous export configuration.](media/continuous-export/include-security-findings-toggle.png)
6. Under **Export target**, choose where you'd like the data saved. Data can be saved in a target of a different subscription (for example, in a central Event Hubs instance or in a central Log Analytics workspace).

    You can also send the data to an [event hub or Log Analytics workspace in a different tenant](benefits-of-continuous-export#export-data-to-an-event-hub-or-log-analytics-workspace-in-another-tenant)
7. Select **Save**.

Note

Log Analytics supports only records that are up to 32 KB in size. When the data limit is reached, an alert displays the message **Data limit has been exceeded**.