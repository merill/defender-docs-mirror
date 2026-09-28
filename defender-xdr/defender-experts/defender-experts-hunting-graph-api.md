---
layout: Conceptual
title: Accessing incident notifications and DENs using Graph security API - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-hunting-graph-api
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Learn how to access Defender Experts Notifications (DENs) and related incident details by using the Microsoft Graph security API.
ms.service: defender-experts-for-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ean
ms.date: 2026-06-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 992a4e51-5400-465e-7020-0cacd28ad0eb
document_version_independent_id: 992a4e51-5400-465e-7020-0cacd28ad0eb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-hunting-graph-api.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-hunting-graph-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-hunting-graph-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 79d5d3a5-96a5-1c29-1260-aaa5dc4df8e3
---

# Accessing incident notifications and DENs using Graph security API - Microsoft Defender XDR | Microsoft Learn

[Defender Experts Notifications](defender-experts-hunting-onboarding#receive-defender-experts-notifications) are incidents that have been generated from hunting conducted by Defender Experts in your environment. They contain information regarding the hunting investigation and recommended actions provided by Defender Experts. You can now access DENs using the [Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview).

Note

Any incident in the Microsoft Defender portal is a collection of correlated alerts. [Microsoft Graph security incident resource type](/en-us/graph/api/resources/security-incident)

The following Defender Experts Notification details are available in the Microsoft Defender portal:

- **Incident title** - starts with *Defender Experts* to distinguish Defender Experts Notifications from other incidents
- **Executive summary** - provides an overview of the investigation summary
- **Recommendation summary** - lists the recommended actions from Defender Experts
- **Advanced hunting queries** - lists the converted KQL hunting queries used for the investigation

In Microsoft Graph security API, the following fields are also available:

- **Graph endpoint** - https://graph.microsoft.com/beta/security/incidents
- The following **field names**that correspond to the Defender Experts Notification details listed above:
    - displayName
    - description
    - recommendedActions
    - recommendedHuntingQueries

Note

The displayName, description, recommendedActions, and recommendedHuntingQueries fields will soon be available in the Graph v1.0 endpoint. For more information, see [Microsoft Graph REST API v1.0](/en-us/graph/api/resources/security-incident)

Your approach to consuming Defender Experts Notifications from the API will vary depending on the downstream system you intend to use and your specific requirements. However, the following steps are a basic implementation to help you get started:

**Starting from incidents in the Graph API**

1. Get incidents from Graph security API.
2. Check for new incidents where **displayName** starts with *Defender Experts*.
3. Continue reading the remaining fields for such incidents.
4. Synchronize the Defender Experts Notification (DEN) information into your downstream tool (for example, ServiceNow).

**Starting from alerts in the Graph API**

1. Get alerts from Graph security API.
2. Check for new alerts where **detectionSource** starts with *microsoftThreatExperts*.
3. Look up corresponding incident by checking **incidentId** listed on the alert.
4. Continue reading the remaining fields for such incidents.
5. Synchronize the Defender Experts Notification (DEN) information into your downstream tool (for example, ServiceNow).