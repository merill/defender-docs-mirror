---
layout: Conceptual
title: Connect Okta to Microsoft Defender for Identity (Preview) - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/okta-integration
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
description: Learn how to connect your Okta app to Defender for Identity using the API connector.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms. reviewer: Himanch
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 63cba776-73ac-79dc-bbb2-db1a66b92714
document_version_independent_id: 63cba776-73ac-79dc-bbb2-db1a66b92714
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/okta-integration.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: okta-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/okta-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 92ec149f-5c75-852f-a836-db995e8258af
---

# Connect Okta to Microsoft Defender for Identity (Preview) - Microsoft Defender for Identity | Microsoft Learn

This page explains how to connect Microsoft Defender for Identity to your Okta account. Connecting Microsoft Defender for Identity to your Okta account provides visibility into Okta activity and enables shared data collection across Microsoft security products. The connector allows Defender for Identity to collect Okta system logs once and share them with other supported Microsoft security products, such as Microsoft Sentinel. Collecting Okta system logs once and sharing them across supported Microsoft security products reduces API usage, avoids duplicate data collection, and simplifies connector management. Before you begin, make sure your Okta and Defender for Identity environments meet the following prerequisites, including required licenses, roles, and access configurations.

Note

If your Okta environment is already integrated with [Protect Okta with Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/protect-okta), connecting it to Microsoft Defender for Identity can cause duplicate Okta data, such as user activity, to appear in the Defender portal.

## Prerequisites

Before connecting your Okta account to Microsoft Defender for Identity, make sure the following prerequisites are met:

### Okta licenses

Your Okta environment must have one of the following licenses:

- Developer
- Enterprise

### Okta roles

The Super Admin role is required only to create the API token. After you create the token, remove the Super Admin role and assign the Read-Only Administrator and Defender for Identity custom roles for ongoing API access.

### Microsoft Entra and Defender XDR role-based access options

To configure the Okta connector in Microsoft Defender for Identity, your account must have either of the following access configurations assigned:

- **Microsoft Entra roles:**

    - Security Operator
    - Security Admin
- **Defender unified RBAC permission:**

    - Core security settings (manage)

### Connect Okta to Microsoft Defender for Identity

The following procedure explains how to connect Microsoft Defender for Identity to your dedicated Okta account using the connector APIs. Connecting Microsoft Defender for Identity to your dedicated Okta account gives you visibility into and control over Okta use.

### Create a dedicated Okta account

Perform the following steps to create a dedicated Okta account for the connector.

1. Create a dedicated Okta account for Microsoft Defender for Identity use only.
2. Assign your Okta account as a Super Admin role.
3. Verify your Okta account.
4. Store the account credentials for later use.
5. Sign in to your dedicated Okta account created in step 1 to create an API token.

### Create an API token

Perform the following steps to create an API token in Okta.

1. In the Okta console, select **Admin**.

    ![Screenshot that shows how to access the Admin button in the Okta console.](media/okta-integration/okta-admin.png)
2. Select **Security** &gt; **API**.

    ![Screenshot of the Okta admin console navigation menu with Security and API options highlighted in the left pane.](media/okta-integration/okta-side-menu-security-api.png)
3. Select **Tokens**
4. Select **Create Token**.

    ![Screenshot of the Okta API Tokens tab with the Create token button highlighted.](media/okta-integration/create-an-okta-token.png)
5. In the Create token pop-up:

    1. Enter a name for your Defender for Identity token.
    2. Select **Any IP**.
    3. Select **Create token**.

    ![Screenshot of the Okta Create token form with fields for token name and IP restriction, and the Create token button highlighted.](media/okta-integration/enter-okta-token-details.png)
6. In the **Token created successfully** pop-up, copy the **Token value** and store it securely. The copied Okta API token is used to connect Okta to Defender for Identity.

    ![Screenshot of the Okta token creation success message.](media/okta-integration/okta-token-created-successfully.png)

### Add Custom user attributes

Add the required custom user attributes in Okta by completing the following steps.

1. Select **Directory &gt; Profile Editor**.
2. Select **User (default)**.
3. Select **Add Attributes**.

    1. Set Data type to String.
    2. Enter the Display name.
    3. Enter the Variable name.
    4. Set User permission to Read Only.
4. Enter the following attributes:

    | Display Name | Variable Name |
    | --- | --- |
    | ObjectSid | ObjectSid |
    | ObjectGuid | ObjectGuid |
    | DistinguishedName | DistinguishedName |
5. Select Save.
6. Verify that the three custom attributes you added are displayed correctly.

    ![Screenshot of the Okta Attributes page. Three attributes are shown: ObjectGuid, DistinguishedName, and ObjectSid.](media/okta-integration/okta-custom-attributes.png)

### Create a custom Okta role

Create a custom Okta role named Microsoft Defender for Identity to provide the permissions required for ongoing API access.

Note

To support ongoing API access, you must assign both the **Read-Only Administrator role** and the **custom Microsoft Defender for Identity role.** The Read-Only Administrator role and the custom Microsoft Defender for Identity role are mandatory to successfully configure the Okta connector. Configuration fails if either role is missing.

After you assign the Read-Only Administrator role and the custom Microsoft Defender for Identity role, you can remove the **Super Admin role**. Removing the Super Admin role after assigning both required roles ensures that only relevant permissions are assigned to your Okta account at all times.

1. Navigate to **Security &gt; Administrator**.
2. Select the **Roles** tab.
3. Select **Create new role**.
4. Set the role name to **Microsoft Defender for Identity**.
5. Select the permissions you want to assign to this role. Include the following permissions:
    - **Edit user's lifecycle states**
    - **Edit user's authenticator operations**
    - **View roles, resources, and admin assignments**
6. Select **Save role**.

![Screenshot showing a list of Okta permissions that need to be assigned when adding a custom role.](media/okta-integration/okta-permissions.png)

### Create a resource set

Create a resource set for the custom Defender for Identity role using the following steps.

1. Select the **Resources** tab.
2. Select **Create new resource set**.
3. Name the resource set **Microsoft Defender for Identity**.
4. Add the following resources:

    - **All users**
    - **All Identity and Access Management resources**

    ![Screenshot that shows the resource set name is Microsoft Defender for Identity.](media/okta-integration/resource-set-information.png)
5. Select **Save selection**.

### Assign the custom role and resource set

To complete the configuration in Okta, assign the custom role and resource set to the dedicated account.

1. Assign the following roles to the dedicated Okta account:

    - Read-Only Administrator.
    - The custom Microsoft Defender for Identity role
2. Assign the Microsoft Defender for Identity resource set to the dedicated Okta account.
3. After confirming that both the Read-Only Administrator role and the custom Microsoft Defender for Identity role are assigned, remove the Super Admin role from the account.

### Configure the connector in Microsoft Defender Portal

Use the following steps to configure the Okta connector in Microsoft Defender Portal.

1. Navigate to the Microsoft Defender Portal.
2. Select **System** &gt; **Data management** &gt; **Data connectors** &gt; **Catalog**

    [![Screenshot showing where to find the Okta connector in the Defender portal.](media/okta-integration/system-data-connector-catalog.png)](media/okta-integration/system-data-connector-catalog.png#lightbox)
3. Select **Okta Single Sign-On** &gt; **Connect a connector**.

    [![Screenshot that shows the connector option for Okta single sign-on.](media/okta-integration/select-okta-single-sign-on.png)](media/okta-integration/select-okta-single-sign-on.png#lightbox)
4. Enter a name for your connector.
5. Enter your Okta domain (for example, my.project.okta.com).
6. Paste the API token you copied from your Okta account.
7. Select **Next**.

    ![Screenshot that shows where to add the connector name, domain, and API key.](media/okta-integration/connect-new-okta-single-sign-on-connector.png)
8. **Select products &gt; Microsoft Defender for Identity**
9. Select **Next**

    [![Screenshot that shows the product page for connecting Okta to Microsoft Defender for Identity.](media/okta-integration/select-product-defender-for-identity.png)](media/okta-integration/select-product-defender-for-identity.png#lightbox)
10. Review Okta details, and select **Connect**.

    [![Screenshot that shows the Okta connector details.](media/okta-integration/review-okta-details.png)](media/okta-integration/review-okta-details.png#lightbox)
11. Verify that your Okta environment appears in the table as enabled.

    ![Screenshot that shows the Okta single sign-on connector was successfully connected.](media/okta-integration/okta-connected.png)

Note

Connecting the Okta connector can take up to 15 minutes.