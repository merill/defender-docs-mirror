---
layout: Conceptual
title: How Microsoft Defender for Identity protects your Okta accounts - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/okta-defender-for-identity-overview
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
description: Learn how Microsoft Defender for Identity protect your Okta accounts and what the integration enables.
ms.date: 2025-08-07T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: himanch
locale: en-us
document_id: 98d2d148-03a6-216a-eb4e-4e457fd2bca9
document_version_independent_id: 98d2d148-03a6-216a-eb4e-4e457fd2bca9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/okta-defender-for-identity-overview.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: okta-defender-for-identity-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/okta-defender-for-identity-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: d0d1ec82-2c9d-c01a-c125-fa973a6e7666
---

# How Microsoft Defender for Identity protects your Okta accounts - Microsoft Defender for Identity | Microsoft Learn

Okta is a cloud-based identity and access management (IAM) platform that helps organizations control how users and administrators sign in and access enterprise applications. Okta manages high-value identities, including privileged accounts and API tokens. As a result, it’s a frequent target for misuse or attack. Many organizations use Okta alongside on-premises systems like Active Directory and cloud services like Microsoft Entra ID. This hybrid model can make it harder to monitor identity activity and detect threats consistently across platforms.

When you connect Okta to Microsoft Defender for Identity, you can extend your identity threat detection and investigation capabilities to include Okta-managed users. Defender for Identity ingests user and activity data from Okta and correlates it with identity data from Active Directory and Microsoft Entra ID. This integration gives you a centralized view of user activity, posture risks, and suspicious behavior across your identity infrastructure, and you can take the necessary remediation actions.

Note

The **Identity details** page in the Microsoft Defender portal shows the **Okta user risk score** only if the **Identity Threat Protection with Okta AI** feature is enabled. For more information, see [Risk scoring (Okta Identity Engine)](https://help.okta.com/oie/en-us/content/topics/security/security_risk_scoring.htm).

## What you can do after connecting Okta

With Okta connected, Defender for Identity provides the following capabilities:

| Capability | Description |
| --- | --- |
| View Okta accounts in the Identity Inventory | Defender for Identity adds Okta users to the identity inventory in the Microsoft Defender portal. These accounts correlate with matching identities from Active Directory or Microsoft Entra ID, to allow unified tracking across platforms. |
| Improve Okta security posture | Defender for Identity evaluates identity configuration in Okta and surfaces posture recommendations in Microsoft Secure Score. Example recommendations include:  - [Assign multifactor authentication to Okta privileged user accounts](/en-us/defender-for-identity/security-posture-assessments/cloud-identities#assign-multifactor-authentication-to-okta-privileged-user-accounts) - [Change password for Okta privileged user accounts](/en-us/defender-for-identity/security-posture-assessments/cloud-identities#change-okta-password-privileged-user-accounts.md) - [High number of Okta accounts with privileged role assigned](/en-us/defender-for-identity/security-posture-assessments/cloud-identities#high-number-of-okta-accounts-with-privileged-role-assigned.md) - [Highly privileged Okta API token](/en-us/defender-for-identity/security-posture-assessments/cloud-identities#highly-privileged-okta-api-token) - [Limit the number of Okta Super Admin accounts](/en-us/defender-for-identity/security-posture-assessments/cloud-identities#limit-number-okta-super-admin-accounts.md) - [Remove dormant Okta privileged accounts](/en-us/defender-for-identity/security-posture-assessments/cloud-identities#remove-dormant-okta-privileged-accounts.md) |
| Get alerts on suspicious Okta activity | Defender for Identity alerts you when it detects high-risk behavior in Okta, including anonymous sign-ins, privileged role assignments, and token abuse. These alerts are available in Microsoft Defender. When connected, Defender for Identity raises the following alerts based on Okta activity:  - Okta anonymous user access  - Privileged API token created  - Privileged API token updated  - Privileged Role assignment to Application  - Suspicious privileged role assignment  For a full list of supported alerts, see: [Defender for Identity Defender alerts](/en-us/defender-for-identity/alerts-xdr#initial-access-alerts). |
| Use advanced hunting to investigate Okta activity | Advanced hunting lets you investigate identity activity across different services including Okta, Active Directory, and Microsoft Entra ID.  The **IdentityInfo** table includes account metadata such as privilege level, group membership, and identity source.  The **IdentityEvents** table includes events related to those identities, such as sign-ins, authentication attempts, and identity-related alerts across supported identity providers.  To explore the full schema and build your own queries, see:  - [IdentityInfo](/en-us/defender-xdr/advanced-hunting-identityinfo-table) - [IdentityEvents(Preview)](/en-us/defender-xdr/advanced-hunting-identityevents-table). |
| Take remediation actions | When Microsoft Defender for Identity identifies an identity as at risk, you can take the following remediation actions directly from the Defender portal to update the user's status in Okta.  - Revoke all user's sessions  - Deactivate user in Okta  - Set user risk in Okta  For more information, see: [Remediation actions in Microsoft Defender for Identity](remediation-actions#roles-and-permissions). |