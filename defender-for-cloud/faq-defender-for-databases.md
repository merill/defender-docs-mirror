---
layout: FAQ
title: Common Questions - Defender for Databases - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-defender-for-databases
summary: >
  <p>Get answers to common questions about Microsoft Defender for Databases.</p>
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
description: Get answers to frequently asked questions about Microsoft Defender for Databases.
ms.topic: faq
ms.date: 2025-05-18T00:00:00.0000000Z
locale: en-us
document_id: 44b778d4-d34f-01bd-d6ca-993c70a5e976
document_version_independent_id: a3009f44-5891-64cf-4ad3-1a72d74e8c76
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-defender-for-databases.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-defender-for-databases
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-defender-for-databases.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b61581fb-2513-b33f-7b7f-cdd9c47c636c
---

# Common Questions - Defender for Databases - Microsoft Defender for Cloud | Microsoft Learn

Get answers to common questions about Microsoft Defender for Databases.

## Is there a performance effect from deploying Microsoft Defender for SQL Servers on Machines?

Microsoft Defender for SQL Servers on Machines focuses on security, but it has a split architecture to balance data uploading and speed with performance:

- Some of our detectors, including an [Extended Events trace](/en-us/azure/azure-sql/database/xevent-db-diff-from-svr) named `SQLAdvancedThreatProtectionTraffic`, run on the machine for real-time speed advantages.
- Other detectors run in the cloud to spare the machine from heavy computational loads.

Lab tests of our solution showed CPU usage averaging 3% for peak slices, compared against benchmark loads. An analysis of our current user data shows a negligible effect on CPU and memory usage.

Performance always varies between environments, machines, and loads. These statements serve as a general guideline, not a guarantee for any individual deployment.

## What happens to the old scan results and baselines after I switch to express configuration?

Old results and baseline settings remain available on your storage account, but they won't be updated or used by the system. You don't need to maintain these files for SQL vulnerability assessment to work after you switch to express configuration, but you can keep your old baseline definitions for future reference.

When express configuration is enabled, you don't have direct access to the result and baseline data because it's stored on internal Microsoft storage.

## Why is my Azure SQL server marked as unhealthy for "SQL servers should have vulnerability assessment configured," even though I set it up properly by using classic configuration?

The policy behind this recommendation checks for the existence of subassessments for the server. With classic configuration, system databases are scanned only if at least one user database exists. A server without any user databases doesn't have scans or reported scan results, which causes the policy to remain unhealthy.

Switching to express configuration mitigates the issue by enabling scheduled and manual scans for system databases.

## Can I set up recurring scans with express configuration?

Express configuration automatically sets up recurring scans for all databases under your server. This behavior is the default, and it isn't configurable at the server or database level.

## Is there a way with express configuration to get the weekly email report that's provided in classic configuration?

You can use workflow automation and Logic Apps email scheduling, by following the Microsoft Defender for Cloud processes:

- Time-based triggers
- Scan-based triggers
- Support for disabled rules

## Why can't I set database policies anymore?

The SQL vulnerability assessment reports all vulnerabilities and misconfigurations in your environment, so including all databases is helpful. Defender for SQL Servers on Machines is billed per server, not per database.

## Can I revert to classic configuration?

Yes. You can revert to classic configuration by using the existing REST APIs and PowerShell cmdlets. When you revert to classic configuration, a notification appears in the Azure portal for changing to express configuration.

## Will express configuration become available for other types of SQL?

Stay tuned for updates!

## Can I choose which experience is the default?

No. Express configuration is the default for every new, supported Azure SQL database.

## Does express configuration change scanning behavior?

No, express configuration provides the same scanning behavior and performance.

## Does express configuration have any effect on pricing?

Express configuration doesn't require a storage account, so you don't need to pay extra storage fees unless you choose to keep old scan and baseline data.

## What does the 1-MB cap per rule mean?

Any individual rule can't produce results that are more than 1 MB. When results for the rule reach that limit, they stop. You can't set a baseline for the rule, the rule isn't included in the overall recommendation health, and the results appear as **Not applicable**.

## After I enable Microsoft Defender for SQL Servers on Machines, how long do I need to wait to see a successful deployment?

It takes approximately 30 minutes to update the protection status via the SQL IaaS Agent Extension, assuming that all the prerequisites are fulfilled.

## How does Defender for SQL Servers on Machines collect logs from the SQL server?

Defender for SQL Servers on Machines uses Extended Events, beginning with SQL Server 2017. On previous versions of SQL Server, Defender for SQL Servers on Machines collects the logs by using the SQL Server audit logs.