---
layout: Conceptual
title: Set up continuous export with Azure Policy - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/continuous-export-azure-policy
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
description: Learn how to set up continuous export of Microsoft Defender for Cloud security alerts and recommendations with Azure Policy.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: f1071004-fcc9-48c3-06f8-152697489a73
document_version_independent_id: 0822ae6d-bdff-103e-610a-f77cf74df29c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/continuous-export-azure-policy.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/continuous-export-azure-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/continuous-export-azure-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
platformId: eee612eb-91d9-2271-9e2b-d98f578c8c4c
---

# Set up continuous export with Azure Policy - Microsoft Defender for Cloud | Microsoft Learn

Continuous export of Microsoft Defender for Cloud alerts and recommendations helps you analyze security data in Log Analytics or Azure Event Hubs. You can configure continuous export at scale by using Azure Policy templates.

Tip

Defender for Cloud also supports one-time manual export to a comma-separated values (CSV) file. For instructions, see [Export alerts to CSV](export-alerts-to-csv).

## Prerequisites

- You need a Microsoft Azure subscription. If you don't have one, you can sign up at the [Azure free subscription page](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must enable Microsoft Defender for Cloud on your Azure subscription. For setup instructions, see [Enable Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription).

Required roles and permissions:

- Security Admin or Owner for the resource group
- Write permissions for the target resource.
- If you use the Azure Policy DeployIfNotExist policies, you must have permissions that let you assign policies.
- To export data to Event Hubs, you must have Write permissions on the Event Hubs policy.
- To export to a Log Analytics workspace:

    - If it *has the SecurityCenterFree solution*, you must have a minimum of Read permissions for the workspace solution: `Microsoft.OperationsManagement/solutions/read`.
    - If it *doesn't have the SecurityCenterFree solution*, you must have write permissions for the workspace solution: `Microsoft.OperationsManagement/solutions/action`.

    For more information about workspace solutions, see [Azure Monitor and Log Analytics workspace solutions](/en-us/previous-versions/azure/azure-monitor/insights/solutions).

## Set up continuous export at scale with Azure Policy

Automating monitoring and incident response can reduce investigation and mitigation time.

To deploy continuous export configurations across your organization, use the provided Azure Policy `DeployIfNotExist` policies.

To implement the Azure Policy `DeployIfNotExist` policies for continuous export:

1. Select a policy to apply:

    | Goal | Policy | Policy ID |
    | --- | --- | --- |
    | Continuous export to Event Hubs | [Deploy export to Event Hubs for Microsoft Defender for Cloud alerts and recommendations](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2fcdfcce10-4578-4ecd-9703-530938e4abcb) | cdfcce10-4578-4ecd-9703-530938e4abcb |
    | Continuous export to Log Analytics workspace | [Deploy export to Log Analytics workspace for Microsoft Defender for Cloud alerts and recommendations](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2fffb6f416-7bd2-4488-8828-56585fef2be9) | ffb6f416-7bd2-4488-8828-56585fef2be9 |
2. Select **Assign**.

    [![Screenshot that shows assigning the Azure Policy.](media/continuous-export-azure-policy/export-policy-assign.png)](media/continuous-export-azure-policy/export-policy-assign.png#lightbox)
3. Select each tab and set parameters based on your requirements:

    1. On the Basics tab, set the policy scope. For centralized management, assign the policy to the management group that contains the subscriptions that use this continuous export configuration.
    2. On the Parameters tab, set the resource group name, location, and Event Hubs details.
    3. (Optional) On the Remediation tab, create a remediation task to apply this assignment to existing subscriptions.
4. Review the summary page.
5. Select **Create**.