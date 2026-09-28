---
layout: Conceptual
title: MessageContents Table in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-messagecontents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how the MessageContents table in Microsoft Defender XDR gives security operations analysts Microsoft Teams message context for threat investigations.
author: poliveria
ms.author: pauloliveria
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.topic: reference
ms.custom: msecd-doc-authoring-1028
ms.date: 2026-09-25T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: cf1c9198-47de-e137-0fb5-6815c9b52509
document_version_independent_id: cf1c9198-47de-e137-0fb5-6815c9b52509
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-messagecontents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-messagecontents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-messagecontents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 87c4c9ad-9d30-7d23-a14b-303bc8b0d8f9
---

# MessageContents Table in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

The `MessageContents` table is an advanced hunting table in Microsoft Defender XDR. The table gives authorized security operations center (SOC) analysts access to Microsoft Teams message snippets and associated message metadata. Analysts can use the table to add message context to Teams threat investigations and correlate message information with security signals in other advanced hunting tables. Access requires advanced hunting and the Preview role.

Note

Custom detection rules and streaming aren't available for the `MessageContents` table.

## Prerequisites

- Access to advanced hunting.
- The Preview role, which includes the required message preview `Read` permission.

## Review MessageContents table data

The table contains supported Teams messages available through the underlying Teams message metadata source, including messages with URLs and federated messages.

| Column name | Data type | Description |
| --- | --- | --- |
| **`Timestamp`** | `datetime` | Date and time when the message was delivered |
| **`TeamsMessageId`** | `string` | Unique identifier for the message |
| **`ThreadId`** | `string` | Unique identifier for the channel or chat thread |
| **`ThreadName`** | `string` | Name of the channel or chat thread |
| **`MessageSnippet`** | `string` | Snippet of the message |
| **`ThreadType`** | `string` | Type of thread |
| **`SenderEmailAddress`** | `string` | Email address of the message sender |
| **`SenderObjectId`** | `string` | Object ID of the message sender |

## Correlate message data

You can join `MessageContents` with other advanced hunting tables to correlate Teams message information with other security signals during an investigation.

## Control access to MessageContents

Access to `MessageContents` is permission-controlled because the table can contain Teams message content. Users without the required advanced hunting and message preview permissions can't access or query the table.

Review which security administrators and SOC analysts in your organization need access to Teams message content for threat investigations. Use your organization's role-based access controls to limit access to the appropriate users.

When **Email & collaboration** &gt; **Defender for Office 365** permissions are active in Microsoft Defender XDR Unified role-based access control (RBAC), assign the Preview role through **Security operations/Raw data (email & collaboration)/Email & collaboration content (read)**. This assignment affects the Defender portal only, not PowerShell. For other role configurations, see [Actions on the Email entity page](/en-us/defender-office-365/mdo-email-entity-page#actions-on-the-email-entity-page).

No action is required if you don't want analysts to use this capability.