---
layout: Conceptual
title: Connect CyberArk Identity to Microsoft Defender for Identity (Preview) - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/connect-cyber-ark
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
description: Learn how to connect your CyberArk Identity app to Defender for Identity using the API connector.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms. reviewer: Himanch
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d307114e-6e0c-5608-ffda-22f1c15149cc
document_version_independent_id: d307114e-6e0c-5608-ffda-22f1c15149cc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/connect-cyber-ark.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: connect-cyber-ark
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/connect-cyber-ark.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 2409996d-1c96-21e4-ec03-5f97a6652933
---

# Connect CyberArk Identity to Microsoft Defender for Identity (Preview) - Microsoft Defender for Identity | Microsoft Learn

Learn how to connect Microsoft Defender for Identity to your existing CyberArk Identity account by using the connector APIs. Connecting Defender for Identity to CyberArk Identity gives you visibility into and control over CyberArk identities. Before you begin, review the Prerequisites to confirm you have the required roles and permissions.

## Prerequisites

Before connecting your CyberArk Identity to Microsoft Defender for Identity, make sure the following prerequisites are met:

**CyberArk Identity roles**

- The System Admin role is required to create an application.

**Microsoft Entra and Defender role-based access options**

To configure the CyberArk Identity connector in Microsoft Defender for Identity, your account must have either of the following access configurations assigned:

- **Microsoft Entra roles:**

    - Security Operator
    - Security Admin
- **Defender Unified RBAC permission:**

    - Core security settings (manage)

## Connect CyberArk Identity to Microsoft Defender for Identity

This procedure explains how to connect Microsoft Defender for Identity to a dedicated CyberArk Identity account by using the connector APIs. Connecting Defender for Identity to a dedicated CyberArk Identity account gives you visibility into and control over CyberArk Identity use.

### Create a custom CyberArk Identity role

Create a custom role in CyberArk Identity with User Management administrative rights:

1. Sign in to CyberArk Identity console as a system administrator.
2. Navigate to **Identity Administration &gt; Core Services &gt; Roles**
3. Select **Add Role**.
4. Add an appropriate name for the custom role.
5. Select **Save**.
6. Select **Administrative Rights** and add rights for **User Management**.
7. Select **Save**.

### Create a CyberArk OAuth Confidential Client

To support ongoing API access, create a new user and assign the custom role. If you need to tag identities as privileged accounts in the Microsoft Defender portal, you must also add the user to the **Privileged Cloud Auditors** role.

1. Sign in to CyberArk Identity console as a system administrator.
2. Navigate to **Identity Administration &gt; Core Services &gt; Users**.
3. Select **Add User**.
4. Enter the **Login Name** and **Display Name**.
5. Under **Status**, select **Is OAuth confidential client**.
6. Copy the username and password. You enter these credentials when you configure the CyberArk Identity connector in the Microsoft Defender portal.
7. Select **Create User**.
8. Navigate to the custom role that you created in Create a custom CyberArk Identity role.
9. Select **Members** and add the user as a member.
10. Select **Save**.
11. Add the user to the **Privileged Cloud Auditors** role. This role is required to tag identities in the Microsoft Defender portal as privileged accounts.

### Connect CyberArk Identity to Defender for Identity

Configure the CyberArk Identity data connector in the Microsoft Defender portal:

1. Sign in to the [Microsoft Defender Portal](https://security.microsoft.com).
2. Go to **System &gt; Data Management &gt; Data Connectors**.

    [![Screenshot that shows where to find the data connector for CyberArk in the Microsoft Defender portal.](media/connect-cyber-ark/data-connector-cyber-ark.png)](media/connect-cyber-ark/data-connector-cyber-ark.png#lightbox)
3. Select **Catalog &gt; CyberArk Identity**.
4. Select on **Connect a connector**
5. Enter a name for your connector.
6. To determine the CyberArk Identity endpoint URL:

    1. In CyberArk Identity, select the signed-in user.
    2. Select **About**.
    3. Copy the **Identity ID** value.
    4. Add `.id.cyberark.cloud` to the Identity ID. For example, `contoso.id.cyberark.cloud`.
7. Enter your CyberArk Identity Privilege Cloud service endpoint.

    1. In the CyberArk Identity Admin console, go to **Identity Administration &gt; Settings &gt; Integration** and locate the **PVWA URL**. Use the value after `https://`. For example,`contoso.privilegecloud.cyberark.cloud`
8. Enter the username and password for the Oauth user. Include the complete username and the CyberArk domain.

    [![Screenshot that shows where to enter your CyberArk connector details in the Defender portal.](media/connect-cyber-ark/cyber-ark-connector-details.png)](media/connect-cyber-ark/cyber-ark-connector-details.png#lightbox)
9. Select **Next**.
10. Select **Protection Types &gt; Identity**, and select **Next**.
11. Review the information and select **Connect**.
12. Verify that the CyberArk Identity connector appears in the **My Connector** table as **Connection Status: Ok**.

    [![Screenshot that shows your CyberARk connector status in the Defender portal.](media/connect-cyber-ark/my-connectors-status.png)](media/connect-cyber-ark/my-connectors-status.png#lightbox)
13. To setup **Actions**, go to **Microsoft Sentinel &gt; Configuration &gt; Automation**.
14. Select **Integration profile** and create one for CyberArk by using the OAuth user's username and password.

    [![Screenshot that shows how to add an integration profile in the Defender portal.](media/connect-cyber-ark/add-integration-profile.png)](media/connect-cyber-ark/add-integration-profile.png#lightbox)