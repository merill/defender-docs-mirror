---
layout: Conceptual
title: Manage indicators in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/indicator-manage
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Edit, delete, or import file hash, IP address, URL/domain, and certificate indicators in Microsoft Defender for Endpoint from the Settings > Endpoints > Indicators page.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-asr
ms.topic: how-to
ms.subservice: asr
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 92dff577-08e3-9b1c-89dc-8f574dbd6b0b
document_version_independent_id: 92dff577-08e3-9b1c-89dc-8f574dbd6b0b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/indicator-manage.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: indicator-manage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/indicator-manage.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 5a75c9a3-ad65-7afc-483b-3722b634ba9a
---

# Manage indicators in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

1. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Indicators** (under **Rules**).
2. Select the tab for the indicator type you want to manage, such as **File hashes**, **IP addresses**, **URLs/domains**, or **Certificates**.
3. Update the indicator details, and then select **Save**. To remove the indicator from the list, select **Delete**.

## Import a list of IoCs

You can upload indicators from a CSV file that defines indicator attributes, actions, and other details.

Download the sample indicators CSV file from the **Indicators** import page (under **Settings** &gt; **Endpoints** &gt; **Indicators**) to review the supported column attributes.

1. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Indicators** (under **Rules**).
2. Select the tab of the entity type you'd like to import indicators for.
3. Select **Import** &gt; **Choose file**.
4. Select **Import**. Repeat for all the files you'd like to import.
5. Select **Done**.

Note

Only 500 indicators can be uploaded for each batch. Attempting to import indicators with specific categories requires the string to be written in Pascal case convention and only accepts the category list available in the Microsoft Defender portal.

The following table shows the supported parameters.

| Parameter | Type | Description |
| --- | --- | --- |
| indicatorType | Enum | Type of the indicator. Possible values are: `FileSha1`, `FileSha256`, `IpAddress`, `DomainName`, and `Url`. **Required** |
| indicatorValue | String | Identity of the [Indicator API resource](api/ti-indicator) entity. **Required** |
| action | Enum | The action that is taken if the indicator is discovered in the organization. Possible values are: `Allowed`, `Audit`, `BlockAndRemediate`, `Warn`, and `Block`. **Required** |
| title | String | Indicator alert title.**Required** |
| description | String | Description of the indicator.**Required** |
| expirationTime | DateTimeOffset | The expiration time of the indicator in the following format `YYYY-MM-DDTHH:MM:SS.0Z`. The indicator gets deleted if the expiration time passes and whatever happens at the expiration time occurs at the seconds (SS) value. **Optional** |
| severity | Enum | The severity of the indicator. Possible values are: `Informational`, `Low`, `Medium`, and `High`. **Optional** |
| recommendedActions | String | TI indicator alert recommended actions. **Optional** |
| rbacGroups | String | Comma-separated list of RBAC groups the indicator would be applied to. **Optional** |
| category | String | Category of the alert. Examples include: Execution and credential access. **Optional** |
| mitretechniques | String | MITRE techniques code/id (comma separated). For more information, see [Enterprise tactics](https://attack.mitre.org/tactics/enterprise/). **Optional**It's recommended to provide a value in the category field when you specify a MITRE technique in the mitretechniques field. |
| GenerateAlert | String | Whether the alert should be generated. Possible Values are: `True` or `False`. **Optional** |

Note

Classless Inter-Domain Routing (CIDR) notation for IP addresses is not supported. For more information, see [Microsoft Defender for Endpoint alert categories are now aligned with MITRE ATT&CK!](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/microsoft-defender-atp-alert-categories-are-now-aligned-with/ba-p/732748).

Network indicators do not support the action type, `BlockAndRemediate`. If a network indicator is set to `BlockAndRemediate`, it won't import.

Watch this video to learn how Microsoft Defender for Endpoint provides multiple ways to add and manage Indicators of compromise (IoCs).