---
layout: Conceptual
title: Reference table for all API security recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/recommendations-reference-api
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
description: This article lists all Microsoft Defender for Cloud API security recommendations that help you harden and protect your resources.
ms.topic: reference
ms.date: 2026-06-18T00:00:00.0000000Z
ms.custom: generated
ai-usage: ai-assisted
locale: en-us
document_id: e8028809-bfaa-e378-2a99-a804390cf798
document_version_independent_id: 23cca93b-64c1-b639-f73b-336ae71c57fd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/recommendations-reference-api.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/recommendations-reference-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/recommendations-reference-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bf4dbf7f-261c-4ae9-9fee-5989668a780a
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1c4b5d48-3f26-4bd8-9592-816d9c1a3420
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: f851a9b8-851c-7416-05c9-ba512c48035f
---

# Reference table for all API security recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

This article lists all the API and API Management security recommendations you might see in Microsoft Defender for Cloud.

The recommendations that appear in your environment are based on the resources that you're protecting and on your customized configuration. You can [see the recommendations in the portal](https://portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/5) that apply to your resources.

To learn about actions that you can take in response to these recommendations, see [Remediate recommendations in Defender for Cloud](implement-security-recommendations).

## Azure API recommendations

### Microsoft Defender for APIs should be enabled

**Description & related policy**: Enable the Defender for APIs plan to discover and protect API resources against attacks and security misconfigurations. [Learn more](defender-for-apis-deploy)

**Severity**: High

### Azure API Management APIs should be onboarded to Defender for APIs

**Description & related policy**: Onboarding APIs to Defender for APIs requires compute and memory utilization on the Azure API Management service. Monitor performance of your Azure API Management service while onboarding APIs, and scale out your Azure API Management resources as needed.

**Severity**: High

### API endpoints that are unused should be disabled and removed from the Azure API Management service

**Description & related policy**: As a security best practice, API endpoints that haven't received traffic for 30 days are considered unused, and should be removed from the Azure API Management service. Keeping unused API endpoints might pose a security risk. These might be APIs that should have been deprecated from the Azure API Management service, but have accidentally been left active. Such APIs typically don't receive the most up-to-date security coverage.

**Severity**: Low

### API endpoints in Azure API Management should be authenticated

**Description & related policy**: API endpoints published within Azure API Management should enforce authentication to help minimize security risk. Authentication mechanisms are sometimes implemented incorrectly or are missing. This allows attackers to exploit implementation flaws and to access data. For APIs published in Azure API Management, this recommendation assesses authentication through verifying the presence of Azure API Management subscription keys for APIs or products where subscription is required, and the execution of policies for validating [JWT](/en-us/azure/api-management/validate-jwt-policy), [client certificates](/en-us/azure/api-management/validate-client-certificate-policy), and [Microsoft Entra](/en-us/azure/api-management/validate-azure-ad-token-policy) tokens. If none of these authentication mechanisms are executed during the API call, the API will receive this recommendation.

**Severity**: High

### Unused API endpoints should be disabled and removed from Function Apps

**Description & related policy**: API endpoints that haven't received traffic for 30 days are considered unused and pose a potential security risk. These endpoints may have been left active accidentally when they should have been deprecated. Often, unused API endpoints lack the latest security updates, making them vulnerable. To prevent potential security breaches, we recommend disabling and removing these HTTP-triggered endpoints from Azure Function Apps.

**Severity**: Low

### Unused API endpoints should be disabled and removed from Logic Apps

**Description & related policy**: API endpoints that haven't received traffic for 30 days are considered unused and pose a potential security risk. These endpoints may have been left active accidentally when they should have been deprecated. Often, unused API endpoints lack the latest security updates, making them vulnerable. To prevent potential security breaches, we recommend disabling and removing these endpoints from Azure Logic Apps.

**Severity**: Low

### Authentication should be enabled on API endpoints hosted in Function Apps

**Description & related policy**: API endpoints published within Azure Function Apps should enforce authentication to help minimize security risk. This is crucial to prevent unauthorized access and potential data breaches. Without proper authentication, sensitive data could be exposed, compromising the security of the system.

**Severity**: High

### Authentication should be enabled on API endpoints hosted in Logic Apps

**Description & related policy**: API endpoints published within Azure Logic Apps should enforce authentication to help minimize security risk. This is crucial to prevent unauthorized access and potential data breaches. Without proper authentication, sensitive data could be exposed, compromising the security of the system.

**Severity**: High

## API management recommendations

### API Management subscriptions shouldn't be scoped to all APIs

**Description & related policy**: API Management subscriptions should be scoped to a product or an individual API instead of all APIs, which could result in excessive data exposure.

**Severity**: Medium

### API Management calls to API backends shouldn't bypass certificate thumbprint or name validation

**Description & related policy**: API Management should validate the backend server certificate for all API calls. Enable SSL certificate thumbprint and name validation to improve the API security.

**Severity**: Medium

### API Management direct management endpoint shouldn't be enabled

**Description & related policy**: The direct management REST API in Azure API Management bypasses Azure Resource Manager role-based access control, authorization, and throttling mechanisms, thus increasing the vulnerability of your service.

**Severity**: Low

### API Management APIs should use only encrypted protocols

**Description & related policy**: APIs should be available only through encrypted protocols, like HTTPS or WSS. Avoid using unsecured protocols, such as HTTP or WS to ensure security of data in transit.

**Severity**: High

### API Management secret named values should be stored in Azure Key Vault

**Description & related policy**: Named values are a collection of name and value pairs in each API Management service. Secret values can be stored either as encrypted text in API Management (custom secrets) or by referencing secrets in Azure Key Vault. Reference secret named values from Azure Key Vault to improve security of API Management and secrets. Azure Key Vault supports granular access management and secret rotation policies.

**Severity**: Medium

### API Management should disable public network access to the service configuration endpoints

**Description & related policy**: To improve the security of API Management services, restrict connectivity to service configuration endpoints, like direct access management API, Git configuration management endpoint, or self-hosted gateways configuration endpoint.

**Severity**: Medium

### API Management minimum API version should be set to 2019-12-01 or higher

**Description & related policy**: To prevent service secrets from being shared with read-only users, the minimum API version should be set to 2019-12-01 or higher.

**Severity**: Medium

### API Management calls to API backends should be authenticated

**Description & related policy**: Calls from API Management to backends should use some form of authentication, whether via certificates or credentials. Doesn't apply to Service Fabric backends.

**Severity**: Medium