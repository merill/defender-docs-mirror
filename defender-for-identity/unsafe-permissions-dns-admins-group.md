---
layout: Conceptual
title: 'Security assessment: Unsafe permissions on the DnsAdmins group - Microsoft Defender for Identity | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/unsafe-permissions-dns-admins-group
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: LiorShapiraa
manager: bagol
ms.author: liorshapira
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: 'This recommendation lists any Group policy objects in your environment that contains password data. '
ms.topic: article
ms.date: 2024-10-05T00:00:00.0000000Z
ms.reviewer: LiorShapiraa
locale: en-us
document_id: a5235164-fe76-fbf3-4e2a-1c6666b5c496
document_version_independent_id: a5235164-fe76-fbf3-4e2a-1c6666b5c496
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/unsafe-permissions-dns-admins-group.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: unsafe-permissions-dns-admins-group
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/unsafe-permissions-dns-admins-group.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: bd477776-b02f-736c-c2f4-06bd0ddb2737
---

# Security assessment: Unsafe permissions on the DnsAdmins group - Microsoft Defender for Identity | Microsoft Learn

This recommendation lists any member of the DNS Admins group that is not a privileged user. Privileged accounts are accounts that are being members of a privileged group such as Domain admins, Schema admins, Read only domain controllers and so on. 

### Why is it important to review the members of the DnsAdmins group?

In AD, the DnsAdmins group is a privileged group that has administrative control over the DNS Server service within a domain. Members of this group have the ability to manage DNS servers, which includes tasks like configuring DNS zones, managing records, and modifying DNS settings. The DnsAdmins group can be delegated to non-AD administrators, like those managing networking functions such as DNS or DHCP, making these accounts attractive targets for compromise.

### How do I use this security assessment to improve my organizational security posture?

1. Review the list of exposed entities to identify non-privileged accounts with risky permissions.
2. Take appropriate action on those accounts by removing the accounts from the DnsAdmins group. If some accounts require these permissions, grant them only the specific access needed.

For example:![Screenshot of Unprivileged account.](media/unsafe-permissions-dns-admins-group/image.png)

### Next steps

[Learn more about Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)