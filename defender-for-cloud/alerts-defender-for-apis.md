---
layout: Conceptual
title: Alerts for Defender for APIs - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-defender-for-apis
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
description: This article lists the security alerts for Defender for APIs visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5bb9a995-7178-f2bb-890a-f8a32158bee7
document_version_independent_id: 2a7fd07d-b544-b06b-f4e6-ff5761291cf0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-defender-for-apis.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-defender-for-apis
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-defender-for-apis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 2eb2b226-c1b7-c345-b218-878be1ac1bd6
---

# Alerts for Defender for APIs - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for Defender for APIs from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Defender for APIs alerts

### **Suspicious population-level spike in API traffic to an API endpoint**

(API\_PopulationSpikeInAPITraffic)

**Description**: A suspicious spike in API traffic was detected at one of the API endpoints. The detection system used historical traffic patterns to establish a baseline for routine API traffic volume between all IPs and the endpoint, with the baseline being specific to API traffic for each status code (such as 200 Success). The detection system flagged an unusual deviation from this baseline leading to the detection of suspicious activity.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Informational

### **Suspicious spike in API traffic from a single IP address to an API endpoint**

(API\_SpikeInAPITraffic)

**Description**: A suspicious spike in API traffic was detected from a client IP to the API endpoint. The detection system used historical traffic patterns to establish a baseline for routine API traffic volume to the endpoint coming from a specific IP to the endpoint. The detection system flagged an unusual deviation from this baseline leading to the detection of suspicious activity.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Informational

### **Unusually large response payload transmitted between a single IP address and an API endpoint**

(API\_SpikeInPayload)

**Description**: A suspicious spike in API response payload size was observed for traffic between a single IP and one of the API endpoints. Based on historical traffic patterns from the last 30 days, Defender for APIs learns a baseline that represents the typical API response payload size between a specific IP and API endpoint. The learned baseline is specific to API traffic for each status code (for example, 200 Success). The alert was triggered because an API response payload size deviated significantly from the historical baseline.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial access

**Severity**: Informational

### **Unusually large request body transmitted between a single IP address and an API endpoint**

(API\_SpikeInPayload)

**Description**: A suspicious spike in API request body size was observed for traffic between a single IP and one of the API endpoints. Based on historical traffic patterns from the last 30 days, Defender for APIs learns a baseline that represents the typical API request body size between a specific IP and API endpoint. The learned baseline is specific to API traffic for each status code (for example, 200 Success). The alert was triggered because an API request size deviated significantly from the historical baseline.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial access

**Severity**: Informational

### **(Preview) Suspicious spike in latency for traffic between a single IP address and an API endpoint**

(API\_SpikeInLatency)

**Description**: A suspicious spike in latency was observed for traffic between a single IP and one of the API endpoints. Based on historical traffic patterns from the last 30 days, Defender for APIs learns a baseline that represents the routine API traffic latency between a specific IP and API endpoint. The learned baseline is specific to API traffic for each status code (for example, 200 Success). The alert was triggered because an API call latency deviated significantly from the historical baseline.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial access

**Severity**: Informational

### **API requests spray from a single IP address to an unusually large number of distinct API endpoints**

(API\_SprayInRequests)

**Description**: A single IP was observed making API calls to an unusually large number of distinct endpoints. Based on historical traffic patterns from the last 30 days, Defenders for APIs learns a baseline that represents the typical number of distinct endpoints called by a single IP across 20-minute windows. The alert was triggered because a single IP's behavior deviated significantly from the historical baseline.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Discovery

**Severity**: Informational

### **Parameter enumeration on an API endpoint**

(API\_ParameterEnumeration)

**Description**: A single IP was observed enumerating parameters when accessing one of the API endpoints. Based on historical traffic patterns from the last 30 days, Defender for APIs learns a baseline that represents the typical number of distinct parameter values used by a single IP when accessing this endpoint across 20-minute windows. The alert was triggered because a single client IP recently accessed an endpoint using an unusually large number of distinct parameter values.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial access

**Severity**: Informational

### **Distributed parameter enumeration on an API endpoint**

(API\_DistributedParameterEnumeration)

**Description**: The aggregate user population (all IPs) was observed enumerating parameters when accessing one of the API endpoints. Based on historical traffic patterns from the last 30 days, Defender for APIs learns a baseline that represents the typical number of distinct parameter values used by the user population (all IPs) when accessing an endpoint across 20-minute windows. The alert was triggered because the user population recently accessed an endpoint using an unusually large number of distinct parameter values.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial access

**Severity**: Informational

### **Parameter value(s) with anomalous data types in an API call**

(API\_UnseenParamType)

**Description**: A single IP was observed accessing one of your API endpoints and using parameter values of a low probability data type (for example, string, integer, etc.). Based on historical traffic patterns from the last 30 days, Defender for APIs learns the expected data types for each API parameter. The alert was triggered because an IP recently accessed an endpoint using a previously low probability data type as a parameter input.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Informational

### **Previously unseen parameter used in an API call**

(API\_UnseenParam)

**Description**: A single IP was observed accessing one of the API endpoints using a previously unseen or out-of-bounds parameter in the request. Based on historical traffic patterns from the last 30 days, Defender for APIs learns a set of expected parameters associated with calls to an endpoint. The alert was triggered because an IP recently accessed an endpoint using a previously unseen parameter.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Informational

### **Access from a Tor exit node to an API endpoint**

(API\_AccessFromTorExitNode)

**Description**: An IP address from the Tor network accessed one of your API endpoints. Tor is a network that allows people to access the Internet while keeping their real IP hidden. Though there are legitimate uses, it is frequently used by attackers to hide their identity when they target people's systems online.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-attack

**Severity**: Medium

### **API Endpoint access from suspicious IP**

(API\_AccessFromSuspiciousIP)

**Description**: An IP address accessing one of your API endpoints was identified by Microsoft Threat Intelligence as having a high probability of being a threat. While observing malicious Internet traffic, this IP came up as involved in attacking other online targets.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-attack

**Severity**: High

### **Suspicious User Agent detected**

(API\_AccessFromSuspiciousUserAgent)

**Description**: The user agent of a request accessing one of your API endpoints contained anomalous values indicative of an attempt at remote code execution. This does not mean that any of your API endpoints have been breached, but it does suggest that an attempted attack is underway.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Medium

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.