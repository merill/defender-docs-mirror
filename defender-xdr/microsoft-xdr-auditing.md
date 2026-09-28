---
layout: Conceptual
title: Search the audit log for events in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/microsoft-xdr-auditing
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the audit log to search for Microsoft Defender XDR activities to help with investigation.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: bf41af45-bdbe-df6d-83e1-61119bf00cad
document_version_independent_id: bf41af45-bdbe-df6d-83e1-61119bf00cad
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/microsoft-xdr-auditing.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-xdr-auditing
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/microsoft-xdr-auditing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 014977cc-2413-1049-6c94-ee2edc2cba93
---

# Search the audit log for events in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

The audit log helps you investigate specific activities across Microsoft 365 services. In the Microsoft Defender portal, Microsoft Defender XDR and Microsoft Defender for Endpoint activities are audited.

Some of the audited activities include:

- Changes to data retention settings
- Changes to advanced features
- Creation of indicators of compromise
- Isolation of devices
- Add\edit\deletion of security roles
- Create\edit custom detection rules
- Assign user to an incidents

For a complete list of Microsoft Defender activities that are audited, see Microsoft Defender activities and Microsoft Defender for Endpoint activities.

Auditing is automatically turned on for Microsoft Defender. Features that are audited are logged in the audit log automatically. Auditing can also collect audit logs from GCC environments.

## Prerequisites

To access the audit log, you need to have the **View-Only Audit Logs** or **Audit Logs** role in Exchange Online. By default, those roles are assigned to the Compliance Management and Organization Management role groups.

Note

Global administrators in Office 365 and Microsoft 365 are automatically added as members of the Organization Management role group in Exchange Online.

Microsoft Defender uses the [Microsoft Purview auditing solution](/en-us/purview/audit-solutions-overview). Before you can look at the audit data in the Microsoft Defender portal, you need to turn on auditing in the Microsoft Purview portal. For more information, see [Turn auditing on or off](/en-us/purview/audit-log-enable-disable).

Important

Global Administrator is a highly privileged role that should be limited to scenarios when you can't use an existing role. Microsoft recommends that you use roles with the fewest permissions. Using accounts with lower permissions helps improve security for your organization.

## Search the audit log

You can search the audit log from the Microsoft Defender portal or the Microsoft Purview compliance portal. For detailed compliance portal instructions, see [Search the audit log in the compliance portal](/en-us/purview/audit-new-search). Audit log record retention is based on Microsoft Purview retention policies. For more information, see [Manage audit log retention policies](/en-us/purview/audit-log-retention-policies).

Follow these steps to search the audit log:

1. Go to the [Microsoft Defender portal's Audit page](https://security.microsoft.com/auditlogsearch). You can also open the [Purview compliance portal](https://purview.microsoft.com) and select **Audit**.

    [![Screenshot of the unified audit log page in Microsoft Defender XDR ](media/microsoft-xdr-auditing/unified-audit-log-xdr.png)](media/microsoft-xdr-auditing/unified-audit-log-xdr.png#lightbox)
2. On the **New Search** page, filter the activities, dates, and users you want to audit.
3. Select **Search**

    [![Screenshot of the unified audit log search options in Microsoft Defender XDR ](media/microsoft-xdr-auditing/unified-audit-search.png)](media/microsoft-xdr-auditing/unified-audit-search.png#lightbox)
4. Export your results to Excel for further analysis.

For step-by-step instructions, see [Search the audit log in the compliance portal](/en-us/purview/audit-new-search).

How long audit log records are kept depends on your Microsoft Purview retention policies. To learn more, see [Manage audit log retention policies](/en-us/purview/audit-log-retention-policies).

## Microsoft Defender XDR audit log activity reference

For a list of all events that are logged for user and admin activities in Microsoft Defender in the Microsoft 365 audit log, see:

- [Custom detection activities in Microsoft Defender in the audit log](/en-us/purview/audit-log-activities#microsoft-defender-xdr-custom-detection-activities)
- [Incident activities in Microsoft Defender in the audit log](/en-us/purview/audit-log-activities#microsoft-defender-xdr-custom-detection-activities)
- [Suppression rule activities in Microsoft Defender in the audit log](/en-us/purview/audit-log-activities#microsoft-defender-xdr-suppression-rule-activities)

## Microsoft Defender for Endpoint audit log activity reference

The Microsoft 365 audit log records user and admin activities in Defender for Endpoint. For details, see:

- [General settings activities in Defender for Endpoint in the audit log](/en-us/purview/audit-log-activities#microsoft-defender-for-endpoint-general-settings-activities)
- [Indicator settings activities in Defender for Endpoint in the audit log](/en-us/purview/audit-log-activities#microsoft-defender-for-endpoint-indicator-settings-activities)
- [Response action activities in Defender for Endpoint in the audit log](/en-us/purview/audit-log-activities#microsoft-defender-for-endpoint-reponse-actions-activities)
- [Roles settings activities in Defender for Endpoint in the audit log](/en-us/purview/audit-log-activities#microsoft-defender-for-endpoint-roles-settings-activities)

## Search for events using a PowerShell script

You can use the following PowerShell code snippet to query the Office 365 Management API for Microsoft Defender XDR events. The script connects to Exchange Online PowerShell, establishes a remote session, and then searches the unified audit log for a specified record type and date range.

Note

Before you run this script, identify the record type value you need. See the API column in [Audit log activities](/en-us/purview/audit-log-activities) for the record type values.

```PowerShell
$cred = Get-Credential
$s = New-PSSession -ConfigurationName microsoft.exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $cred -Authentication Basic -AllowRedirection 
Import-PSSession $s
Search-UnifiedAuditLog -StartDate 2023/03/12 -EndDate 2023/03/20 -RecordType <ID>
```

Note

See the API column in [Audit log activities](/en-us/purview/audit-log-activities) for the record type values.

For more information, see [Use a PowerShell script to search the audit log](/en-us/purview/audit-log-search-script)