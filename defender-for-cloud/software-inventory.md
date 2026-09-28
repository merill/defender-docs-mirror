---
layout: Conceptual
title: Review the Software Inventory in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/software-inventory
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
description: Software inventory in Microsoft Defender for Cloud shows software on your connected resources. Learn how to browse, query, and export it.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 01cc79a4-6e5a-5603-8236-d9d696b2d0a0
document_version_independent_id: 22080990-dc47-42ed-319b-9904b80cf37b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/software-inventory.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/software-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/software-inventory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: fdf74a60-8f62-db04-eb15-147b6ffefe13
---

# Review the Software Inventory in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

The Defender for Servers plan in Microsoft Defender for Cloud provides vulnerability scanning using Microsoft Defender Vulnerability Management. Microsoft Defender for Endpoint and Defender Vulnerability Management are integrated natively into Defender for Cloud.

The software inventory feature, provided by Defender Vulnerability Management, shows known software in your organization, with security information about discovered applications.

- Defender for Cloud shows the integrated software inventory on the **Inventory** page, summarizing software running on resources connected to Defender for Cloud.
- To query and retrieve inventory data at scale, use [Azure Resource Graph (ARG)](/en-us/azure/governance/resource-graph/index). For deep custom insights, use [Kusto Query Language (KQL)](/en-us/azure/data-explorer/kusto/query/).

This article explains how to review the software inventory. Before you begin, review the prerequisites to ensure the required Defender plans are enabled.

## Prerequisites

To see the software inventory, enable one of these paid plans.

- [Defender CSPM plan](concept-cloud-security-posture-management) with [agentless machine scanning](concept-agentless-data-collection) enabled.
- [Defender for Servers Plan 1 or Plan 2](defender-for-servers-introduction) with [Defender for Endpoint integration](integration-defender-for-endpoint) enabled, or Defender for Servers Plan 2 with agentless machine scanning enabled.

Note

If software that isn't supported appears in the inventory, only limited data is available.

## Browse the software inventory

1. In Defender for Cloud, select **Inventory**.
2. If you meet the prerequisites, the **Installed applications** filter shows you a list of software deployed in the environment.
3. In **Value**, filter for a specific app.

Resources connected to Defender for Cloud and running those apps are displayed. Blank options show machines where Defender for Servers or Defender for Endpoint isn't available.

## Query the software inventory

In addition to the predefined filters, you can explore the software inventory data from Azure Resource Graph Explorer.

1. Select **Azure Resource Graph Explorer**.

    ![Screenshot showing Azure Resource Graph Explorer opened in the Azure portal.](media/multi-factor-authentication-enforcement/opening-resource-graph-explorer.png)
2. Select the following subscription scope: **securityresources/softwareinventories**
3. Use one of the following query examples, customize one, or write your own.
4. Select **Run query**.

### Query examples

To generate a basic list of installed software:

```kusto
securityresources
| where type == "microsoft.security/softwareinventories"
| project id, Vendor=properties.vendor, Software=properties.softwareName, Version=properties.version
```

To filter by version numbers:

```kusto
securityresources
| where type == "microsoft.security/softwareinventories"
| project id, Vendor=properties.vendor, Software=properties.softwareName, Version=tostring(properties.version)
| where Software=="windows_server_2019" and parse_version(Version)<=parse_version("10.0.17763.1999")
```

To find machines with a combination of software products:

```kusto
securityresources
| where type == "microsoft.security/softwareinventories"
| extend vmId = properties.azureVmId
| where properties.softwareName == "apache_http_server" or properties.softwareName == "mysql"
| summarize count() by tostring(vmId)
| where count_ > 1
```

To combine a software product with another security recommendation:

(For example, machines that have MySQL installed and exposed management ports)

```kusto
securityresources
| where type == "microsoft.security/softwareinventories"
| extend vmId = tolower(properties.azureVmId)
| where properties.softwareName == "mysql"
| join (
    securityresources
| where type == "microsoft.security/assessments"
| where properties.displayName == "Management ports should be closed on your virtual machines" and properties.status.code == "Unhealthy"
| extend vmId = tolower(properties.resourceDetails.Id)
) on vmId
```

## Export the inventory

You can export filtered inventory data to a CSV file or save queries in Resource Graph Explorer for later use.

1. To save filtered inventory in CSV form, select **Download CSV report**.
2. To save a query in Resource Graph Explorer, select **Open a query**.
3. When you're ready to save a query, select **Save as**. In **Save query**, specify a query name and description, and choose whether the query is private or shared.