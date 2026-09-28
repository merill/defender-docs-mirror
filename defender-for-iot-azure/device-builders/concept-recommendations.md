---
layout: Conceptual
title: Security recommendations for IoT Hub - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-recommendations
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
ms.subservice: device-builders
description: Learn about the concept of security recommendations and how they're used in the Defender for IoT Hub.
ms.topic: reference
ms.date: 2023-01-01T00:00:00.0000000Z
locale: en-us
document_id: 8e3f3f89-5ef5-1ce5-6b7c-bd254fa110b8
document_version_independent_id: 60bdb194-84cc-a3fa-2823-ff264e103d68
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-recommendations.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-recommendations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/15394aaa-986f-4800-91ed-a516bac17284
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/208ef28a-da36-4c4d-b82e-a4702ac68c2e
platformId: 9e19f1fc-d790-7c8b-7cd8-2be7870ed235
---

# Security recommendations for IoT Hub - Microsoft Defender for IoT | Microsoft Learn

Defender for IoT scans your Azure resources and IoT devices and provides security recommendations to reduce your attack surface. Security recommendations are actionable and aim to aid customers in complying with security best practices.

In this article, you will find a list of recommendations, which can be triggered on your IoT Hub.

## Built in recommendations in IoT Hub

Recommendation alerts provide insight and suggestions for actions to improve the security posture of your environment.

### High severity

| Severity | Name | Data Source | Description | RecommendationType |
| --- | --- | --- | --- | --- |
| High | Same authentication credentials used by multiple devices | IoT Hub | IoT Hub authentication credentials are used by multiple devices. This could indicate an illegitimate device is impersonating a legitimate device and also exposes the risk of device impersonation by a malicious actor. | IoT\_SharedCredentials |
| High | High level permissions configured in IoT Edge model twin for IoT Edge module | IoT Hub | IoT Edge module is configured to run in privileged mode, with extensive Linux capabilities or with host-level network access (send/receive data to host machine). | IoT\_PrivilegedDockerOptions |

### Medium severity

| Severity | Name | Data Source | Description | RecommendationType |
| --- | --- | --- | --- | --- |
| Medium | Service principal not used with ACR repository | IoT Hub | Authentication schema used to pull an IoT Edge module from an ACR repository does not use Service Principal Authentication. | IoT\_ACRAuthentication |
| Medium | TLS cipher suite upgrade needed | IoT Hub | Unsecured TLS configurations detected. Immediate TLS cipher suite upgrade recommended. | IoT\_VulnerableTLSCipherSuite |
| Medium | Default IP filter policy should be deny | IoT Hub | By default, IP filter configuration needs rules defined for allowed traffic and should deny all other traffic. | IoT\_IPFilter\_DenyAll |
| Medium | IP filter rule includes a large IP range | IoT Hub | An IP filter rule source allowable IP range is too large. Overly permissive rules can expose your IoT Hub to malicious actors. | IoT\_IPFilter\_PermissiveRule |
| Medium | Recommended Rules for ip filter | IoT Hub | We Recommend you to change your IP filter to the following rules, the rules obtained by your IotHub behavior | IoT\_RecommendedIpRulesByBaseLine |
| Medium | SecurityGroup has inconsistent module settings | IoT Hub | Within this device security group, an anomaly device has inconsistent IoT Edge module settings when compared with the rest of the security group. | IoT\_InconsistentModuleSettings |

### Low severity

| Severity | Name | Data Source | Description | RecommendationType |
| --- | --- | --- | --- | --- |
| Low | IoT Edge Hub memory can be optimized | IoT Hub | Optimize your IoT Edge Hub memory usage by turning off protocol heads for any protocols not used by Edge modules in your solution. | IoT\_EdgeHubMemOptimize |
| Low | No logging configured for IoT Edge module | IoT Hub | Logging is disabled for this IoT Edge module. | IoT\_EdgeLoggingOptions |