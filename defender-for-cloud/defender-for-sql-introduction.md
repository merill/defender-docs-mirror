---
layout: Conceptual
title: Benefits and Features of Defender for Azure SQL Databases - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-introduction
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
description: Learn how Microsoft Defender for Azure SQL Databases helps you discover, track, and mitigate vulnerabilities, and alerts you to potential threats.
ms.date: 2025-05-13T00:00:00.0000000Z
ms.topic: overview
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: 1d386127-b5e2-34cf-112f-638299ac088a
document_version_independent_id: acc7d46e-058f-ebb3-f36e-2d7413257362
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-sql-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-sql-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-sql-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab7faaf-d791-4a26-96a2-3b11738538e7
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/302e28b0-1f09-4811-9a9b-2a72e0770581
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: e5c45b61-f5f7-957a-8d64-ffd252e21bad
---

# Benefits and Features of Defender for Azure SQL Databases - Microsoft Defender for Cloud | Microsoft Learn

In Microsoft Defender for Cloud, the *Defender for Azure SQL Databases* plan within Defender for Databases helps you discover and mitigate potential [database vulnerabilities](sql-azure-vulnerability-assessment-overview). It alerts you to anomalous activities that might indicate a threat to your databases.

When you enable Defender for Azure SQL Databases, all supported resources within the subscription are protected. Future resources that you create on the same subscription will also be protected. For information about billing, see the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

Defender for Azure SQL Databases helps protect read/write replicas of:

- Azure SQL [single databases](/en-us/azure/azure-sql/database/single-database-overview) and [elastic pools](/en-us/azure/azure-sql/database/elastic-pool-overview).
- [Azure SQL managed instances](/en-us/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview).
- [Azure Synapse Analytics (formerly Azure SQL Data Warehouse) dedicated SQL pools](/en-us/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is).

Defender for Azure SQL Databases helps protect the following SQL Server products:

- SQL Server version 2012, 2014, 2016, 2017, 2019, and 2022
- [SQL Server on Azure Virtual Machines](/en-us/azure/azure-sql/virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview)
- [SQL Server enabled by Azure Arc](/en-us/sql/sql-server/azure-arc/overview)

## Benefits

### Vulnerability assessment

Defender for Azure SQL Databases discovers, tracks, and helps you fix potential database vulnerabilities. These vulnerability assessment scans provide an overview of your SQL machines' security state and details of any security findings, including anomalous activities that could indicate threats to your databases. [Learn more about the vulnerability assessment](sql-azure-vulnerability-assessment-overview).

### Threat protection

Defender for Azure SQL Databases uses [Advanced Threat Protection](/en-us/azure/azure-sql/database/threat-detection-overview) to continuously monitor your SQL servers for threats like:

- **Potential SQL injection attacks**: For example, vulnerabilities detected when applications generate a faulty SQL statement in the database.
- **Anomalous database access and query patterns**: For example, an abnormally high number of failed sign-in attempts with different credentials (a brute force attack).
- **Suspicious database activity**: For example, a legitimate user accessing a SQL server from a breached computer that communicated with a crypto-mining command and control (C&C) server.

Defender for Azure SQL Databases provides action-oriented security alerts in Defender for Databases. These alerts include details of the suspicious activity, guidance on how to mitigate the threats, and options for continuing your investigations by using Microsoft Sentinel. [Learn more about the security alerts for SQL servers](alerts-sql-database-and-azure-synapse-analytics).