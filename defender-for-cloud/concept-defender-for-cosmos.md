---
layout: Conceptual
title: Overview of Defender for Azure Cosmos DB - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-defender-for-cosmos
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
description: Learn about the benefits, features, and security capabilities of Microsoft Defender for Azure Cosmos DB to help protect your databases.
ms.topic: concept-article
ms.date: 2024-12-24T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f615901b-e65f-1675-7083-99f2fe83f7c0
document_version_independent_id: 2351a42e-4873-5358-24d8-f2f8eeaed0e1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-defender-for-cosmos.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-defender-for-cosmos
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-defender-for-cosmos.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd668c2f-f5b3-4573-8ad1-019570e3e2db
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cc82e69d-afbe-4554-9f4c-6705fc860c42
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: a953f531-30f4-01d6-ce84-ed6fc76ae44c
---

# Overview of Defender for Azure Cosmos DB - Microsoft Defender for Cloud | Microsoft Learn

In Microsoft Defender for Cloud, the *Defender for Azure Cosmos DB* plan within Defender for Databases detects potential SQL injections, known bad actors, and suspicious access patterns based on [Microsoft Defender Threat Intelligence](https://www.microsoft.com/security/business/siem-and-xdr/microsoft-defender-threat-intelligence/). It also identifies potential exploitation of your database through compromised identities or malicious insiders.

Defender for Azure Cosmos DB continually analyzes the personal data stream from the Azure Cosmos DB service. When it detects potentially malicious activities, it generates security alerts in Defender for Cloud. These alerts provide details of the suspicious activity, along with relevant investigation steps, remediation actions, and security recommendations to prevent future attacks.

You can [enable Microsoft Defender for Azure Cosmos DB](quickstart-enable-database-protections) for all your databases (recommended), or you can enable it at either the subscription level or the resource level. Importantly, Defender for Azure Cosmos DB doesn't access the Azure Cosmos DB account data and doesn't affect the service's performance.

For billing information about Defender for Azure Cosmos DB, see the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

The following table lists supported and unsupported Azure Cosmos DB APIs in Defender for Azure Cosmos DB:

| Supported | Not supported |
| --- | --- |
| Azure Cosmos DB for NoSQL | Azure Cosmos DB for Apache Cassandra  Azure Cosmos DB for MongoDB  Azure Cosmos DB for Table  Azure Cosmos DB for Apache Gremlin |

For cloud availability, see [Defender for Cloud support matrices for Azure commercial/other clouds](support-matrix-defender-for-cloud).

## Benefits

Defender for Azure Cosmos DB uses advanced threat detection capabilities and Microsoft Threat Intelligence data. It continuously monitors your Azure Cosmos DB accounts for threats like SQL injection, compromised identities, and data exfiltration.

Defender for Cloud provides action-oriented security alerts with details of the suspicious activity and guidance on how to mitigate threats. Use this information to quickly remediate security issues and improve the security of your Azure Cosmos DB accounts.

You can export alerts to Microsoft Sentinel, to any partner security information and event management (SIEM) solution, or to any external tool. To learn how to stream alerts, see [Stream alerts to monitoring solutions](export-to-siem).

## Alert types

Activities that trigger security alerts enriched with threat intelligence include:

- **Potential SQL injection attacks**: Due to the structure and capabilities of Azure Cosmos DB queries, many known SQL injection attacks don't work in Azure Cosmos DB. However, some variations of SQL injections could succeed and might result in exfiltrating data from your Azure Cosmos DB accounts. Defender for Azure Cosmos DB detects both successful and failed attempts, and it helps you harden your environment to prevent these threats.
- **Anomalous database access patterns**: An example is access from an onion router (Tor) exit node, known suspicious IP addresses, unusual applications, and unexpected locations.
- **Suspicious database activity**: An example is suspicious key-listing patterns that resemble known malicious lateral movement techniques and data extraction patterns.

Tip

For a comprehensive list of all Defender for Azure Cosmos DB alerts, see [Alerts for Azure Cosmos DB](alerts-azure-cosmos-db). This information is useful for workload owners who want to know what threats can be detected. It can also help security operations center (SOC) teams gain familiarity with detections before investigating them. [Learn more about how to manage and respond to security alerts in Microsoft Defender for Cloud](manage-respond-alerts).