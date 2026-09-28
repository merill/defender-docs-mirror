---
layout: Conceptual
title: Files API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-files
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides information about using the Files API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: c9f8355f-21f7-50d4-9d53-b09f374ae8ff
document_version_independent_id: c9f8355f-21f7-50d4-9d53-b09f374ae8ff
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-files.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-files
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-files.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: aecc57c5-f2a6-4950-31cf-3c21844cc3c3
---

# Files API - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

- This API is not available for Microsoft 365 Cloud App Security.

The Files API provides you with metadata about the files and folders stored in your cloud apps, such as last modification date, ownership, and more.

The following lists the supported requests:

- [List files](api-files-list)
- [Fetch file](api-files-fetch)

## Filters

For information about how filters work, see [Filters](api-introduction#filters).

The following table describes the supported filters:

| Filter | Type | Operators | Description |
| --- | --- | --- | --- |
| service | integer | eq, neq | Filter files from specified app appID, for example: 11770 |
| instance | integer | eq, neq | Filter files from specified instances |
| fileType | integer | eq, neq | Filter files with the specified file type. Possible values include:**0**: Other**1**: Document**2**: Spreadsheet**3**: Presentation**4**: Text**5**: Image**6**: Folder |
| allowDeleted | boolean | eq | Possible values include:**true**: Returns deleted files**false** or not set: Returns nondeleted (including trashed) files. This value is overridden by the *trashed* operator |
| policy | array of strings | cabinetmatchedrulesequals, neq, isset, isnotset | Filter file matches and associated governance tasks related to the specified policies |
| filename | string | eq | Filter files by filename |
| modifiedDate | timestamp | lte, gte, range, lte\_ndays, gte\_ndays | Filter files by the date they were last modified |
| createdDate | timestamp | lte, gte, range | Filter files by the date they were created |
| collaborators.entity | entity pk | eq, neq | Filter files shared with specified entities. Example: `[{ "id": "entity-id", "inst": 0 }]` |
| collaborators.domains | string | eq, neq | Filter files shared with specified domains |
| collaborators.groups | string | eq, neq | Filter files shared with specified groups |
| collaborators.withDomain | string | eq, neq, deq | Filter files shared with specified domains |
| owner.entity | entity pk | eq, neq | Filter files owned by specified entities. Example: `[{ "id": "entity-id", "saas": 11161, "inst": 0 }]` |
| owner.orgUnit | string | eq, neq | Filter files with owners from specified organizational units |
| sharing | integer | eq, neq | Filter files with the specified sharing levels. Possible values include:**4**: Public (Internet)**3**: Public**2**: External**1**: Internal**0**: Private |
| fileId | string | eq, neq | Filter files by file ID |
| fileLabels | string | eq, neq, isset, isnotset | Filter files containing the specified file labels (tags) IDs |
| fileScanLabels | string | eq, neq, isset, isnotset | Filter files containing the specified content inspection warnings (tags) IDs |
| extension | string | eq, neq | Filter files by a given file extension |
| mimeType | string | eq, neq | Filter files by a given MIME type, must be a single string |
| trashed | boolean | eq | Possible values include:**true**: Returns only trashed files**false**: Returns nontrashed files |
| parentFolder | folder | eq, neq | Filter files contained in the specified folders |
| folder | boolean | eq | Possible values include:**true**: Returns only folders**false**: Returns only files |
| quarantined | boolean | eq | Possible values include:**true**: Returns only quarantined files**false**: Returns only nonquarantined files |
| snapshotLastModifiedDate | timestamp | lte, gte, range | Filter files by the date their snapshot was last modified |

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).