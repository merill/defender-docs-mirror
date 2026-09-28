---
layout: Conceptual
title: Enable Defender for Storage by Using an Azure Built-in Policy - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-policy-enablement
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
description: Learn how to enable and configure the Microsoft Defender for Storage plan at scale by using an Azure built-in policy.
ms.topic: install-set-up-deploy
ms.date: 2025-06-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 4eae16b3-855c-66b7-cf36-40bfac3fe880
document_version_independent_id: 10ced7df-613e-4eb9-4bb6-55f904c41abd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-policy-enablement.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-policy-enablement
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-policy-enablement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: f9bdd4c0-723c-11b3-fddf-1acd5b851a5d
---

# Enable Defender for Storage by Using an Azure Built-in Policy - Microsoft Defender for Cloud | Microsoft Learn

You should enable Microsoft Defender for Storage via a built-in policy. This method facilitates enablement at scale. It also ensures that a consistent security policy is applied across all existing and future storage accounts within the defined scope, such as entire management groups. This approach keeps the storage accounts protected with Defender for Storage according to your organization's defined configuration.

Tip

You can always [configure specific storage accounts](advanced-configurations-for-malware-scanning#override-defender-for-storage-subscription-level-settings) with custom settings that differ from the settings configured at the subscription level. That is, you can override subscription-level settings.

## Azure built-in policy

To enable and configure Defender for Storage at scale by using an Azure built-in policy, follow these steps:

1. Sign in to the Azure portal and go to the **Policy** dashboard.
2. On the left menu, select **Definitions**.
3. In the **Security Center** category, search for and then select **Configure Microsoft Defender for Storage to be enabled**.

    This policy enables all Defender for Storage capabilities: activity monitoring, malware scanning, and sensitive-data threat detection. You can also get it here: [List of built-in policy definitions](/en-us/azure/governance/policy/samples/built-in-policies#security-center). If you want to enable a policy without the configurable features, use **Configure basic Microsoft Defender for Storage to be enabled (Activity Monitoring only)**.

    [![Screenshot that shows where to select policy definitions.](media/defender-for-storage-malware-scan/policy-definitions.png)](media/defender-for-storage-malware-scan/policy-definitions.png#lightbox)
4. Select the policy and review it.
5. Select **Assign**. You can fine-tune, edit, and add custom rules to the policy.

    [![Screenshot that shows where to assign a policy.](media/defender-for-storage-malware-scan/policy-assign.png)](media/defender-for-storage-malware-scan/policy-assign.png#lightbox)
6. After you finish reviewing the policy details, select **Review + create**.
7. Select **Create** to assign the policy.

Tip

You can configure malware scanning to send scanning results to:

- [Azure Event Grid custom topic](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-event-grid-for-malware-scanning): For near-real-time automatic response based on every scanning result.
- [Log Analytics workspace](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-logging-for-malware-scanning): For storing every scan result in a centralized log repository for compliance and audit.

[Learn more on how to set up a response for malware scanning results](defender-for-storage-configure-malware-scan).