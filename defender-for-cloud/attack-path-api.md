---
layout: Conceptual
title: Retrieve attack path data with the Azure Resource Graph API - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/attack-path-api
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
description: Query attack path data programmatically in Microsoft Defender for Cloud by using the Azure Resource Graph API.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 15c31042-46ba-8e63-2344-81fa306af0df
document_version_independent_id: ea6bae85-5b2d-96c0-c0ab-54f108cf2c70
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/attack-path-api.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/attack-path-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/attack-path-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3928677-9b71-43a6-875f-004dc4f98b65
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/6bbc70ca-58b2-4c69-8249-28ec92c08029
platformId: e7eeb3e9-8354-71b9-a37f-02a7f8fceabb
---

# Retrieve attack path data with the Azure Resource Graph API - Microsoft Defender for Cloud | Microsoft Learn

You can consume attack path data programmatically by querying the Azure Resource Graph (ARG) application programming interface (API). The API returns externally driven, exploitable attack paths that focus on real threats.

To query the ARG API, see [Azure Resource Graph API query documentation](/en-us/rest/api/azureresourcegraph/resourcegraph%282020-04-01-preview%29/resources/resources?source=recommendations&amp;tabs=HTTP).

## Consume attack path data programmatically using API

The following examples show sample ARG queries that you can run:

**Get all attack paths in subscription ‘X’**:

```kusto
securityresources
| where type == "microsoft.security/attackpaths"
| where subscriptionId == <SUBSCRIPTION_ID>
```

**Get all instances for a specific attack path**: The following query filters attack path resources within a specific subscription and matches them by display name. Replace `<DISPLAY_NAME>` with the name of the attack path, for example, `Internet exposed VM with high severity vulnerabilities and read permission to a Key Vault`.

```kusto
securityresources
| where type == "microsoft.security/attackpaths"
| where subscriptionId == "<Subscription ID>"
| extend AttackPathDisplayName = tostring(properties["displayName"])
| where AttackPathDisplayName == "<DISPLAY_NAME>"
```

### API response schema

The following table lists the data fields returned from the API response:

| Field | Description |
| --- | --- |
| ID | The Azure resource ID of the attack path instance |
| Name | The Unique identifier of the attack path instance |
| Type | The Azure resource type, always equals `microsoft.security/attackpaths` |
| Tenant ID | The tenant ID of the attack path instance |
| Location | The location of the attack path |
| Subscription ID | The subscription of the attack path |
| Properties.description | The description of the attack path |
| Properties.displayName | The display name of the attack path |
| Properties.attackPathType | The type of the attack path |
| Properties.manualRemediationSteps | Manual remediation steps of the attack path |
| Properties.refreshInterval | The refresh interval of the attack path |
| Properties.potentialImpact | The potential impact of the attack path being breached |
| Properties.riskCategories | The categories of risk of the attack path |
| Properties.entryPointEntityInternalID | The internal ID of the entry point entity of the attack path |
| Properties.targetEntityInternalID | The internal ID of the target entity of the attack path |
| Properties.assessments | Mapping of entity internal ID to the security assessments on that entity |
| Properties.graphComponent | List of graph components representing the attack path |
| Properties.graphComponent.insights | List of insights graph components related to the attack path |
| Properties.graphComponent.entities | List of entities graph components related to the attack path |
| Properties.graphComponent.connections | List of connections graph components related to the attack path |
| Properties.AttackPathID | The unique identifier of the attack path instance |