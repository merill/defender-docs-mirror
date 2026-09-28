---
layout: Conceptual
title: Manage related identities and accounts in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/manage-related-identities-accounts
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
description: Learn how to correlate accounts manually or with account correlation rules in Microsoft Defender for Identity, and unlink accounts that are no longer needed.
ms.date: 2026-07-23T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Almog Omrad
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1017
locale: en-us
document_id: c68d99d9-12a5-b0e0-1794-1cab42436b80
document_version_independent_id: c68d99d9-12a5-b0e0-1794-1cab42436b80
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/manage-related-identities-accounts.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-related-identities-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/manage-related-identities-accounts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 02fde170-2c3b-517e-daef-f9e6bb8ae784
---

# Manage related identities and accounts in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

In enterprise environments, identities are often fragmented. A single user might have multiple accounts across systems, including personal, privileged, legacy, cloud-based, or orphaned accounts. These accounts can cover on-premises Active Directory, Microsoft Entra ID, or non-Microsoft identity providers such as Okta and Ping.

Fragmentation makes it difficult to maintain a unified view of identity across the organization. Manually linking or unlinking related accounts in Microsoft Defender for Identity helps you:

- Correlate identity components across different systems.
- Improve protection by creating a complete identity context.
- Support investigations and response actions with unified identity views.

You can correlate accounts in either of the following ways:

- **Manual correlation**: Link individual accounts to an identity by using the procedures in this article.
- **Rule-based correlation**: Use account correlation rules to automatically correlate accounts. In the Microsoft Defender portal, go to **Settings** &gt; **Identities** &gt; **Account Correlation Rules**. For details, see [Manage account correlation rules](custom-account-correlation-rules).

For example:

- **Personal and privileged accounts**: A user might have two accounts, one for everyday work and another with elevated permissions for administrative tasks. For example:
    - `rick.hofer@contoso.onmicrosoft.com` (regular account)
    - `rhofer@contoso.onmicrosoft.com` (privileged account)
- **Multiple domains**: Large organizations often manage several domains. Linking accounts across these domains provides full visibility into a user's activity. For example:
    - `chris@fabrikam.com`
    - `chris@contoso.com`
- **Personal and service accounts**: A user might have both a personal account and a service account they own or manage. Linking those accounts helps connect ownership and responsibility to the same identity. For example:
    - `valeria.barrios@contoso.com`
    - `backup.service@contoso.com`
- **Legacy accounts**: A user might still have an active account in a legacy system. Linking accounts ensures the legacy account is monitored and tied back to the correct identity. For example:
    - `gabriela.laureano@contoso.com`
    - `glaureano@contosolegacy.local`
- **Accounts in multiple services**: A user might have a Microsoft Entra ID account, an Okta account, and a Ping account. Manually linking these accounts to the user's identity creates a consolidated view that supports identity-centric protection and investigation.

Use the procedures in this article to manually link accounts to identities and to manually unlink unused, legacy, or orphaned accounts from identities in Defender for Identity.

Note

As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate from the Identity inventory. Manual and policy-based identity correlations defined in the Identity inventory don't currently affect the following Defender for Cloud Apps features:

- Built-in detections
- UEBA (User and Entity Behavior Analytics)
- Scoped deployment
- Governance actions
- Defender for Cloud Apps policies
- Activity log
- Cloud discovery user enrichment and anonymization
- RBAC scoping

These Defender for Cloud Apps features continue to use the Cloud Application Accounts inventory.

## Prerequisites

Before you begin, ensure that you meet the following requirement:

- You must have [Unified role-based access control (URBAC)](/en-us/defender-for-identity/role-groups) roles: Global Administrator or Security Data (Manage).

## Manually link accounts to an identity in Defender for Identity

Use the following steps to manually link accounts to an identity in Defender for Identity.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Assets** &gt; **Identities**. Or, to go directly to the **Identity Inventory** page, use https://security.microsoft.com/identity-inventory.

    [![Screenshot of the identity inventory page in the Microsoft Defender portal.](media/identity-inventory/identity-inventory-page.png)](media/identity-inventory/identity-inventory-page.png#lightbox)
2. On the **Identities** tab of the **Identity Inventory** page, select an identity from the list by clicking on the **Display name** value.
3. On the identity details page that opens, select the **Observed in organization** tab, and verify the **Accounts** tab is selected.

    [![Screenshot that shows the accounts observed in an organization.](media/link-unlink-account-to-identity/accounts-observed-in-organization.png)](media/link-unlink-account-to-identity/accounts-observed-in-organization.png#lightbox)
4. On the **Accounts** tab, select ![](media/link-accounts.png)**Link**.
5. The **Link accounts** wizard opens. On the **Select accounts** page, use the search box to find an account. You can search by:

    - Display name
    - User principal name (UPN)
    - Security identifier (SID)
    - Source provider account

    Select one account by selecting the check box next to the **Display name** column, and then select **Next**.

    [![Screenshot that shows a list of accounts that you can link. ](media/link-unlink-account-to-identity/select-accounts.png)](media/link-unlink-account-to-identity/select-accounts.png#lightbox)
6. On the **Enter justification** page, enter a short explanation why you're linking these accounts. A valid explanation includes:

    - Up to 50 characters.
    - Letters, numbers, spaces, `@`, or `_`.

    Select **Next**.

    [![Screenshot that shows where to enter the justification for why you're linking the accounts.](media/link-unlink-account-to-identity/enter-justification.png)](media/link-unlink-account-to-identity/enter-justification.png#lightbox)
7. On the **Review and finish** page, review the information, and select **Back** to make changes. When you're finished, select **Submit**.

    [![Screenshot that shows the review of the selected accounts and the justification.](media/link-unlink-account-to-identity/review-and-finish.png)](media/link-unlink-account-to-identity/review-and-finish.png#lightbox)

    After the account is successfully linked, select **Done**

## Manually unlink legacy, orphaned, or unused accounts from an identity in Defender for Identity

Use the following steps to manually unlink legacy, orphaned, or unused accounts from an identity.

1. On the **Identities** tab of the **Identity Inventory** page at https://security.microsoft.com/identity-inventory, select an **Identity** from the list by clicking on the **Display name** value.
2. On the identity details page that opens, select the **Observed in organization** tab, and verify the **Accounts** tab is selected.
3. On the **Accounts** tab, select the account you want to unlink from the identity by selecting the check box next to the **Display name** column, and then select ![](media/unlink-accounts.png)**Unlink**.
4. In the **Unlink accounts from ...** confirmation dialog that opens, read the information, and then select **Unlink accounts**.

## What to expect after linking or unlinking an account in Defender for Identity

After you link or unlink an account, the following changes occur:

- The selected accounts are linked or unlinked immediately.
- The system updates the identity context and refreshes the account list.