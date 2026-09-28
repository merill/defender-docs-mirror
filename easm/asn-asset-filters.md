---
layout: Conceptual
title: ASN Asset Filters - Defender ASN domain asset filters | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/asn-asset-filters
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
description: This article outlines the filter functionality available in Microsoft Defender External Attack Surface Management for ASN assets specifically, including operators and applicable field values.
author: danielledennis
ms.author: dandennis
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 41152514-2e71-de0d-8da3-43e57e5a51a2
document_version_independent_id: ef08f054-33ac-81a3-0e7a-48f2df4bbccf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/asn-asset-filters.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/asn-asset-filters
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/asn-asset-filters.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: fbefc9b2-6562-7b64-ce41-2d06ef5ddebe
---

# ASN Asset Filters - Defender ASN domain asset filters | Microsoft Learn

This article lists the available filters for Autonomous System Number (ASN) assets in Microsoft Defender External Attack Surface Management. Each filter entry describes the filter's purpose, expected value format, and supported operators. Use these filters to refine your Defender EASM inventory searches and locate a specific ASN or group of ASNs.

## Freeform filters

These filters require you to type the search value yourself. The list is sorted by the number of operators each filter supports, then by name.

| Filter name | Description | Value format | Applicable operators |
| --- | --- | --- | --- |
| ASN | Autonomous System Number is a network identification for transporting data on the Internet between Internet routers. An ASN associates any public IP blocks tied to it where hosts are located. | 12345 | `Equals``Not Equals``In``Not In``Empty``Not Empty` |
| Whois Admin Email | The email address of the listed administrator of a Whois record. | name@domain.com | `Equals``Not Equals``Starts with``Does not start with``Matches``Does Not Match``In``Not in``Starts with in``Does not start with in``Matches in``Does not match in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |
| Whois Admin Name | The name of the listed administrator. | John Smith |  |
| Whois Admin Organization | The organization associated with the administrator. | Contoso Ltd. |  |
| Whois Email | The primary contact email in a Whois record. | name@domain.com |  |
| Whois Registrant Email | The email address of the listed registrant. | name@domain.com |  |
| Whois Registrant Name | The name of the listed registrant. | John Smith |  |
| Whois Registrant Organization | An organization associated with the listed registrant. | Contoso Ltd. |  |
| Whois Technical Email | The email address of the listed technical contact. | name@domain.com |  |
| Whois Technical Name | The name of the listed technical contact. | John Smith |  |
| Whois Technical Organization | The organization associated to the listed technical contact. | Contoso Ltd. |  |