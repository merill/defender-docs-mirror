---
layout: Conceptual
title: Azure Monitor Agent (AMA) in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/auto-deploy-azure-monitoring-agent
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
description: Learn how Microsoft Defender for Cloud uses the Azure Monitor Agent (AMA) for Defender for SQL Servers on Machines and the free data ingestion benefit in Defender for Servers Plan 2.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: template-how-to, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: bb7752d3-bb10-69e8-7595-4e018c9c6783
document_version_independent_id: daf31d82-7978-b665-9d08-4d05595ed0a2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/auto-deploy-azure-monitoring-agent.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/auto-deploy-azure-monitoring-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/auto-deploy-azure-monitoring-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: 2a000314-5b0f-1b74-7482-335656ac6e8c
---

# Azure Monitor Agent (AMA) in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud uses the Azure Monitor Agent (AMA) to:

- Protect databases in the Defender for SQL Servers on Machines plan.
- Take advantage of the [free data ingestion](data-ingestion-benefit) benefit provided in Defender for Servers Plan 2.

## AMA in Defender for SQL Servers on Machines

Defender for SQL Servers on Machines uses the AMA to collect machine information for posture assessment. This data helps detect misconfigurations and prevent attacks.

- The AMA replaces the Log Analytics agent (also known as the Microsoft Monitoring Agent (MMA)) that the plan previously used.
- The MMA is deprecated. If you're using MMA, migrate to AMA by using the [auto-provisioning instructions for Defender for SQL Servers on Machines](defender-for-sql-autoprovisioning).

Important

The AMA configuration for SQL Servers on Machines applies only to government clouds.

Autoprovisioning for the AMA is turned on by default when you enable the database plan. You can turn automatic provisioning off and on as needed.

The AMA is implemented as a virtual machine extension, but you can deploy it in other ways. For deployment options, see [Monitor virtual machines with Azure Monitor agent](/en-us/azure/azure-monitor/vm/monitor-virtual-machine-agent).