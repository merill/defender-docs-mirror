---
layout: Conceptual
title: Modify Defender for Servers plan settings in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/configure-servers-coverage
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
description: Learn how to configure settings in the Defender for Servers plan in Microsoft Defender for Cloud.
ms.topic: install-set-up-deploy
ms.date: 2025-02-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: fc264d3c-93a0-957a-38ea-d3e95f26af98
document_version_independent_id: d6bdf8e4-241f-87e0-2029-230bb92a4fe7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/configure-servers-coverage.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/configure-servers-coverage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/configure-servers-coverage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: ffc7740c-4515-c003-7bd3-ff9919d1061f
---

# Modify Defender for Servers plan settings in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

After [deploying the Defender for Servers plan](tutorial-enable-servers-plan) in Microsoft Defender for Cloud, you can check which machines are protected by the plan, and configure plan settings as needed.

## Check machine protection

Find machines protected by the plan.

1. In Defender for Cloud, select **Inventory**.
2. In the **Resource Type** query, you can filter the inventory to narrow down results to resources supported by Defender for Servers. For example:

    - Use the **Resource type** query to find virtual machines, AWS EC2 instances, and GCP Compute instances.
    - Use the **Environment** query to narrow down to Azure, AWS, or GCP resources.
3. In the virtual machine list, review the **Defender for Cloud** column:

    [![Screenshot that shows you where to select Inventory from the main menu.](media/configure-servers-coverage/select-inventory.png)](media/configure-servers-coverage/select-inventory.png#lightbox)
4. If the column setting is **On**, then Defender for Cloud is enabled, along with any plans switched on in Defender for Cloud, including Defender for Servers.

You can also check protection coverage for all subscriptions and resources using the [Coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook).

## Modify plan settings

Some features are turned on by default when you enable Defender for Servers. You can modify plan features manually as follows:

1. In subscription enabled for Defender for Cloud, select **Environment settings**.
2. Locate Defender for Servers and select **Settings**.
3. In **Settings and monitoring**, select the setting you want to modify.

    | **Feature** | **Details** | **Modify plan** |
    | --- | --- | --- |
    | **Vulnerability assessment** | When you enable Defender for Servers Plan 1 (P1) or Plan 2 (P2), [vulnerability scanning](auto-deploy-vulnerability-assessment) is enabled by default. | [Manually configure](deploy-vulnerability-assessment-defender-vulnerability-management) vulnerability scanning settings. |
    | **Endpoint protection**. | When you enable Defender for Servers Plan 1 (P1) or 2 (P2), Defender for Endpoint is integrated by default. Protection features from Defender for Endpoint are available. Automatic provisioning of the Defender for Endpoint agent on connected machines is enabled. | [Turn endpoint protection on and off](enable-defender-for-endpoint) in a plan. |
    | **Agentless scanning** | [Agentless scanning](concept-agentless-data-collection) provides a number of scanning capabilities. It's enabled by default when Defender for Servers Plan 2 (or the Defender Cloud Security Posture Management (CSPM) plan) is turned on. | [Turn agentless scanning on and off](enable-agentless-scanning-vms), and [exclude machines from agentless scanning](exclude-machines-agentless-scanning). |
    | **File integrity monitoring** | When you enable Defender for Servers Plan 2, you can turn on file integrity monitoring. It's not turned on by default | [Learn about](file-integrity-monitoring-compare-baselines) and [enable](file-integrity-monitoring-enable-defender-endpoint) file integrity monitoring |