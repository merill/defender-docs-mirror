---
layout: Conceptual
title: How to search the audit logs for actions performed by Defender Experts - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-mdr-auditing
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: As a tenant administrator, you can use Microsoft Purview to search the audit logs for the actions Microsoft Defender Experts did in your tenant to perform their investigations.
ms.service: defender-experts-for-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-manage
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-dex
ms.date: 2026-06-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 0e3bb43d-ca4b-ba13-2461-306fb4cbd6d1
document_version_independent_id: 0e3bb43d-ca4b-ba13-2461-306fb4cbd6d1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-mdr-auditing.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-mdr-auditing
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-mdr-auditing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: a27c1faa-e779-ae77-cdc5-310e41010045
---

# How to search the audit logs for actions performed by Defender Experts - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender Experts MDR](defender-experts-mdr-overview)
- [Microsoft Defender Experts for Servers](defender-experts-servers-overview)

As a tenant administrator, you can use Microsoft Purview to search the audit logs for the times Microsoft Defender Experts signed into your tenant and the actions they did there to perform their investigations. You can also search the audit logs for the changes done by your tenant administrators to the Defender Experts settings.

Auditing is automatically turned on in the Microsoft Defender portal. Features that are audited are logged in the audit log automatically. Auditing can also collect audit logs from GCC environments.

Note

Make sure you have the right [permissions required for audit log search](/en-us/microsoft-365/compliance/audit-log-search#before-you-search-the-audit-log).

## Search the audit logs for actions performed by Defender Experts

Perform the following steps to search audit logs for actions performed by Defender Experts in your tenant:

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) to use [Audit New Search](/en-us/microsoft-365/compliance/audit-new-search).
2. Provide a **Date and time range (UTC)**.
3. Select the **Workload** and **Record type** from the list shown in the following table to further narrow your search.
4. Select **Search** to list the audit logs related to actions taken by our experts in your tenant.

[![Partial screenshot of Microsoft Purview portal Defender New search page.](media/auditing/audit.png)](media/auditing/audit.png#lightbox)

| Action performed by Defender Experts | Workload | Record type |
| --- | --- | --- |
| Sign into customer tenant | AzureActiveDirectory | AzureActiveDirectoryStsLogon |
| Make changes to incidents in Microsoft Defender portal | Microsoft365Defender | MS365Dincident |
| Make changes to alert suppression rules in Microsoft Defender portal | Microsoft365Defender | MS365DSuppressionRule |
| Make changes to indicators in Microsoft Defender for Endpoint | MicrosoftDefenderForEndpoint | MSDEIndicatorsSettings |
| Perform device remediation actions in Microsoft Defender for Endpoint | MicrosoftDefenderForEndpoint | MSDEResponseActions |

[![Partial screenshot of a sample audit log related to Defender Experts.](media/auditing/audit-2.png)](media/auditing/audit-2.png#lightbox)

## Search the audit logs for actions performed by your administrators in the Defender Experts settings

Perform the following steps to search audit logs for changes made by your administrators in the Defender Experts settings:

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) to use [Audit New Search](/en-us/microsoft-365/compliance/audit-new-search).
2. Provide a **Date and time range (UTC)**.
3. Under **Workload**, choose *MicrosoftDefenderExperts*.
4. Select **Search** to list the audit logs related to actions taken by your tenant administrators to the Defender Experts settings.

[![Partial screenshot of Microsoft Purview portal Defender New search page showing the Workload field selected to MicrosoftDefenderExperts.](media/auditing/audit-3.png)](media/auditing/audit-3.png#lightbox)

## Search the audit logs using a PowerShell script

In addition to using Audit New Search in the Microsoft Purview portal, you can use PowerShell cmdlets to search for audit logs. [Search the audit log with a PowerShell script](/en-us/microsoft-365/compliance/audit-log-search-script).