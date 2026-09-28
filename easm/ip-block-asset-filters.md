---
layout: Conceptual
title: IP Block Asset Filters - Defender EASM IP block asset filters | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/ip-block-asset-filters
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/133/azure
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
ms.service: defender-easm
description: This article outlines the filter functionality available in Microsoft Defender External Attack Surface Management for IP block assets specifically, including operators and applicable field values.
author: danielledennis
ms.author: dandennis
ms.date: 2026-06-15T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 738dd3ab-40fd-2aeb-4378-080f62d53792
document_version_independent_id: 44c88b56-1346-f64a-4f39-a5b4e6c7e4c9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/ip-block-asset-filters.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/ip-block-asset-filters
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/ip-block-asset-filters.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 463fc200-c58c-1015-0363-7c5da6f7de95
---

# IP Block Asset Filters - Defender EASM IP block asset filters | Microsoft Learn

This article lists the inventory filters available for IP block assets in Microsoft Defender External Attack Surface Management. Use these filters to search for a specific subset of IP blocks based on criteria such as IP version, ASN, BGP prefix, IP block range, and Whois registration details. Each filter supports specific operators and value formats, which are described in the tables below.

## Defined value filters

The following filters provide a drop-down list of options to select. The available values are predefined.

| Filter name | Description | Value format | Applicable operators |
| --- | --- | --- | --- |
| IPv4 | Indicates that the host resolves to a 32-bit number notated in four octets (example: 192.168.92.73). | true / false | `Equals``Not Equals` |
| IPv6 | Indicates that the host resolves to an IP comprised of 128-bit hexadecimal digits noted in 4-digit groups. | true / false |  |

## Freeform filters

The following filters require that the user manually enters the value with which they want to search. This list is organized according to the number of applicable operators for each filter, then alphabetically.

| Filter name | Description | Value format | Applicable operators |
| --- | --- | --- | --- |
| ASN | Autonomous System Number is a network identification for transporting data on the Internet between Internet routers. An ASN is associated to any public IP blocks tied to it where hosts are located. | 12345 | `Equals``Not Equals``In``Not In``Empty``Not Empty` |
| BGP Prefix | Any text values in the BGP prefix. | 123 4567 89 192.168.92.73/16 | `Equals``Not Equals``Starts with``Does not start with``In``Not in``Starts with in``Does not start with in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |
| IP Block | The IP block that is associated with the asset. | 192.168.92.73/16 |  |
| Whois Admin Email | The email address of the listed administrator of a Whois record. | name@domain.com |  |
| Whois Admin Name | The name of the listed administrator. | John Smith |  |
| Whois Admin Organization | The organization associated with the administrator. | Contoso Ltd. |  |
| Whois Email | The primary contact email in a Whois record. | name@domain.com |  |
| Whois Registrant Email | The email address of the listed registrant. | name@domain.com |  |
| Whois Registrant Name | The name of the listed registrant. | John Smith |  |
| Whois Registrant Organization | An organization associated with the listed registrant. | Contoso Ltd. |  |
| Whois Technical Email | The email address of the listed technical contact. | name@domain.com |  |
| Whois Technical Name | The name of the listed technical contact. | John Smith |  |
| Whois Technical Organization | The organization associated to the listed technical contact. | Contoso Ltd. |  |