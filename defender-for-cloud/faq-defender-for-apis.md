---
layout: FAQ
title: Common questions - Defender for APIs - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-defender-for-apis
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
description: Frequently asked questions about Defender for APIs
ms.topic: faq
ms.date: 2025-08-10T00:00:00.0000000Z
locale: en-us
document_id: cb61ec51-af06-8586-ae54-d10c23ab927b
document_version_independent_id: a6f1504e-fba0-f8e6-ce27-993983074a58
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-defender-for-apis.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-defender-for-apis
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-defender-for-apis.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bf4dbf7f-261c-4ae9-9fee-5989668a780a
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1c4b5d48-3f26-4bd8-9592-816d9c1a3420
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: e220c481-d8a1-01e6-da5b-40c103c04fe0
---

# Common questions - Defender for APIs - Microsoft Defender for Cloud | Microsoft Learn

## Availability and onboarding

### How can I onboard APIs to Microsoft Defender for APIs at scale?

After enabling the Defender for APIs plan on your Azure subscription, the next required step is to onboard individual APIs within your Azure API Management (APIM) instances. To help automate this process at scale, we provide sample PowerShell and CLI scripts that handle this second step of onboarding APIs. These scripts support onboarding at the APIM service level, subscription level, and tenant level, and are available in our [GitHub repository here](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/DefenderforAPIs-onboardAPIM-at-scale).

### I'm getting an error while onboarding APIs to Defender for APIs from the Recommendations page.

If you encounter errors like "Access Denied," "Forbidden," "Role Assignment not found," or "Authorization Failed," ensure you have the right level of permission for the Azure API Management service and Microsoft Defender for Cloud. You can find the [required set of permissions](defender-for-apis-introduction).  To fix the error "Request Header or Cookie Too Large," clear your browser cookies and try the operation again.

### Does onboarding APIs to Defender for APIs affect my Azure API Management service?

Enabling Defender for APIs monitoring coverage requires compute and memory utilization on the Azure API Management service. Monitor the performance of your Azure API Management service while onboarding APIs and scale out your Azure API Management resources when needed.

### I use Azure API Management Consumption tier offering. Can I use Defender for APIs?

No, support for Azure API Management consumption tier is currently not available.

### How does Defender for APIs handle support for API revisions in Azure API Management?

API revisions in Azure API Management are treated as separate API endpoints within Defender for Cloud because each revision is unique and might have its own security insights. The exception is during onboarding and offboarding to Defender for APIs, where all revisions are grouped together at the Azure API Management API level. Offline API revisions aren't eligible to onboard to Defender for Cloud, as they don't handle any traffic and therefore pose no security risk.

### Does Defender for APIs collect API traffic logs from Azure API Management?

Defender for APIs receives a copy of all HTTP request and response traffic sent to the API management service for all onboarded APIs. This process includes the request URL, the response status code, and a subset of HTTP headers for the requests and responses. Defender for APIs also receives a copy of some HTTP request and response bodies, capped at a size of 64 KB.

### Why can't I select multiple resources?

API Management service resources don't enable multi-selection with metrics. Let the API Management service team know this capability is important and upvote this request.

### Do I need to manually offboard APIs from Microsoft Defender for APIs before deleting them from API Management?

No, manual offboarding is not required. Microsoft Defender for APIs automatically detects when an API is deleted from Azure API Management and handles the cleanup accordingly. There is no impact on your API Management environment, and you can safely delete APIs without taking any additional steps in Defender. This behavior is fully supported and aligns with Microsoft's recommended practices.

## Questions related to region/geo

### I just moved my APIs within my Azure API Management service to a new region. Why are these APIs not updated?

APIs moved from one region to another require [offboarding](defender-for-apis-manage#offboard-an-api) and [onboarding](defender-for-apis-deploy) of the APIs.

### How do I enable Defender for APIs plan for a specific set of Azure API Management services?

Microsoft Defender for APIs plan is enabled at the subscription level. Select which APIs in Azure API Management from that subscription are onboarded for security coverage.

### I onboarded APIs from Azure API Management to Defender for APIs. However, they still appear under unhealthy resources on the recommendation page. Additionally, I don't see any security insights for the APIs I onboarded. Why?

Defender for APIs takes 30 minutes to generate the first security insights after onboarding an API and to move the onboarded APIs from unhealthy to healthy status. Thereafter, security insights are refreshed every 30 minutes.

### Why do security insights within the API collection details page show as "Awaiting Data"?

API endpoints that receive no traffic since onboarding to Defender for APIs display the message 'Awaiting data' under security insights. Until the API endpoint receives traffic, the security insight assessment can't be made.

### Why did the API endpoint insights and security recommendations reset back to "Awaiting Data" and "Not Applicable"?

Logic resets the API endpoint's status for the authentication, allows anonymous access, sensitive data classification, and external traffic observed/internet exposed assessments to "Awaiting Data" in the Defender for Cloud API Security dashboard. It also sets the status to "Not Applicable" in related security recommendations if no traffic is received for a certain period. This period is typically 30 days but might be reset sooner if the API endpoint's [Azure API management policies](/en-us/azure/api-management/api-management-howto-policies) are modified within Azure API Management.

### I have a self-hosted Azure API Management gateway. Can I use Defender for APIs for securing my APIs?

Currently, Defender for APIs support is limited to the cloud-hosted instances of Azure API Management gateways only.

### My Azure API Management service is in a virtual network. Do I need to have more connectivity configured for Defender for APIs?

No, Defender for APIs doesn't need special configuration for accessing API data from Azure API Management service behind a virtual network.

### What is the IP address shown in Defender for APIs alerts description page if x-forwarded-for is configured within our network?

Defender for APIs shows the IP address of the inbound IP address from client IPs. If x-forwarded-for is used, Defender for APIs validates the IP hops as part of the x-forwarded-for used within the request to show the most accurate IP that the inbound request is coming from.

### We use a custom domain URL within Azure API Management, does Defender for APIs show this URL as the Endpoint URL?

Custom domain URLs aren't shown within the Endpoint URL. The Defender for APIs Endpoint URL shows the base URL of your API Management API endpoint.

### Does Defender for APIs support APIs published in multi-region Azure API Management deployments?

Yes, all API security capabilities, including security posture and threat detections, are fully supported in Azure API Management multi-region deployments. This capability includes support for both primary and secondary regions.

## Questions about alerts in Defender for APIs

### How soon can we receive alerts on anomalous APIs?

APIs are assessed against their behavior by studying traffic for the past 30 days. The alerts on anomalous APIs might be generated sooner if the API receives significant traffic for the ML models to learn traffic behavior.

## Questions about Defender for APIs and WAF

### Is Azure WAF sufficient for securing APIs?

While Web Application Firewalls (WAF) are valuable for protecting applications, they might not provide complete security for APIs. WAFs apply generalized protection measures like dictionary, pattern, and signature mapping, which work well for applications with consistent traffic patterns. However, APIs are unique to each application and have dynamically changing nature, making the abstract protections offered by WAFs less effective.  APIs have different request and response payloads, and each consumer interacts with them in their own specific ways. The general dictionary, pattern, and signature mappings used by WAFs might not adequately offer complete in-depth protection for APIs due to their uniqueness. Although there are some cases where overlap exists, such as detecting and preventing SQL injection attacks, APIs often require more granular security measures.  To achieve the level of security needed for APIs, a solution like Microsoft Defender for APIs is