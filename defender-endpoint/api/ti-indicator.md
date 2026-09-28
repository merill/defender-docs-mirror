---
layout: Conceptual
title: Indicator resource type - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/ti-indicator
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Specify the entity details and define the expiration of the indicator using Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2025-12-11T00:00:00.0000000Z
locale: en-us
document_id: ea579036-3d15-086e-ac08-0cd24d8eace2
document_version_independent_id: ea579036-3d15-086e-ac08-0cd24d8eace2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/ti-indicator.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/ti-indicator
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/ti-indicator.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: da69123e-cac5-0b1f-fae4-01ee5e52df81
---

# Indicator resource type - Microsoft Defender for Endpoint | Microsoft Learn

## Properties

| Property | Type | Description |
| --- | --- | --- |
| ID | String | Identity of the [Indicator](ti-indicator) entity. |
| indicatorValue | String | The value of the [Indicator](ti-indicator). |
| indicatorType | Enum | Type of the indicator. Possible values are: `FileSha1`, `FileSha256`, `FileMd5`, `CertificateThumbprint`, `IpAddress`, `DomainName`, and `Url`. |
| application | String | The application associated with the indicator. |
| action | Enum | The action that is taken if the indicator is discovered in the organization. Possible values are: `Warn`, `Block`, `Audit`, `Alert`, `AlertAndBlock`, `BlockAndRemediate`, and `Allowed`. |
| externalID | String | ID the customer can submit in the request for custom correlation. |
| sourceType | Enum | `User` in case the Indicator created by a user (for example, from the portal), `AadApp` in case it submitted using automated application via the API. |
| createdBySource | string | The name of the user/application that submitted the indicator. |
| createdBy | String | Unique identity of the user/application that submitted the indicator. |
| lastUpdatedBy | String | Identity of the user/application that last updated the indicator. |
| creationTimeDateTimeUtc | DateTimeOffset | The date and time when the indicator was created. |
| expirationTime | DateTimeOffset | The expiration time of the indicator. |
| lastUpdateTime | DateTimeOffset | The last time the indicator was updated. |
| severity | Enum | The severity of the indicator. Possible values are: `Informational`, `Low`, `Medium`, and `High`. |
| title | String | Indicator title. |
| description | String | Description of the indicator. |
| recommendedActions | String | Recommended actions for the indicator. |
| rbacGroupNames | List of strings | RBAC device group names where the indicator is exposed and active. Empty list in case it exposed to all devices. |
| rbacGroupIds | List of strings | RBAC device group IDs where the indicator is exposed and active. Empty list in case it exposed to all devices. |
| generateAlert | Enum | **True** if alert generation is required, **False** if this indicator shouldn't generate an alert. |

## Indicator Types

The indicator action types supported by the API are:

- Allowed
- Audit
- Block
- BlockAndRemediate
- Warn (Defender for Cloud Apps only)

For more information on the description of the response action types, see [Create indicators](../indicators-overview).

Note

AlertAndBlock and Alert are legacy response actions that were supported only until January 2022.

## Json representation

```json
{
    "id": "994",
    "indicatorValue": "881c0f10c75e64ec39d257a131fcd531f47dd2cff2070ae94baa347d375126fd",
    "indicatorType": "FileSha256",
    "action": "BlockAndRemediate",
    "application": null,
    "source": "user@contoso.onmicrosoft.com",
    "sourceType": "User",
    "createdBy": "user@contoso.onmicrosoft.com",
    "severity": "Informational",
    "title": "Michael test",
    "description": "test",
    "recommendedActions": "nothing",
    "creationTimeDateTimeUtc": "2019-12-19T09:09:46.9139216Z",
    "expirationTime": null,
    "lastUpdateTime": "2019-12-19T09:09:47.3358111Z",
    "lastUpdatedBy": null,
    "rbacGroupNames": ["team1"]
}
```