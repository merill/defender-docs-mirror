---
layout: Conceptual
title: Microsoft Defender XDR incidents APIs and the incidents resource type - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-incident
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the methods and properties of the Incidents resource type in Microsoft Defender XDR.
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2026-08-07T00:00:00.0000000Z
locale: en-us
document_id: 17f015dd-423b-2d7d-91c5-3e5198948f05
document_version_independent_id: 17f015dd-423b-2d7d-91c5-3e5198948f05
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-incident.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-incident
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-incident.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: ee92f228-a108-2e56-cf1b-9ffe87915c5f
---

# Microsoft Defender XDR incidents APIs and the incidents resource type - Microsoft Defender XDR | Microsoft Learn

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview?view=graph-rest-1.0&amp;preserve-view=true).

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

An [incident](incidents-overview) is a collection of related alerts that help describe an attack. Events from different entities in your organization are aggregated automatically by Microsoft Defender. You can use the incidents API to programmatically access your organization's incidents and related alerts.

## Quotas and resource allocation

You can request up to 50 calls per minute or 1,500 calls per hour. Each method also has its own quotas. For more information on method-specific quotas, see the respective article for the method you want to use.

A `429` HTTP response code indicates that you've reached a quota, either by number of requests sent, or by allotted running time. The response body includes the time until the quota you reached is reset.

## Permissions

The incidents API requires different kinds of permissions for each of its methods. For more information about required permissions, see the respective method's article.

## Methods

| Method | Return Type | Description |
| --- | --- | --- |
| [List incidents](api-list-incidents) | [Incident](api-incident) list | Get a list of incidents. |
| [Update incident](api-update-incidents) | [Incident](api-incident) | Update a specific incident. |
| [Get incident](api-get-incident) | [Incident](api-incident) | Get a single incident. |

## Request body, response, and examples

Refer to the respective method articles for more details on how to construct a request or parse a response, and for practical examples.

## Common properties

| Property | Type | Description |
| --- | --- | --- |
| incidentId | long | Incident unique ID. |
| redirectIncidentId | nullable long | The Incident ID the current Incident was merged to. |
| incidentName | string | The name of the Incident. |
| createdTime | DateTimeOffset | The date and time (in UTC) the Incident was created. |
| lastUpdateTime | DateTimeOffset | The date and time (in UTC) the incident was last updated. Use this property to identify incidents that changed after they were created. |
| assignedTo | string | Owner of the Incident. |
| severity | Enum | Severity of the incident. Possible values are: `UnSpecified`, `Informational`, `Low`, `Medium`, and `High`. Severity can change as alerts are added to or removed from the incident. The incident resource doesn't provide a history of severity changes. |
| status | Enum | Specifies the current status of the incident. Possible values are: `Active`, `InProgress`, `Resolved`, and `Redirected`. |
| classification | Enum | Specification of the incident. Possible values are: `TruePositive`, `Informational, expected activity`, and `FalsePositive`. |
| determination | Enum | Specifies the determination of the incident. <br>Possible determination values for each classification are: <br>- **True positive**: `Multistage attack` (MultiStagedAttack), `Malicious user activity` (MaliciousUserActivity), `Compromised account` (CompromisedUser) – consider changing the enum name in public api accordingly, `Malware` (Malware), `Phishing` (Phishing), `Unwanted software` (UnwantedSoftware), and `Other` (Other).<br>- **Informational, expected activity:**`Security test` (SecurityTesting), `Line-of-business application` (LineOfBusinessApplication), `Confirmed activity` (ConfirmedUserActivity) - consider changing the enum name in public api accordingly, and `Other` (Other).<br>- **False positive:**`Not malicious` (Clean) - consider changing the enum name in public api accordingly, `Not enough data to validate` (InsufficientData), and `Other` (Other). |
| tags | string list | List of Incident tags (customTags only). |
| comments | List of incident comments | Incident Comment object contains: comment string, createdBy string, and createTime date time. |
| alerts | alert list | List of related alerts. See examples at [List incidents](api-list-incidents) API documentation. |

Note

Around August 29, 2022, previously supported alert determination values (`Apt` and `SecurityPersonnel`) will be deprecated and no longer available via the API.