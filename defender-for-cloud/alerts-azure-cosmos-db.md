---
layout: Conceptual
title: Alerts for Azure Cosmos DB - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-azure-cosmos-db
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
description: This article lists the security alerts for Azure Cosmos DB visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 71e91eb7-2b28-7d75-bba0-a68e90275dfa
document_version_independent_id: 66876144-8fee-426a-52a7-2b91d16467eb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-azure-cosmos-db.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-azure-cosmos-db
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-azure-cosmos-db.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd668c2f-f5b3-4573-8ad1-019570e3e2db
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cc82e69d-afbe-4554-9f4c-6705fc860c42
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 5499de86-6d3e-2ddd-9362-b94e855f8147
---

# Alerts for Azure Cosmos DB - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for Azure Cosmos DB from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Azure Cosmos DB alerts

[Further details and notes](concept-defender-for-cosmos)

### **Access from a Tor exit node**

(CosmosDB\_TorAnomaly)

**Description**: This Azure Cosmos DB account was successfully accessed from an IP address known to be an active exit node of Tor, an anonymizing proxy. Authenticated access from a Tor exit node is a likely indication that a threat actor is trying to hide their identity.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial Access

**Severity**: High/Medium

### **Access from a suspicious IP**

(CosmosDB\_SuspiciousIp)

**Description**: This Azure Cosmos DB account was successfully accessed from an IP address that was identified as a threat by Microsoft Threat Intelligence.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial Access

**Severity**: Medium

### **Access from an unusual location**

(CosmosDB\_GeoAnomaly)

**Description**: This Azure Cosmos DB account was accessed from a location considered unfamiliar, based on the usual access pattern.

Either a threat actor has gained access to the account, or a legitimate user has connected from a new or unusual geographic location

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial Access

**Severity**: Informational

### **Unusual volume of data extracted**

(CosmosDB\_DataExfiltrationAnomaly)

**Description**: An unusually large volume of data has been extracted from this Azure Cosmos DB account. This might indicate that a threat actor exfiltrated data.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Medium

### **Extraction of Azure Cosmos DB accounts keys via a potentially malicious script**

(CosmosDB\_SuspiciousListKeys.MaliciousScript)

**Description**: A PowerShell script was run in your subscription and performed a suspicious pattern of key-listing operations to get the keys of Azure Cosmos DB accounts in your subscription. Threat actors use automated scripts, like Microburst, to list keys and find Azure Cosmos DB accounts they can access.

This operation might indicate that an identity in your organization was breached, and that the threat actor is trying to compromise Azure Cosmos DB accounts in your environment for malicious intentions.

Alternatively, a malicious insider could be trying to access sensitive data and perform lateral movement.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Collection

**Severity**: Medium

### **Suspicious extraction of Azure Cosmos DB account keys**

(AzureCosmosDB\_SuspiciousListKeys.SuspiciousPrincipal)

**Description**: A suspicious source extracted Azure Cosmos DB account access keys from your subscription. If this source is not a legitimate source, this might be a high impact issue. The access key that was extracted provides full control over the associated databases and the data stored within. See the details of each specific alert to understand why the source was flagged as suspicious.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Informational

### **SQL injection: potential data exfiltration**

(CosmosDB\_SqlInjection.DataExfiltration)

**Description**: A suspicious SQL statement was used to query a container in this Azure Cosmos DB account.

The injected statement might have succeeded in exfiltrating data that the threat actor isn't authorized to access.

Due to the structure and capabilities of Azure Cosmos DB queries, many known SQL injection attacks on Azure Cosmos DB accounts can't work. However, the variation used in this attack might work and threat actors can exfiltrate data.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Medium

### **SQL injection: fuzzing attempt**

(CosmosDB\_SqlInjection.FailedFuzzingAttempt)

**Description**: A suspicious SQL statement was used to query a container in this Azure Cosmos DB account.

Like other well-known SQL injection attacks, this attack won't succeed in compromising the Azure Cosmos DB account.

Nevertheless, it's an indication that a threat actor is trying to attack the resources in this account, and your application might be compromised.

Some SQL injection attacks can succeed and be used to exfiltrate data. This means that if the attacker continues performing SQL injection attempts, they might be able to compromise your Azure Cosmos DB account and exfiltrate data.

You can prevent this threat by using parameterized queries.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-attack

**Severity**: Low

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.