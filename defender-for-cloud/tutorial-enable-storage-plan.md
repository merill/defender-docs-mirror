---
layout: Conceptual
title: Deploy Microsoft Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/tutorial-enable-storage-plan
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
description: Learn how to enable Microsoft Defender for Storage on your Azure subscription for Microsoft Defender for Cloud.
ms.topic: install-set-up-deploy
ms.date: 2025-05-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 04e30b72-8912-e63e-2c86-33ec209f2eac
document_version_independent_id: 6c904b0a-1653-d769-7c4f-67ac7ce27965
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/tutorial-enable-storage-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/tutorial-enable-storage-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/tutorial-enable-storage-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: f0e35c1b-13c3-5039-08c2-ba3659744335
---

# Deploy Microsoft Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Storage is an Azure-native solution. It offers an advanced layer of intelligence for detecting and mitigating threats in storage accounts. It uses [Microsoft Defender Threat Intelligence](https://www.microsoft.com/security/business/siem-and-xdr/microsoft-defender-threat-intelligence/), Microsoft Defender Antivirus technologies, and sensitive data discovery. It helps protect the Azure Blob Storage, Azure Files, and Azure Data Lake Storage services.

Defender for Storage provides a comprehensive alert suite, near-real-time malware scanning (as an add-on), and sensitive-data threat detection at no extra cost. You can use these features to quickly detect, assess, and respond to potential security threats with detailed information. This ability helps prevent major impacts on your data and workload, including malicious file uploads, sensitive data exfiltration, and data corruption.

Organizations can customize their protection and enforce consistent security policies by enabling Defender for Storage on subscriptions and storage accounts with granular control and flexibility.

Tip

If you're currently using the classic Defender for Storage plan, consider [migrating to the new plan](defender-for-storage-classic-migrate). The new plan offers several benefits over the classic plan.

To learn about pricing and regional availability, check out the [Microsoft Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also estimate costs by using the [Defender for Cloud cost calculator](cost-calculator).

## Prerequisites

Before you enable Defender for Storage, ensure that you have the necessary permissions and other prerequisites in place. For more information, see [Prerequisites for Microsoft Defender for Storage](support-matrix-defender-for-storage).

## Setup and configuration options

To enable and configure Defender for Storage and to ensure maximum protection and cost optimization, you can use these available options:

- Enable or disable Defender for Storage at the subscription level or the storage account level.
- Enable or disable the configurable features for malware scanning and sensitive-data threat detection.
- Set a monthly cap on the malware scanning per storage account per month for controlling costs. (The default value is 10,000 GB.)
- Configure methods to set up a response to malware scanning results.
- Configure methods for logging malware scanning results. The malware scanning feature has advanced configurations to help security teams support various workflows and requirements.
- [Override subscription-level settings to configure specific storage accounts](advanced-configurations-for-malware-scanning#override-defender-for-storage-subscription-level-settings). You can use custom configurations that differ from the settings configured at the subscription level.

## Deployment methods

There are several ways to enable and configure Defender for Storage. The following links provide direct access to enablement pages for each supported deployment method:

- [Azure built-in policy](defender-for-storage-policy-enablement) (recommended)
- Infrastructure as code (IaC) templates, including:
    - [Terraform](defender-for-storage-infrastructure-as-code-enablement?tabs=enable-subscription#terraform-template)
    - [Bicep](defender-for-storage-infrastructure-as-code-enablement?tabs=enable-subscription#bicep-template)
    - [Azure Resource Manager](defender-for-storage-infrastructure-as-code-enablement?tabs=enable-subscription#azure-resource-manager-template)
- [Azure portal](defender-for-storage-azure-portal-enablement?tabs=enable-subscription)
- [Azure PowerShell](defender-for-storage-powershell-enablement??tabs=enable-subscription)
- [REST API](defender-for-storage-rest-api-enablement?tabs=enable-subscription)

We recommend that you enable Defender for Storage via a policy. This method facilitates enablement at scale. It also ensures that a consistent security policy is applied across all existing and future storage accounts within the defined scope, such as entire management groups. This approach keeps the storage accounts protected with Defender for Storage according to your organization's defined configuration.

## View your current coverage

Defender for Cloud provides access to [workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that provide insights into your security posture. The [coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) helps you understand your current coverage by showing which plans are enabled on your subscriptions and resources.

In addition, you can view Defender for Storage threat protection and posture coverage directly in Storage Center, alongside your storage resources.

Storage Center gives you a centralized, storage-native view of Defender for Storage protection status. This view helps you quickly understand:

- Which storage accounts are protected, partially protected, or not protected
- Where malware scanning, activity monitoring, and sensitive data discovery are enabled
- Where security gaps exist across Azure Blob Storage and Azure Files storage

You can drill down from high-level insights to service-level and resource-level views, and seamlessly deep‑link into Defender for Cloud to take action and remediate gaps.

Learn more about [Azure storage](/en-us/azure/storage/blobs/storage-blobs-overview).