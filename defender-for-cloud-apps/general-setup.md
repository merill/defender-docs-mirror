---
layout: Conceptual
title: Set up Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/general-setup
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
description: Set up your Defender for Cloud Apps environment and enable the Identity inventory integration to get a centralized view of identities.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 1db3ca85-2954-5dd0-79e4-42c4b9657972
document_version_independent_id: 1db3ca85-2954-5dd0-79e4-42c4b9657972
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/general-setup.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: general-setup
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/general-setup.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 3c4fde13-9bab-773c-7f1e-ca8ba5898ba2
---

# Set up Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn

The following procedure gives you instructions for customizing your Microsoft Defender for Cloud Apps environment.

## Prerequisites

For portal access requirements, see [Portal access](network-requirements#portal-access).

## Set up your Defender for Cloud Apps environment

Perform the following steps to set up your Defender for Cloud Apps environment:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **System** -&gt; **Organization details**, it's important that you provide an **Organization display name** for your organization.
3. Provide an **Environment name** (tenant). This information is especially important if you manage more than one tenant.
4. (Optional) Upload a **Logo** file to be displayed in email notifications and web pages sent from the system. The logo must be a .PNG file with a maximum size of 150 x 50 pixels, on a transparent background.

    Logos are stored in publicly accessible storage. The source URL for your image is protected and stored internally.

    Providing this image is voluntary, it’s up to you to decide if you want to share this data with us. You can also choose to delete the logo at any time, and the logo file will be deleted from our storage. This decision does not affect the security of your organization or your users in any way.
5. Make sure you add a list of your **Managed domains** to identify internal users. Adding managed domains is a crucial step. Defender for Cloud Apps uses the managed domains to determine which users are internal, external, and where files should and shouldn't be shared. Managed domain data is used for reports and alerts.

    - Users in domains that aren't configured as internal are marked as external. People outside the organization aren't scanned for activities or files.
6. If you're integrating with Microsoft Purview Information Protection, make sure you first enable the [App connector for Microsoft 365](connect-office-365). Then see [Microsoft Purview Information Protection Integration](azip-integration) for setup information.

## Enable Identity inventory integration

Enable Identity Inventory Integration to ingest cloud app accounts into the [Identity inventory](/en-us/defender-for-identity/identity-inventory), providing a centralized view of identities across on-premises, cloud, and SaaS environments.

Warning

After you enable Identity Inventory Integration, the integration can't be disabled.

Review the following important considerations before enabling this setting:

- As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate. These improvements **don't currently affect the following Defender for Cloud Apps capabilities**:

    - Built-in detections
    - UEBA (User and Entity Behavior Analytics)
    - Scoped deployment
    - Governance actions
    - Defender for Cloud Apps policies
    - Activity log
    - Cloud discovery user enrichment and anonymization
    - RBAC scoping

    These features continue to use the Cloud Application Accounts inventory. For more information, see [Cloud app accounts](accounts).
- The existing **Cloud Apps Accounts view remains available** to ensure backward compatibility.

### Prerequisites

To view the configuration page, you need any read or write role.

To change the configuration, you need one of the following roles:

- **Microsoft Entra ID roles**: Global Administrator, Security Administrator, or Cloud App Administrator
- **Defender for Cloud Apps built-in roles**: Global administrator

Tip

Use the least-privileged role that's sufficient for the task. Security Administrator or Cloud App Administrator is preferred over Global Administrator. If Global Administrator access is needed, consider using [Privileged Identity Management (PIM)](/en-us/entra/id-governance/privileged-identity-management/pim-configure) for just-in-time access.

To enable the integration:

1. In the Microsoft Defender portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **System**, select **Identity Inventory Integration**.
3. On the **Identity Inventory Integration** page, select the **Enable Identity Inventory Integration** checkbox.

    Note

    If Defender for Cloud Apps scoping is enabled for your tenant, the checkbox is unavailable.
4. Select **Confirm**.

After the integration is enabled, SaaS and cloud accounts are ingested into the Identity inventory. These accounts appear in the **Human identities** tab on the [Identity inventory](/en-us/defender-for-identity/identity-inventory) page.