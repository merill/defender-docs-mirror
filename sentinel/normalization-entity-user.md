---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) User Entity reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-entity-user
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
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
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: ofshezaf
description: This article displays the Microsoft Sentinel User Entity schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2025-07-18T00:00:00.0000000Z
locale: en-us
document_id: 89c23777-ea2c-72b9-dcd0-06c9486f6109
document_version_independent_id: 522af306-ff4b-b29c-c9b3-69b7a9b3396f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-entity-user.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-entity-user
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-entity-user.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 0b580678-6b3f-a854-c5a8-e087603daeca
---

# The Advanced Security Information Model (ASIM) User Entity reference | Microsoft Learn

Users are central to activities reported by events. The user entity fields listed in this section are used to describe the users involved in the action. When used in an event, prefixes are used to designate the role of a user entity in the activity. The prefixes `Src` and `Dst` are used to designate the user role in network related events, in which a source system and a destination system communicate. The prefixes 'Actor' and 'Target' are used for system oriented events such as process events.

## The user ID and scope

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **UserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the user. |
| **UserScope** | Optional | string | The scope in which UserId and Username are defined. For example, a Microsoft Entra tenant domain name. The UserIdType field represents also the type of the associated with this field. |
| **UserScopeId** | Optional | string | The ID of the scope in which UserId and Username are defined. For example, a Microsoft Entra tenant directory ID. The UserIdType field represents also the type of the associated with this field. |
| **UserIdType** | Optional | UserIdType | The type of the ID stored in the UserId field. |
| **UserSid**, **UserUid**, **UserAadId**, **UserOktaId**, **UserAWSId**, **UserPuid** | Optional | String | Fields used to store specific user IDs. Select the ID most associated with the event as the primary ID stored in UserId. Populate the relevant specific ID field, in addition to UserId, even if the event has only one ID. |
| **UserAADTenant**, **UserAWSAccount** | Optional | String | Fields used to store specific scopes. Use the UserScope field for the scope associated with the ID stored in the UserId field. Populate the relevant specific scope field, in addition to UserScope, even if the event has only one ID. |

The allowed values for a user ID type are:

| Type | Description | Example |
| --- | --- | --- |
| **SID** | A Windows user ID. | `S-1-5-21-1377283216-344919071-3415362939-500` |
| **UID** | A Linux user ID. | `4578` |
| **AADID** | A Microsoft Entra user ID. | `00aa00aa-bb11-cc22-dd33-44ee44ee44ee` |
| **OktaId** | An Okta user ID. | `00urjk4znu3BcncfY0h7` |
| **AWSId** | An AWS user ID. | `72643944673` |
| **PUID** | A Microsoft 365 user ID. | `10032001582F435C` |
| **SalesforceId** | A Salesforce user ID. | `00530000009M943` |

## The user name

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Username** | Optional | String | The source username, including domain information when available. Use the simple form only if domain information isn't available. Store the Username type in the UsernameType field. |
| **UsernameType** | Optional | UsernameType | Specifies the type of the username stored in the Username field. |
| **UserUPN**, **WindowsUsername**, **DNUsername**, **SimpleUsername** | Optional | String | Fields used to store additional usernames, if the original event includes multiple usernames. Select the username most associated with the event as the primary username stored in Username. |

The allowed values for a username type are:

| Type | Description | Example |
| --- | --- | --- |
| **UPN** | A UPN or Email address username designator. | `johndow@contoso.com` |
| **Windows** | A Windows username including a domain. | `Contoso\johndow` |
| **DN** | An LDAP distinguished name designator. | `CN=Jeff Smith,OU=Sales,DC=Fabrikam,DC=COM` |
| **Simple** | A simple user name without a domain designator. | `johndow` |
| **AWSId** | An AWS user ID. | `72643944673` |

## Additional user fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **UserType** | Optional | UserType | The type of source user. Supported values include: - `Regular` - `Machine` - `Admin` - `System` - `Application` - `Service Principal` - `Service` - `Anonymous` - `Other`. The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the OriginalUserType field. |
| **OriginalUserType** | Optional | String | The original destination user type, if provided by the reporting device. |