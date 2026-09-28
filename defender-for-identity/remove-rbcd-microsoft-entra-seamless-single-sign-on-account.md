---
layout: Conceptual
title: 'Security assessment: Remove Resource Based Constrained Delegation for Microsoft Entra seamless SSO account - Microsoft Defender for Identity | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/remove-rbcd-microsoft-entra-seamless-single-sign-on-account
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: RonitLitinsky
manager: bagol
ms.author: rlitinsky
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: This article describes Microsoft Defender for Identity's Microsoft Entra Seamless Single sign-on (SSO) account with Resource Based Constrained Delegation (RBCD) applied security posture assessment report.
ms.topic: article
ms.date: 2024-08-22T00:00:00.0000000Z
ms.reviewer: LiorShapiraa
ms.custom: sfi-image-nochange
locale: en-us
document_id: 19ba0fe7-9e3b-93d3-4159-1f99183f7b56
document_version_independent_id: 19ba0fe7-9e3b-93d3-4159-1f99183f7b56
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/remove-rbcd-microsoft-entra-seamless-single-sign-on-account.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: remove-rbcd-microsoft-entra-seamless-single-sign-on-account
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/remove-rbcd-microsoft-entra-seamless-single-sign-on-account.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 92a78fdc-d29e-cd24-c4ec-f8f3f9891dba
---

# Security assessment: Remove Resource Based Constrained Delegation for Microsoft Entra seamless SSO account - Microsoft Defender for Identity | Microsoft Learn

This article describes Microsoft Defender for Identity's Microsoft Entra Seamless Single sign-on (SSO) account with Resource Based Constrained Delegation (RBCD) applied security posture assessment report.

Note

This security assessment will be available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services and Sign on method as part of Microsoft Entra Connect configuration is set to single sign-on and the SSO computer account exists. Learn more about Microsoft Entra seamless sign-on [here](/en-us/entra/identity/hybrid/connect/how-to-connect-sso).

## Why might the Microsoft Entra seamless SSO computer account with RBCD configured be a risk?

Microsoft Entra seamless SSO automatically signs in users when they're using their corporate desktops that are connected to your corporate network. Seamless SSO provides users with easy access to your cloud-based applications without using any other on-premises components. Seamless SSO creates a computer account named AZUREADSSOACC in each Windows Server AD Forest in your on-premises Windows Server AD directory. If resource-based constrained delegation is configured on the AZUREADSSOACC computer account, an account with the delegation would be able to generate service tickets for the AZUREADSSOACC account on behalf of any user and impersonate any user in the Microsoft Entra tenant that is synchronized from AD.

## How do I use this security assessment to improve my hybrid organizational security posture?

1. Review the recommended action at https://security.microsoft.com/securescore?viewid=actionsfor Remove Resource Based Constrained Delegation for Microsoft Entra seamless SSO account.
2. Review the list of exposed entities to discover which of your Microsoft Entra SSO computer accounts have RBCD applied.
3. Evaluate if the RBCD configuration for the AZUREADSSOACC account is essential for your operations. If the delegation is not required for critical functionalities, it’s safer to remove it by ensuring that the `msDS-AllowedToActOnBehalfOfOtherIdentity` attribute on any AZUREADSSOACC account is empty – this is the normal state for this account:

![Screenshot of the user details page.](media/remove-rbcd-microsoft-entra-seamless-single-sign-on-account/permissions.png)

Note

While assessments are updated in near real time, scores and statuses are updated every 24 hours. While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status may still take time until it's marked as **Completed**.