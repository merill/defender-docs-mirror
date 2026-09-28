---
layout: Conceptual
title: Microsoft Sentinel DNS over AMA connector reference - available fields and normalization schema | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/dns-ama-fields
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
description: This article lists available fields for filtering DNS data using the Windows DNS Events via AMA connector, and the normalization schema for Windows DNS server fields.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: reference
ms.date: 2022-09-01T00:00:00.0000000Z
locale: en-us
document_id: f644c6b0-46b4-2d1f-8f43-9d0c8d11ac65
document_version_independent_id: 9ee019ca-f069-9000-4ea3-c25701399c58
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/dns-ama-fields.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/dns-ama-fields
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/dns-ama-fields.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 330d3f5e-7866-43b7-51d0-5bd85947d35c
---

# Microsoft Sentinel DNS over AMA connector reference - available fields and normalization schema | Microsoft Learn

Microsoft Sentinel allows you to stream and filter events from your Windows Domain Name System (DNS) server logs to the `ASimDnsActivityLog` normalized schema table. This article describes the fields used for filtering the data, and the normalization schema for the Windows DNS server fields.

The Azure Monitor Agent (AMA) and its DNS extension are installed on your Windows Server to upload data from your DNS analytical logs to your Microsoft Sentinel workspace. You stream and filter the data using the [Windows DNS Events via AMA connector](dns-ama-fields).

## Available fields for filtering

This table shows the available fields. The field names are normalized using the DNS schema.

| Field name | Values | Description |
| --- | --- | --- |
| EventOriginalType | Numbers between 256 and 280 | The Windows DNS eventID, which indicates the type of the DNS protocol event. |
| EventResultDetails | • NOERROR• FORMERR• SERVFAIL• NXDOMAIN• NOTIMP• REFUSED• YXDOMAIN• YXRRSET• NXRRSET• NOTAUTH• NOTZONE• DSOTYPENI• BADVERS• BADSIG• BADKEY• BADTIME• BADALG• BADTRUNC• BADCOOKIE | The operation's DNS result string as defined by the Internet Assigned Numbers Authority (IANA). |
| DvcIpAdrr | IP addresses | The IP address of the server reporting the event. This field also includes geo-location and malicious IP information. |
| DnsQuery | Domain names (FQDN) | The string representing the domain name to be resolved.• Can accept multiple values in a comma-separated list, and wildcards. For example:`*.microsoft.com,google.com,facebook.com`• Review these considerations for [using wildcards](connect-dns-ama#use-wildcards). |
| DnsQueryTypeName | • A• NS• MD• MF• CNAME• SOA• MB• MG• MR• NULL• WKS• PTR• HINFO• MINFO• MX• TXT• RP• AFSDB• X25• ISDN• RT• NSAP• NSAP-PTR• SIG• KEY• PX• GPOS• AAAA• LOC• NXT• EID• NIMLOC• SRV | The requested DNS attribute. The DNS resource record type name as defined by IANA. |

## ASIM normalized DNS schema

This table describes and translates Windows DNS server fields into the normalized field names as they appear in the [DNS normalization schema](normalization-schema-dns#schema-details).

| Windows DNS field name | Normalized field name | Type | Description |
| --- | --- | --- | --- |
| EventID | EventOriginalType | String | The original event type or ID. |
| RCODE | EventResult | String | The outcome of the event (success, partial, failure, NA). |
| RCODE parsed | EventResultDetails | String | The DNS response code as defined by IANA. |
| InterfaceIP | DvcIpAdrr | String | The IP address of the event reporting device or interface. |
| AA | DnsFlagsAuthoritative | Integer | Indicates whether the response from the server was authoritative. |
| AD | DnsFlagsAuthenticated | Integer | Indicates that the server verified all of the data in the answer and the authority of the response, according to the server policies. |
| RQNAME | DnsQuery | String | The domain needs to be resolved. |
| QTYPE | DnsQueryType | Integer | The DNS resource record type as defined by IANA. |
| Port | SrcPortNumber | Integer | Source port sending the query. |
| Source | SrcIpAddr | IP address | The IP address of the client sending the DNS request. For a recursive DNS request, this value is typically the reporting device's IP, in most cases, `127.0.0.1`. |
| ElapsedTime | DnsNetworkDuration | Integer | The time it took to complete the DNS request. |
| GUID | DnsSessionId | String | The DNS session identifier as reported by the reporting device. |