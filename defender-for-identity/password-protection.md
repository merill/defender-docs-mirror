---
layout: Conceptual
title: Password protection in Microsoft Defender - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/password-protection
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-xdr
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how the Password protection page in Microsoft Defender helps you find leaked credentials, exposed passwords, and weak password policies across your identity sources.
ms.date: 2026-08-24T00:00:00.0000000Z
ms.topic: concept-article
ms.custom: msecd-doc-authoring-1020
ai-usage: ai-assisted
locale: en-us
document_id: cb40d730-d176-7a33-9d4e-6af1da84a359
document_version_independent_id: cb40d730-d176-7a33-9d4e-6af1da84a359
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/password-protection.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: password-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/password-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 63eb5be3-593e-6b69-0658-f7189bdcb651
---

# Password protection in Microsoft Defender - Microsoft Defender for Identity | Microsoft Learn

Compromised credentials remain one of the most common ways attackers gain initial access, even in environments that use multifactor authentication and modern authentication protocols. Password risks are often spread between different tools and identity providers, which can make it difficult for security teams to assess exposure and prioritize remediation.

The **Password protection** page in Microsoft Defender consolidates password-related risks from your identity sources into a single, prioritized view. Use it to find leaked credentials, exposed passwords, weak password policies, and configuration issues in on-premises Active Directory, Microsoft Entra ID, federated identities, non-Microsoft identity providers like Okta, and SaaS apps connected through Microsoft Defender for Cloud Apps. For each issue, you can see why an account is at risk and take action, such as resetting a password or disabling an account, directly from the page.

## Prerequisites

To access the **Password protection** page, you need:

- A Microsoft Defender for Identity license, or another license that includes Defender for Identity (such as E5), and a Microsoft Entra ID Protection license.
- A user role with at least [Security Reader](/en-us/azure/active-directory/roles/permissions-reference#security-reader) permissions.
- To review SaaS app sources, a Microsoft Defender for Cloud Apps license and an app connector for each SaaS app you want to see. Only SaaS apps that support SSPM appear.

## The Password protection page

In the Microsoft Defender portal, select **Identities** &gt; **Password protection**.

[![Screenshot of the Microsoft Defender Password protection page.](media/investigate-passwords/password-protection.png)](media/investigate-passwords/password-protection.png#lightbox)

The page includes a left panel where you select the identity source you want to review. Supported identity sources include:

- **Active Directory**: Available on all four tabs.
- **Microsoft Entra ID**: Available on the Leaked Credentials tab.
- **Okta**: Available on the Password Hygiene and Password Policies tabs.
- **SaaS apps**: Available on the Password Hygiene and Password Policies tabs for SaaS apps connected to Microsoft Defender for Cloud Apps that support SaaS Security Posture Management (SSPM), such as Salesforce and ServiceNow. For the full list, see [security configuration visibility per connected app](/en-us/defender-cloud-apps/enable-instant-visibility-protection-and-governance-actions-for-your-apps#user-app-governance-and-security-configuration-visibility).

The page has four tabs:

- **Password Hygiene**: Shows accounts with password weaknesses that attackers commonly exploit. Each item is a recommendation you can act on to reduce risk.
- **Password Policies**: Shows password policies from your identity providers side by side. Use this tab to check whether your policies meet current security standards. See Policy information for details.
- **Leaked Credentials**: Shows accounts with credentials that were found outside your organization, for example on public paste sites or the dark web. From this tab, you can reset passwords or disable accounts, individually or in bulk.
- **Exposed Passwords**: Shows accounts and settings that store or expose passwords in insecure ways, such as in plain text or in easily discoverable locations. Examples include clear-text credentials in Active Directory attributes (identified using AI-based detection) and reversible passwords in Group Policy Objects (GPOs).

## Policy information

The **Password Policies** tab shows:

| Column | Description |
| --- | --- |
| **Name** | The name of the password policy. |
| **Provider** | The identity provider that enforces the policy. |
| **Maximum password age** | The maximum number of days before a password must be changed. |
| **Minimum password age** | The minimum number of days before a password can be changed. |
| **Password history length** | The number of previous passwords that can't be reused. |
| **Password complexity** | Whether password complexity requirements are enabled. |
| **Lockout threshold** | The number of failed sign-in attempts before the account is locked. |
| **Lockout duration** | The duration of the account lockout after the threshold is reached. |

## Account information

The **Password Hygiene**, **Leaked Credentials**, and **Exposed Passwords** tabs show account-level data with this information:

[![Screenshot that shows the Password protection page with the Exposed passwords tab showing. ](media/investigate-passwords/password-protection-exposed-passwords.png)](media/investigate-passwords/password-protection-exposed-passwords.png#lightbox)

| Column | Description |
| --- | --- |
| **Name** | The display name of the account. |
| **SID** | The Security Identifier of the account. |
| **Entity type** | The type of entity (for example, User or Computer). |
| **Domain** | The Active Directory domain the account belongs to. |
| **Service account type** | The type of service account, if applicable. |