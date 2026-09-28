---
layout: Conceptual
title: How Microsoft Defender for Identity protects your CyberArk identity accounts - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/defender-for-identity-cyber-ark-overview
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
description: Learn how Microsoft Defender for Identity protect your CyberArk accounts and what the integration enables.
ms.date: 2026-02-15T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: himanch
locale: en-us
document_id: d479edcc-1927-fae7-b3de-fb427e269512
document_version_independent_id: d479edcc-1927-fae7-b3de-fb427e269512
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/defender-for-identity-cyber-ark-overview.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-for-identity-cyber-ark-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/defender-for-identity-cyber-ark-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 9d405a8b-a543-a5c6-1893-2387724ff81b
---

# How Microsoft Defender for Identity protects your CyberArk identity accounts - Microsoft Defender for Identity | Microsoft Learn

CyberArk Identity is a SaaS-based privileged access management (PAM) solution that manages privileged accounts across cloud and enterprise environments.

When you connect CyberArk Identity with Microsoft Defender for Identity, identity data from CyberArk Identity is added to the identity inventory and correlated with identities from on-premises Active Directory and Microsoft Entra ID. Accounts that are managed by CyberArk Identity as PAM accounts are tagged in the inventory.

## What you can do after connecting CyberArk Identity to Microsoft Defender for Identity

After you connect CyberArk Identity, Microsoft Defender for Identity provides the following capabilities:

| Capability | Description |
| --- | --- |
| View CyberArk accounts in the identity inventory | CyberArk users are added to the identity inventory in the Microsoft Defender portal. These accounts correlate with matching identities from Active Directory or Microsoft Entra ID, to allow unified tracking across platforms.  Additionally, Active Directory accounts that are managed by CyberArk Identity as PAM accounts are tagged in the inventory.  This applies only to AD accounts where the platform type in CyberArk Identity is a Windows Domain Account. |
| Improve CyberArk security posture | Evaluates CyberArk Identity accounts for security risks such as stale privileged accounts and excessive privileged role assignments, and generates posture recommendations. Example recommendations include:  - Change password for CyberArk Identity privileged user accounts- Remove stale CyberArk Identity privileged accounts - Limit the number of CyberArk Identity accounts with system admin role - High number of CyberArk Identity accounts with a privileged role assigned |
| Use advanced hunting to investigate CyberArk identities and their related activities | Captures CyberArk Identity inventory The [IdentityInfo](/en-us/defender-xdr/advanced-hunting-identityinfo-table) table includes account metadata such as privilege level, group membership, and identity source. |
| Take remediation actions | If an identity is determined to be at risk, the following remediation actions can be taken from within the MicrosoftDefender portal: - Disable user in CyberArk Identity  - Enable user in CyberArk Identity  - Reset password for PAM account in CyberArk Identity |