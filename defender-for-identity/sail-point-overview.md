---
layout: Conceptual
title: How Microsoft Defender for Identity protects your SailPoint Identity Security Cloud accounts - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/sail-point-overview
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how Microsoft Defender for Identity protect your SailPoint Identity Security Cloud and what the integration enables.
ms.date: 2026-03-04T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: himanch
locale: en-us
document_id: ce488127-dd8a-4144-1e16-d5d185a51339
document_version_independent_id: ce488127-dd8a-4144-1e16-d5d185a51339
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/sail-point-overview.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sail-point-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/sail-point-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: fe57c712-4e4f-3c85-06e2-ab3268ddbf4a
---

# How Microsoft Defender for Identity protects your SailPoint Identity Security Cloud accounts - Microsoft Defender for Identity | Microsoft Learn

Microsoft Defender for Identity helps protect your on-premises Active Directory and Microsoft Entra ID environments from advanced threats. Connecting SailPoint Identity Security Cloud with Microsoft Defender for Identity (MDI) gives you the ability to detect, investigate, and respond to identity-based threats across both cloud and on-premises infrastructures.

## What you can do after connecting SailPoint Identity Security Cloud to Microsoft Defender for Identity

After you connect SailPoint Identity Security Cloud, Microsoft Defender for Identity provides the following capabilities:

| Capability | Description |
| --- | --- |
| View SailPoint accounts in the identity inventory | - Adds SailPoint Identity Security Cloud accounts into the identity inventory and correlates them with identities from on-premises, Active Directory and Microsoft Entra ID. |
| Improve SailPoint security posture | Evaluates SailPoint Identity Security Cloud accounts for security risks such as stale privileged accounts and excessive privileged role assignments, and generates posture recommendations. Example recommendations include:  - Change password for SailPoint Identity Security Cloud privileged user accounts- Remove stale SailPoint Identity Security Cloud privileged accounts - Limit the number of SailPoint Identity Security Cloud accounts with system admin role - High number of SailPoint Identity Security Cloud accounts with a privileged role assigned  - Assign multifactor authentication for SailPoint privileged user accounts |
| Use advanced hunting to investigate SailPoint identities and their related activities | The [IdentityInfo](/en-us/defender-xdr/advanced-hunting-identityinfo-table) and the [IdentityEvents](/en-us/defender-xdr/advanced-hunting-identityevents-table) advanced hunting tables include inventory and event data from SailPoint Identity Security Cloud for investigation. |
| Take remediation actions | If an identity is determined to be at risk, the following remediation actions can be taken from within the Microsoft Defender portal: - Disable user in SailPoint Identity Security Cloud  - Enable user in SailPoint Identity Security Cloud |