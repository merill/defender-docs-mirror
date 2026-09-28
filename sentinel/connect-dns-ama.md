---
layout: Conceptual
title: Stream and filter Windows DNS logs with the AMA connector | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-dns-ama
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Ingest and filter data from your Windows DNS server logs with this data connector. Query this data to protect your DNS servers from threats and attacks.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: dd21c249-af36-dd0e-cd7b-506e786cc729
document_version_independent_id: 7824fb56-06b9-b7de-e2f2-0fd2cc06a36b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-dns-ama.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-dns-ama
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-dns-ama.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 41ea313d-98de-5904-dce1-81e0bac395cc
---

# Stream and filter Windows DNS logs with the AMA connector | Microsoft Learn

This article describes how to use the Azure Monitor Agent (AMA) connector to stream and filter events from your Windows Domain Name System (DNS) server logs. You can then deeply analyze your data to protect your DNS servers from threats and attacks. The AMA and its DNS extension are installed on your Windows Server to upload data from your DNS analytical logs to your Microsoft Sentinel workspace.

DNS is a widely used protocol, which maps between host names and computer readable IP addresses. Because DNS wasn’t designed with security in mind, the service is highly targeted by malicious activity, making its logging an essential part of security monitoring. Some well-known threats that target DNS servers include DDoS attacks targeting DNS servers, DNS DDoS Amplification, DNS hijacking, and more.

While some mechanisms were introduced to improve the overall security of the DNS protocol, DNS servers are still a highly targeted service. Organizations can monitor DNS logs to better understand network activity, and to identify suspicious behavior or attacks targeting resources within the network. The **Windows DNS Events via AMA** connector provides visibility into DNS network activity and suspicious behavior. For example, use the connector to identify clients that try to resolve malicious domain names, view and monitor request loads on DNS servers, or view dynamic DNS registration failures.

Note

The Windows DNS Events via AMA connector only supports analytical log events.

## Prerequisites

Before you begin, verify that you have:

- A Log Analytics workspace enabled for Microsoft Sentinel.
- The **Windows DNS Events via AMA** data connector installed as part of the **Windows Server DNS** solution from content hub.
- Windows server 2016 and later supported, or Windows Server 2012 R2 with the auditing hotfix.
- DNS server role installed with **DNS-Server** analytical event logs enabled. DNS analytical event logs aren't enabled by default. For more information, see [Enable analytical event logging](/en-us/windows-server/networking/dns/dns-logging-and-diagnostics#enable-analytical-event-logging).

To collect events from any system that isn't an Azure virtual machine, ensure that [Azure Arc](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage) is installed. Install and enable Azure Arc before you enable the Azure Monitor Agent-based connector. The Azure Arc installation requirement applies to:

- Windows servers installed on physical machines
- Windows servers installed on on-premises virtual machines
- Windows servers installed on virtual machines in non-Azure clouds

## Configure the Windows DNS over AMA connector via the portal

Use the portal setup option to configure the connector using a single Data Collection Rule (DCR) per workspace. Afterwards, use advanced filters to filter out specific events or information, uploading only the valuable data you want to monitor, reducing costs and bandwidth usage.

If you need to create multiple DCRs, configure the connector via API instead. Using the API to create multiple DCRs will still show only one DCR in the portal.

**To configure the connector**:

1. In Microsoft Sentinel, open the **Data connectors** page, and locate the **Windows DNS Events via AMA** connector.
2. Towards the bottom of the side pane, select **Open connector page**.
3. In the **Configuration** area, select **Create data collection rule**. You can create a single DCR per workspace.

    The DCR name, subscription, and resource group are automatically set based on the workspace name, the current subscription, and the resource group the connector was selected from. For example:

    ![Screenshot of creating a new D C R for the Windows D N S over A M A connector.](media/connect-dns-ama/windows-dns-ama-connector-create-dcr.png)
4. Select the **Resources** tab &gt; **Add Resource(s)**.
5. Select the VMs on which you want to install the connector to collect logs. For example:

    ![Screenshot of selecting resources for the Windows D N S over A M A connector.](media/connect-dns-ama/windows-dns-ama-connector-select-resource.png)
6. Review your changes and select **Save** &gt; **Apply**.

## Configure the Windows DNS over AMA connector via API

Use the API setup option to configure the connector using multiple [DCRs](/en-us/rest/api/monitor/data-collection-rules) per workspace. If you'd prefer to use a single DCR, configure the connector via the portal instead.

Using the API to create multiple DCRs still shows only one DCR in the portal.

Use the following example as a template to create or update a DCR:

### Request URL and header

```http
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/dataCollectionRules/{dataCollectionRuleName}?api-version={latest-supported-version}
```

For the latest supported API version, see [Data Collection Rules - REST API (Azure Monitor)](/en-us/rest/api/monitor/data-collection-rules).

![Screenshot of the API version's appearance in the DCR documentation.](media/connect-dns-ama/windows-dns-ama-connector-dcr-api-version.png)

### Request body

Use the following sample request body when creating the DCR. This payload defines the DCR properties, including the location, platform kind, data sources, event filters, and the Log Analytics workspace destination:

```json
{
    "location": "eastus2",
    "kind" : "Windows",
    "properties": {
        "dataSources": {
            "windowsEventLogs": [],
            "extensions": [
                {
                    "streams": [
                        "Microsoft-ASimDnsActivityLogs"
                    ],
                    "extensionName": "MicrosoftDnsAgent",
                    "extensionSettings": {
                        "Filters": [
                            {
                                "FilterName": "SampleFilter",
                                "Rules": [
                                    {
                                        "Field": "EventOriginalType",
                                        "FieldValues": [
                                            "260"
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    "name": "SampleDns"
                }
            ]
        },
        "destinations": {
            "logAnalytics": [
                {
                    "name" : "WorkspaceDestination",
                    "workspaceId" : "{WorkspaceGuid}",
                    "workspaceResourceId" : "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.OperationalInsights/workspaces/{sentinelWorkspaceName}"
                }
            ]
        },
        "dataFlows": [
            {
                "streams": [
                    "Microsoft-ASimDnsActivityLogs"
                ],
                "destinations": [
                    "WorkspaceDestination"
                ]
            }
        ],
    },
    "tags" : {}
}
```

## Use advanced filters in your DCRs

DNS server event logs can contain a huge number of events. We recommend using advanced filtering to filter out unneeded events before the data is uploaded, saving valuable triage time and costs. The filters remove the unneeded data from the stream of events uploaded to your workspace, and are based on a combination of multiple fields.

For more information, see [Available fields for filtering](dns-ama-fields#available-fields-for-filtering).

### Create advanced filters via the portal

Use the following procedure to create filters via the portal. For more information about creating filters with the API, see Advanced filtering examples.

**To create filters via the portal**:

1. On the connector page, in the **Configuration** area, select **Add data collection filters**.
2. Enter a name for the filter and select the filter type, which is a parameter that reduces the number of collected events. Parameters are normalized according to the DNS normalized schema. For more information, see [Available fields for filtering](dns-ama-fields#available-fields-for-filtering).

    ![Screenshot of creating a filter for the Windows D N S over A M A connector.](media/connect-dns-ama/windows-dns-ama-connector-create-filter.png)
3. Select the values for which you want to filter the field from among the values listed in the drop-down.

    ![Screenshot of adding fields to a filter for the Windows D N S over A M A connector.](media/connect-dns-ama/windows-dns-ama-connector-filter-fields.png)
4. To add complex filters, select **Add exclude field to filter** and add the relevant field.

    - Use comma-separated lists to define multiple values for each field.
    - To create compound filters, use different fields with an AND relation.
    - To combine different filters, use an OR relation between them.

    Filters also support wildcards as follows:

    - Add a dot after each asterisk (`*.`).
    - Don't use spaces between the list of domains.
    - Wildcards apply to the domain's subdomains only, including `www.domain.com`, regardless of the protocol. For example, if you use `*.domain.com`in an advanced filter:
        - The filter applies to `www.domain.com` and `subdomain.domain.com`, regardless of whether the protocol is HTTPS, FTP, and so on.
        - The filter doesn't apply to `domain.com`. To apply a filter to `domain.com`, specify the domain directly, without using a wildcard.
5. To add more new filters, select **Add new exclude filter**.
6. When you're finished adding filters, select **Add**.
7. Back on the main connector page, select **Apply changes** to save and deploy the filters to your connectors. To edit or delete existing filters or fields, select the edit or delete icons in the table under the **Configuration** area.
8. To add fields or filters after your initial deployment, select **Add data collection filters** again.

### Advanced filtering examples

Use the following examples to create commonly used advanced filters, via the portal or API.

#### Don't collect specific event IDs

This filter instructs the connector not to collect EventID 256 or EventID 257 or EventID 260 with IPv6 addresses.

**Using the Microsoft Sentinel portal**:

1. Create a filter with the **EventOriginalType** field, using the **Equals** operator, with the values **256**, **257**, and **260**.

    ![Screenshot of filtering out event IDs for the Windows D N S over A M A connector.](media/connect-dns-ama/windows-dns-ama-connector-eventid-filter.png)
2. Create a filter with the **EventOriginalType** field defined above, and using the **And** operator, also including the **DnsQueryTypeName** field set to **AAAA**.

    ![Screenshot of filtering out event IDs and IPv6 addresses for the Windows D N S over A M A connector.](media/connect-dns-ama/windows-dns-ama-connector-eventid-dnsquery-filter.png)

**Using the API**:

The following JSON shows the equivalent filter definitions for the API. The first filter excludes events with EventID 256, 257, or 260 that have an AAAA (IPv6) query type, and the second filter excludes EventID 230 with specific error result details.

```json
"Filters": [
    {
        "FilterName": "SampleFilter",
        "Rules": [
            {
                "Field": "EventOriginalType",
                "FieldValues": [
                    "256", "257", "260"                                                                              
                ]
            },
            {
                "Field": "DnsQueryTypeName",
                "FieldValues": [
                    "AAAA"                                        
                ]
            }
        ]
    },
    {
        "FilterName": "EventResultDetails",
        "Rules": [
            {
                "Field": "EventOriginalType",
                "FieldValues": [
                    "230"                                        
                ]
            },
            {
                "Field": "EventResultDetails",
                "FieldValues": [
                    "BADKEY","NOTZONE"                                        
                ]
            }
        ]
    }
]
```

#### Don't collect events with specific domains

This filter instructs the connector not to collect events from any subdomains of microsoft.com, google.com, amazon.com, or events from facebook.com or center.local.

**Using the Microsoft Sentinel portal**:

Set the **DnsQuery** field using the **Equals** operator, with the list *\*.microsoft.com,\*.google.com,facebook.com,\*.amazon.com,center.local*.

Review these considerations for wildcard filtering in DNS AMA domain filters.

![Screenshot of filtering out domains for the Windows D N S over A M A connector.](media/connect-dns-ama/windows-dns-ama-connector-domain-filter.png)

To define different values in a single field, use the **OR** operator.

**Using the API**:

The following JSON shows the equivalent domain exclusion filter for the DCR API payload, excluding DNS query events that match specific domains and their subdomains. Review these considerations for wildcard filtering in DNS AMA domain filters.

```json
"Filters": [ 
    { 
        "FilterName": "SampleFilter", 
        "Rules": [ 
            { 
                "Field": "DnsQuery", 
                "FieldValues": [ 
                    "*.microsoft.com", "*.google.com", "facebook.com", "*.amazon.com","center.local"                                                                               
                ]
            }
        ]
    }
]
```

## Normalization using ASIM

This connector is fully normalized using [Advanced Security Information Model (ASIM) parsers](normalization). The connector streams events originated from the Windows DNS analytical logs into the normalized table named `ASimDnsActivityLogs`. This table acts as a translator, using one unified language, shared across all DNS connectors to come.

For a source-agnostic parser that unifies all DNS data and ensures that your analysis runs across all configured sources, use the [ASIM DNS unifying parser](normalization-schema-dns#out-of-the-box-parsers)`_Im_Dns`.

The ASIM unifying parser complements the native `ASimDnsActivityLogs` table. While the native table is ASIM compliant, the parser is needed to add capabilities, such as aliases, available only at query time, and to combine `ASimDnsActivityLogs` with other DNS data sources.

The [ASIM DNS schema](normalization-schema-dns) represents the DNS protocol activity, as logged in the Windows DNS server in the analytical logs. The schema is governed by official parameter lists and RFCs that define fields and values.

See the [list of Windows DNS server fields](dns-ama-fields#asim-normalized-dns-schema) translated into the normalized field names.