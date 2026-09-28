---
layout: Conceptual
title: SSL Certificate Asset Filters - Defender EASM SSL certificate asset filters | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/ssl-certificate-asset-filters
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
description: This article outlines the filter functionality available in Microsoft Defender External Attack Surface Management for SSL certificate assets specifically, including operators and applicable field values.
author: danielledennis
ms.author: dandennis
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3805945f-9399-4a5c-73cc-1699107e3367
document_version_independent_id: 8e7d1f95-7c15-544b-7bcb-9d2737cdf03a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/ssl-certificate-asset-filters.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/ssl-certificate-asset-filters
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/ssl-certificate-asset-filters.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: d374c71c-f5d4-1c92-aedf-ae72aa9ce1f9
---

# SSL Certificate Asset Filters - Defender EASM SSL certificate asset filters | Microsoft Learn

This article provides a reference for all filters available for SSL certificate assets in Microsoft Defender External Attack Surface Management. Use these filters to search your inventory for a specific SSL certificate or a select group of certificates based on defined or freeform filter values. Each filter listing includes applicable operators and accepted value formats to help you refine your queries.

## Defined value filters

The following filters provide a drop-down list of options to select. The available values are predefined.

| Filter name | Description | Value format | Applicable operators |
| --- | --- | --- | --- |
| Self Signed | Indicates whether the SSL certificate was self-signed. | True / False | `Equals``Not Equals` |
| Cert Expiration | The date when a certificate will expire. | Expired, Expires in 30 days, Expires in 60 days, Expires in 90 days, Expires in &gt; 90 days | `Equals``Not Equals``In``Not In` |
| Cert Validation | Indicates the method used to validate the cert, which is indicative of itss trustworthiness. | Domain, Organization, Extended | `Equals``Not Equals``In``Not In``Empty``Not Empty` |

## Freeform filters

The following filters require the user to manually enter a filter value to search for. This list is organized by the number of applicable operators for each filter, then alphabetically.

| Filter name | Description | Value format | Applicable operators |
| --- | --- | --- | --- |
| Cert Key Size | The number of bits within a SSL certificate key. | 2048 | `Equals``Not Equals``In``Not In``Greater Than or Equal To``Less Than or Equal To``Between``Empty``Not Empty` |
| Cert Key Algorithm | The key algorithm used to encrypt the certificate. | RSA | `Equals``Not Equals``Starts with``Does not start with``In``Not in``Starts with in``Does not start with in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |
| Cert Serial Number | The serial number associated with a certificate. | 426f9c536bf46487c641d1fc20529b39bb3 |  |
| Cert Signature Algorithm | The hash algorithm used to sign the certificate. | SHA256withRSA |  |
| Cert Signature Algorithm Oid | The OID identifying the hash algorithm used to sign the certificate request. | 1.2.840.113549.1.1.5 |  |
| Cert Issuer Alternative Name | Any alternative name(s) of the issuer of the certificate. | ZeroSSL ECC Domain Secure Site CA | `Equals``Not Equals``Starts with``Does not start with``Matches``Does Not Match``In``Not in``Starts with in``Does not start with in``Matches in``Does not match in``Contains``Does Not Contain``Contains In``Does Not Contain In``Empty``Not Empty` |
| Cert Issuer Common Name | The common name of the issuer. | ZeroSSL ECC |  |
| Cert Issuer Organization | The organization linked to the issuer. | GoDaddy.com, Inc. |  |
| Cert Issuer Organizational Unit | Indicates the department within an organization that is responsible for the issuing of the certificate. | http://certs.godaddy.com/repository/ |  |
| Cert Subject Alternative Name | Any alternative names for the subject (e.g. protected entity) of the SSL certificate. | `www.host.contoso.com` |  |
| Cert Subject Common Name | The Issuer Common Name of the subject of the SSL certificate. | host.contoso.com |  |
| Cert Subject Organization | The organization linked to the subject of the SSL certificate. | Contoso Ltd. |  |
| Cert Subject Organizational Unit | Indicates the department within a subject organization that is responsible for the certificate. | Compliance |  |