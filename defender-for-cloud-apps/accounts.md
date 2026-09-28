---
layout: Conceptual
title: Investigate accounts from connected apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/accounts
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
description: Learn how to investigate accounts from connected apps in Microsoft Defender for Cloud Apps. Review account activity, permissions, group memberships, and access for people outside the organization.
ai-usage: ai-assisted
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: gayasalomon
ms.custom:
- msecd-doc-authoring-1016
- sfi-image-nochange
locale: en-us
document_id: 2e0fe252-465d-10de-ebdc-922b0d7e0f0a
document_version_independent_id: 2e0fe252-465d-10de-ebdc-922b0d7e0f0a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/accounts.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/accounts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: f85b2ad2-ed55-a681-2b57-c12c2aae7918
---

# Investigate accounts from connected apps - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps shows you account information from your connected applications. This article explains how to view and use the Cloud application accounts inventory to investigate accounts, filter by account type, and take actions on accounts from connected apps.

After you connect an app using the [App connector](/en-us/defender-cloud-apps/enable-instant-visibility-protection-and-governance-actions-for-your-apps), Defender for Cloud Apps reads account data including permissions, group memberships, aliases, and app usage.

When Defender for Cloud Apps detects a new account in a connected app, for example through activities or file sharing, it adds the account to the accounts list. This lets you see activity from people outside the organization in your cloud apps.

You can view the **Cloud application accounts** inventory from the tile at the top of the [Identity Inventory page](/en-us/defender-for-identity/identity-inventory).

Tip

If the [Identity inventory integration](/en-us/defender-cloud-apps/general-setup#enable-identity-inventory-integration) is enabled, cloud application accounts also appear in the **Human identities** tab on the Identity inventory page, providing a centralized view of all identities across your environment.

## Cloud application accounts page

The **Cloud application accounts** page shows details about accounts from connected cloud applications, including activity history and security alerts.

You can filter the tab to find specific accounts or narrow down to specific account types. For example, you can filter for all external accounts that haven't been accessed since last year.

Use the **Cloud application accounts** page to:

- Check for accounts that are inactive in a particular service and consider revoking their license.
- Filter for accounts with admin permissions.
- Search for accounts that belong to people who left your organization but might still be active.
- Take actions on accounts, such as suspending an app or opening the account settings page.
- View which accounts are included in each user group.
- See which apps are accessed by each account and which apps are deleted for specific accounts.

[![Screenshot of the Cloud application accounts tab showing account details, filters, and available actions.](media/accounts/cloud-application-accounts.png)](media/accounts/cloud-application-accounts.png#lightbox)

### Use account filters

The **Cloud application accounts** tab includes predefined filters for common scenarios. You can also turn on the **Advanced filters** toggle to filter by additional attributes or create conditions such as "does not equal".

Predefined filters include:

- **Account name**: Filter by specific accounts.
- **Affiliation**: Internal or external. Set internal accounts under **Settings** by defining the **IP address range of your organization**. Admin accounts are marked with a red tie icon.

    ![Icon indicating an admin account, shown as a red tie.](media/accounts-admin-icon.png)
- **App**: Filter by any connected app used by accounts in your organization.
- **Groups**: Filter by members of user groups in Defender for Cloud Apps, both built-in and imported user groups.
- **Show Admins only**: Filter for admin accounts only.

### Additional actions for cloud application accounts

You can take additional actions from the **Cloud application accounts** tab. Select the three dots at the end of an account's row to view options such as viewing related activities and incidents. Select the account row to see other accounts related to the same user.