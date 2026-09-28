---
layout: Conceptual
title: Managing internal tokens (legacy) - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-tokens-legacy
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides information about the internal legacy method of generating and managing API tokens for Defender for Cloud Apps.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 1d40102e-c114-9361-7c07-cd0133b2ba86
document_version_independent_id: 1d40102e-c114-9361-7c07-cd0133b2ba86
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-tokens-legacy.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-tokens-legacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-tokens-legacy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 9eb5adac-3e99-ed74-e7c1-15f52ca79466
---

# Managing internal tokens (legacy) - Microsoft Defender for Cloud Apps | Microsoft Learn

In order to access the Defender for Cloud Apps API, you have to create an API token and use it in your software to connect to the API. This token is included in the header when Defender for Cloud Apps makes API requests.

The API tokens tab enables you to help you manage all the API tokens of your tenant.

## Generate a token

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **System**, select **API tokens**.
2. Select **Add token** and provide a name to identify the token in the future, and select **Generate**.

    ![Defender for Cloud Apps generates API token.](media/api-token-gen.png)
3. Copy the token value and save it somewhere for recovery - if you lose it you need to regenerate the token. The token has the privileges of the user who issued it. For example, a security reader can't issue a token that can alter data.
4. You can filter the tokens by status: Active, Inactive, or Generated.

    - **Generated:** Tokens that have never been used.
    - **Active:** Tokens that were generated and were used within the past seven days.
    - **Inactive:** Tokens that were used, but there was no activity in the last seven days.
5. After you generate a new token, you'll be provided with a new URL to use to access Defender for Cloud Apps.

    ![Defender for Cloud Apps API token.](media/generate-api-token.png)

    The generic portal URL continues to work but is considerably slower than the custom URL provided with your token. If you forget the URL at any time, you can view it by going to the **?** icon in the menu and selecting **About**.

## API token management

The API token page includes a table of all the API tokens that were generated.

Full admins see all tokens generated for this tenant. Other users only see the tokens that they generated themselves.

The table provides details about when the token was generated and when it was last used and allows you to revoke the token.

After a token is revoked, it's removed from the table, and the software that was using it fails to make API calls until a new token is provided.

Note

- SIEM connectors and log collectors also use API tokens. These tokens should be managed from the log collectors and SIEM agent sections and don't appear in this table.
- Deprovisioned users API tokens are retained in Defender for Cloud Apps but can't be used. Any attempt to use them will result in a permission denied response. However, we recommend that such tokens are revoked on the **API tokens** page.

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).