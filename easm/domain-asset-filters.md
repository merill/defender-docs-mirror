---
layout: Conceptual
title: Domain Asset Filters - Defender EASM domain asset filters | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/domain-asset-filters
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
description: This article outlines the filter functionality available in Microsoft Defender External Attack Surface Management for domain assets specifically, including operators and applicable field values.
author: danielledennis
ms.author: dandennis
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ff897784-6b56-1188-c409-e93dc98faa0c
document_version_independent_id: 266c097e-160f-58c3-2410-b59c915b95c6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/domain-asset-filters.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/domain-asset-filters
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/domain-asset-filters.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: e42655ae-729e-416c-f533-32e28bcaef6a
---

# Domain Asset Filters - Defender EASM domain asset filters | Microsoft Learn

This article lists the filters that specifically apply to domain assets in Microsoft Defender External Attack Surface Management. Use these filters to refine your inventory searches and locate a specific subset of domain assets. Each filter entry describes the filter's purpose, provides example values, and lists the applicable operators. Some filters offer predefined values from a drop-down list, while others require you to manually enter a value.

## Use defined-value domain asset filters

The following filters provide a drop-down list of options to select. The available values are predefined.

| Filter name | Description | Value format example | Applicable operators |
| --- | --- | --- | --- |
| Parked Domain | Indicates whether a website is registered but not connected to an online service (website, email hosting). | true / false | `Equals``Not Equals` |
| Domain Expiration | The registration expiry date range for the domain. | Expired, Expires in 30 days, Expires in 60 days, Expires in 90 days, Expires in &gt; 90 days | `Equals``Not Equals``In``Not In` |

## Use freeform domain asset filters

The following filters require that the user manually enters the value with which they want to search. This list is organized according to the number of applicable operators for each filter, then alphabetically. Note that many values are case-sensitive.

| Filter name | Description | Value format example | Applicable operators |
| --- | --- | --- | --- |
| Domain Status | Any detected domain configurations. | clientDeleteProhibited, clientRenewProhibited, clientTransferProhibited, clientUpdateProhibited | `Equals``Not Equals``Starts with``Does not start with``In``Not In``Starts with in``Does not start with in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |
| Domain | The domain name of the desired asset(s). | Must align with the standard format of domains in inventory: “domain.tld” | `Equals``Not Equals``Starts with``Does not start with``Matches``Does not match``In``Not In``Starts with in``Does not start with in``Matches in``Does not match in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |
| Name Server | Any name servers connected to the domain. | dns.domain.com |  |
| Registrar | The name of the registrar within the WhoIs record. | GODADDY.COM, INC. |  |
| Whois Admin Email | The email address of the listed administrator of a Whois record. | name@domain.com |  |
| Whois Admin Name | The name of the listed administrator. | John Smith |  |
| Whois Admin Organization | The organization associated with the administrator. | Contoso Ltd. |  |
| Whois Email | The primary contact email in a Whois record. | name@domain.com |  |
| Whois Registrant email | The email address of the listed registrant. | name@domain.com |  |
| Whois Registrant Name | The name of the listed registrant. | John Smith |  |
| Whois Registrant Organization | An organization associated with the listed registrant. | Contoso Ltd. |  |
| Whois Technical Email | The email address of the listed technical contact. | name@domain.com |  |
| Whois Technical Name | The name of the listed technical contact. | John Smith |  |
| Whois Technical Organization | The organization associated to the listed technical contact. | Contoso Ltd. |  |
| IANA ID | The allocated unique ID for a domain, IP or AS seen within WhoIs, IANA and ICANN records. | 1005 | `Equals``Not Equals``In``Not In``Empty``Not Empty` |