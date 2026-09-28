---
layout: Conceptual
title: Contact Asset Filters - Defender EASM contact asset filters | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/contact-asset-filters
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
description: This article outlines the filter functionality available in Microsoft Defender External Attack Surface Management for contact assets specifically, including operators and applicable field values.
author: danielledennis
ms.author: dandennis
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a61057b1-025b-04b9-8b20-529d2bdfe31d
document_version_independent_id: 397e6da2-8858-5db0-0b0f-d4e33962957b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/contact-asset-filters.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/contact-asset-filters
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/contact-asset-filters.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 235fc041-ade4-6ae7-97b5-69f51d82ca5e
---

# Contact Asset Filters - Defender EASM contact asset filters | Microsoft Learn

The following filters specifically apply to contact assets. Use the contact-asset filters when searching for a specific contact.

## Freeform filters

The following filters require that the user manually enters the value with which they want to search. This list is organized by the number of applicable operators for each filter, then alphabetically. Many of the manually entered values are case-sensitive.

| Filter name | Description | Value format | Applicable operators |
| --- | --- | --- | --- |
| Whois Email | The primary contact email in a Whois record. | name@domain.com | `Equals``Not Equals``Starts with``Does not start with``Matches``Does Not Match``In``Not in``Starts with in``Does not start with in``Matches in``Does not match in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |