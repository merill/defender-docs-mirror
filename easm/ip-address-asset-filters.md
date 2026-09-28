---
layout: Conceptual
title: IP Address Asset Filters - Defender EASM IP address asset filters | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/ip-address-asset-filters
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
description: This article outlines the filter functionality available in Microsoft Defender External Attack Surface Management for IP address assets specifically, including operators and applicable field values.
author: danielledennis
ms.author: dandennis
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: fb8a39c6-fdfe-a6e6-6e4e-4f1f643f9e9f
document_version_independent_id: 2aa19489-4e9b-5171-6287-cf37bf91d5c8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/ip-address-asset-filters.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/ip-address-asset-filters
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/ip-address-asset-filters.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: aebcbd14-c8c6-2aac-2c81-08dcaab9a872
---

# IP Address Asset Filters - Defender EASM IP address asset filters | Microsoft Learn

This article provides a comprehensive reference for all filters that apply specifically to IP address assets in Microsoft Defender External Attack Surface Management. Use these filters when searching your inventory for a specific subset of IP addresses based on criteria such as port status, geolocation, web components, banners, and CVE scores. This article organizes the available filters into two categories: Defined value filters, which provide predefined options, and Freeform filters, which accept custom input. Each category lists the applicable operators and expected value formats.

## Defined value filters

The following filters provide a drop-down list of options to select. The available values are predefined.

| Filter name | Description | Value format | Applicable operators |
| --- | --- | --- | --- |
| IPv4 | Indicates that the host resolves to a 32-bit number notated in four octets (for example, 192.168.92.73). | true / false | `Equals``Not Equals` |
| IPv6 | Indicates that the host resolves to an IP comprised of 128-bit hexadecimal digits noted in eight four-digit groups. | true / false |  |
| Is Mail Server Record | Indicates that the host powers a mail server. | true / false |  |
| Is Name Server Record | Indicates that the host powers a name server. | true / false |  |
| Port Last Seen | Indicates the time frame in which a port was last observed on the host. | 7 days, 14 days, 30 days | `Equals``In` |

## Freeform filters

The following filters require that the user manually enters the value with which they want to search. This list is organized by the number of applicable operators for each filter, then alphabetically.

| Filter name | Description | Value format | Applicable operators |
| --- | --- | --- | --- |
| Port State | Indicates the status of the observed port. | Open, Filtered | `Equals``In` |
| Port | Any ports detected on the asset. | 443, 80 | `Equals``Not Equals``In``Not In` |
| ASN | Autonomous System Number is a network identification for transporting data on the Internet between Internet routers. An ASN will have associated public IP blocks tied to it where hosts are located. | 12345 | `Equals``Not Equals``In``Not In``Empty``Not Empty` |
| Banner | A banner is a text displayed by a host that provides details such as the type and version of software running on the system or server. | We recommend using the “matches” operator to search for HTML banners by keyword (for example, “HTTP/1.1”) | `Matches``Does not match``Matches in``Does not match in``Empty``Not empty` |
| Affected CVSS Score | Searches for assets with a CVE that matches a specific numerical score or range of scores. | Numerical (1-10), supports decimal values (for example, 8.6). | `Equals``Not Equals``In``Not In``Greater Than or Equal To``Less Than or Equal To``Between``Empty``Not Empty` |
| Affected CVSS v3 Score | Searches for assets with a CVE v3 that matches a specific numerical score or range of scores. | Numerical (1-10), supports decimal values (for example, 8.6). |  |
| Attribute Type | Additional services running on the asset. This can include IP addresses trackers. | address, AdblockPlusAcceptableAdsSignature | `Equals``Not Equals``Starts with``Does not start with``In``Not in``Starts with in``Does not start with in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |
| Attribute Type & Value | The attribute type and value within a single field. | address 192.168.92.73 |  |
| Attribute Value | The values for any attributes found on the asset. | 192.168.92.73 |  |
| CWE ID | Searches for assets by a specific CWE ID, or range of IDs. | CWE-89 |  |
| City | The city of origin detected for this asset. | Redmond |  |
| Country | The country/region of origin detected for this asset. | United States |  |
| Country Code | The applicable country code for the country/region of origin. | USA |  |
| IP Address | Any known IPs associated to the primary IP. | 192.168.92.73 |  |
| IP Block | The IP block that is associated with the asset. | 192.168.92.73/16 |  |
| State/Province | The state of origin detected for this asset. | Washington |  |
| State/Province Code | The state or province code associated with the state of origin. | WA |  |
| Web Component Type | The infrastructure type of a detected component. | Hosting Provider, DDOS Protection, Service, Server |  |
| Host | Any hosts associated with the asset. | host.contoso.com | `Equals``Not Equals``Starts with``Does not start with``Matches``Does Not Match``In``Not in``Starts with in``Does not start with in``Matches in``Does not match in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |
| Web Component Name | The name(s) of any web components running on the asset. | Netscaler Gateway, jQuery |  |
| Web Component Name & Version | A list of any detected web component names and associated versions that have been observed on the asset. | Netscaler Gateway 12.1, jQuery 3.4.1 |  |
| Web Component Version | The version number associated to any web component detected on the asset. | 12.1, 3.4.1 |  |