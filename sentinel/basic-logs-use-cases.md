---
layout: Conceptual
title: When to use the Microsoft Sentinel data lake | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/basic-logs-use-cases
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
description: Learn what log sources might be appropriate for the Microsoft Sentinel data lake and what attributes to look for, to decide about other sources.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: concept-article
ms.date: 2025-07-15T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: be047620-cb8f-6e29-12ec-1a0c1d7f1d38
document_version_independent_id: 0e46a66f-45c8-6891-f593-b372489a9f5b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/basic-logs-use-cases.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/basic-logs-use-cases
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/basic-logs-use-cases.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: edcf689e-bd00-684b-0dde-f001ff7ee522
---

# When to use the Microsoft Sentinel data lake | Microsoft Learn

This article highlights log sources to consider configuring as data lake tier only when enabling a connector. Before choosing a tier for which to configure a given table, check which tier is most appropriate for your use case. For more information about data categories and data tiers, see [Log retention plans in Microsoft Sentinel](log-plans).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Storage access logs for cloud providers

Storage access logs can provide a secondary source of information for investigations that involve exposure of sensitive data to unauthorized parties. These logs can help you identify issues with system or user permissions granted to the data.

Many cloud providers allow you to log all activity. You can use these logs to hunt for unusual or unauthorized activity, or to investigate in response to an incident.

## NetFlow logs

NetFlow logs are used to understand network communication within your infrastructure, and between your infrastructure and other services over Internet. Most often, you use this data to investigate command and control activity because it includes source and destination IPs and ports. Use the metadata provided by NetFlow to help you piece together information about an adversary on the network.

## VPC flow logs for cloud providers

Virtual Private Cloud (VPC) flow logs have become important for investigations and threat hunting. When organizations operate cloud environments, threat hunters need to be able to examine network flows between clouds or between clouds and endpoints.

## TLS/SSL certificate monitor logs

TLS/SSL certificate monitor logs have had outsized relevance in recent high profile cyber-attacks. While TLS/SSL certificate monitoring isn't a common log source, the logs provide valuable data for several types of attacks where certificates are involved. They help you understand the source of the certificate:

- Whether it was self-signed
- How it was generated
- If the certificate was issued from a reputable source

## Proxy logs

Many networks maintain a transparent proxy to provide visibility over traffic of internal users. Proxy server logs contain requests made by users and applications on a local network. These logs also contain application or service requests made over the Internet, such as application updates. What is logged depends on the appliance or solution. But the logs often provide:

- Date
- Time
- Size
- Internal host that made the request
- What the host requested

When you dig into the network as part of an investigation, proxy log data overlap can be a valuable resource.

## Firewall logs

Firewall event logs are often the most fundamental network log sources for threat hunting and investigations. Firewall event logs can reveal abnormally large file transfers, volume, frequency of communication by a host, probing connection attempts, and port scanning. Firewall logs are also useful as a data source for various unstructured hunting techniques, such as stacking ephemeral ports, or grouping and clustering different communication patterns.

## IoT Logs

A new and growing source of log data is Internet of Things (IoT)-connected devices. IoT devices might log their own activity and/or sensor data captured by the device. IoT visibility for security investigations and threat hunting is a major challenge. Advanced IoT deployments save log data to a central cloud service like Azure.