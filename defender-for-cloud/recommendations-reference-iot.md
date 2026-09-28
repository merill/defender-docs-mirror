---
layout: Conceptual
title: Reference table for all IoT security recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/recommendations-reference-iot
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
description: This article lists all Microsoft Defender for Cloud IoT security recommendations that help you harden and protect your resources.
ms.topic: reference
ms.date: 2025-05-18T00:00:00.0000000Z
ms.custom: generated
ai-usage: ai-assisted
locale: en-us
document_id: fc6455e0-db9f-534d-ec81-c319d81dfc65
document_version_independent_id: e27f774d-0f65-28b8-137b-929325b1ca06
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/recommendations-reference-iot.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/recommendations-reference-iot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/recommendations-reference-iot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 19a0c426-556c-461a-cce0-3e26a0afa411
---

# Reference table for all IoT security recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

This article lists all the IoT security recommendations you might see in Microsoft Defender for Cloud.

The recommendations that appear in your environment are based on the resources that you're protecting and on your customized configuration. You can [see the recommendations in the portal](https://portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/5) that apply to your resources.

To learn about actions that you can take in response to these recommendations, see [Remediate recommendations in Defender for Cloud](implement-security-recommendations).

Tip

If a recommendation description says *No related policy*, usually it's because that recommendation is dependent on a different recommendation.

For example, the recommendation *Endpoint protection health failures should be remediated* relies on the recommendation that checks whether an endpoint protection solution is installed (*Endpoint protection solution should be installed*). The underlying recommendation *does* have a policy. Limiting policies to only foundational recommendations simplifies policy management.

## Azure IoT recommendations

### Default IP Filter Policy should be Deny

**Description**: IP Filter Configuration should have rules defined for allowed traffic and should deny all other traffic by default (No related policy).

**Severity**: Medium

### Diagnostic logs in IoT Hub should be enabled

**Description**: Enable logs and retain them for up to a year. This enables you to recreate activity trails for investigation purposes when a security incident occurs or your network is compromised. (Related policy: [Diagnostic logs in IoT Hub should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f383856f8-de7f-44a2-81fc-e5135b5c2aa4)).

**Severity**: Low

### Identical Authentication Credentials

**Description**: Identical authentication credentials to the IoT Hub used by multiple devices. This could indicate an illegitimate device impersonating a legitimate device. It also exposes the risk of device impersonation by an attacker (No related policy).

**Severity**: High

### IP Filter rule large IP range

**Description**: An Allow IP Filter rule's source IP range is too large. Overly permissive rules might expose your IoT hub to malicious intenders (No related policy).

**Severity**: Medium