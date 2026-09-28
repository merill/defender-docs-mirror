---
layout: Conceptual
title: Connect SailPoint Identity Security Cloud to Microsoft Defender for Identity (Preview) - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/connect-sail-point
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
description: Learn how to connect your SailPoint Identity Security Cloud app to Defender for Identity using the API connector.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Himanch
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e6b3dc87-eb13-9772-7075-bd2f55f80df5
document_version_independent_id: e6b3dc87-eb13-9772-7075-bd2f55f80df5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/connect-sail-point.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: connect-sail-point
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/connect-sail-point.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 3c68cd9f-4ce0-5ad4-7777-67bf8067717e
---

# Connect SailPoint Identity Security Cloud to Microsoft Defender for Identity (Preview) - Microsoft Defender for Identity | Microsoft Learn

This article describes how to connect SailPoint Identity Security Cloud to Microsoft Defender for Identity by using the API connector in the Microsoft Defender portal. After you set up this integration, security administrators can gain visibility into SailPoint-managed identities, investigate identity-related threats, and monitor account activity directly from Defender for Identity. Before you start, make sure you have the required SailPoint IdentityNow Admin role and the necessary Microsoft Entra or Defender XDR permissions. For full details, review the prerequisites for connecting SailPoint.

## Prerequisites

Make sure you meet these requirements before you start:

**SailPoint Identity Security Cloud roles**

- The IdentityNow Admin role is required only to create an application.

**Microsoft Entra and Defender role-based access options**

Your account needs one of these access options to set up the connector:

- **Microsoft Entra roles:**

    - Security Operator
    - Security Admin
- **Defender Unified RBAC permission:**

    - Core security settings (manage)

## Connect SailPoint Identity Security Cloud to Microsoft Defender for Identity

To set up the connection, create a personal access token in SailPoint and then configure the connector in the Defender portal.

### Create a SailPoint Identity Security Cloud Personal Access Token

Before you begin, create a dedicated SailPoint Identity Security Cloud user for this integration. Then create a personal access token for that user:

1. Sign in to SailPoint Identity Security Cloud as the dedicated user.
2. Go to **User's Preferences &gt; Personal Access Tokens**.
3. Select **New Token**.
4. Add the following scopes to the token:
    1. idn:accounts:read
    2. idn:entitlement:read
    3. sp:search:read
    4. idn:accounts-state:manage
5. Copy the **Client ID** and **Secret**. You need these values later to finish the setup.

### Connect SailPoint Identity Security Cloud to Defender for Identity

Use the Defender portal to configure the SailPoint connector:

1. Sign in to the [Microsoft Defender Portal](https://security.microsoft.com).
2. Go to **System &gt; Data Management &gt; Data Connectors**.
3. Select **Catalog &gt; SailPoint Identity Security Cloud**.
4. Select **Connect a connector**

    1. Enter a name for your connector.
    2. Enter your SailPoint Identity Security Cloud API Endpoint URL. Use the value after `https://` and make sure 'api' is included in the URL. For example, `contoso.api.identitynow.com`.
    3. Enter your **Client ID** and **Client Secret**.

    [![Screenshot that shows where to enter the client ID and Client Secret in the Defender portal.](media/connect-sail-point/name-and-connection-details.png)](media/connect-sail-point/name-and-connection-details.png#lightbox)
5. Select **Next**.
6. Select **Protection Types &gt; Identity**, and then select **Next**.

    [![Screenshot that shows the selection of protection types in the Defender portal.](media/connect-sail-point/select-product-microsoft-defender-for-identity.png)](media/connect-sail-point/select-product-microsoft-defender-for-identity.png#lightbox)
7. Review the information and select **Connect**.
8. Verify that the SailPoint Identity connector appears in the **My Connector** table as **Connection Status: Ok**.