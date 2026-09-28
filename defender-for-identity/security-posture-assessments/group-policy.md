---
layout: Conceptual
title: Group policy security assessments - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/security-posture-assessments/group-policy
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
description: This section provides security assessments related to Group Policy Objects (GPOs) in Active Directory environments.
ms.topic: article
ms.date: 2025-09-15T00:00:00.0000000Z
ms.reviewer: LiorShapiraa
locale: en-us
document_id: 1e55d9fe-c33c-5cee-894f-d2ed2f24f127
document_version_independent_id: 1e55d9fe-c33c-5cee-894f-d2ed2f24f127
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/security-posture-assessments/group-policy.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-posture-assessments/group-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/security-posture-assessments/group-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 98f38c37-5d7a-a768-d259-a659347e27d5
---

# Group policy security assessments - Microsoft Defender for Identity | Microsoft Learn

## GPO can be modified by unprivileged accounts

**Description**

This recommendation lists any Group Policy Objects in your environment that can be modified by standard users which can potentially lead to the compromise of the domain.

Attackers may attempt to obtain information on Group Policy settings to uncover vulnerabilities that can be exploited to gain higher levels of access, understand the security measures in place within a domain, and identify patterns in domain objects. This information can be used to plan subsequent attacks, such as identifying potential paths to exploit within the target network or finding opportunities to blend in or manipulate the environment.

**User impact**

A user, service or application that relies on these permissions may stop functioning. 

**Implementation**

Carefully review each assigned permission, identify any dangerous permission granted, and modify them to remove any unnecessary or excessive user rights.