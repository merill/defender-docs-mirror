---
layout: Conceptual
title: Cloud discovery data anonymization - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/cloud-discovery-anonymizer
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
description: This article provides information about how to protect user privacy by anonymizing the usernames in your cloud discovery data.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom:
- msecd-doc-authoring-1016
- sfi-ga-blocked
- sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 16307b9c-711d-c09f-5016-79c83e17bfda
document_version_independent_id: 16307b9c-711d-c09f-5016-79c83e17bfda
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/cloud-discovery-anonymizer.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cloud-discovery-anonymizer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/cloud-discovery-anonymizer.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: cacacbc1-0e30-35e6-ebb6-0a1d97df6fe8
---

# Cloud discovery data anonymization - Microsoft Defender for Cloud Apps | Microsoft Learn

Cloud discovery data anonymization enables you to protect user privacy. Once the data log is uploaded to Microsoft Defender for Cloud Apps, the log is sanitized and all username information is replaced with encrypted usernames. By replacing usernames with encrypted values, all cloud activities are kept anonymous. When necessary, for a specific security investigation (for example, a security breach or suspicious user activity), admins can resolve the real username. If an admin has a reason to suspect a specific user, they can also look up the encrypted username of a known username, and then start investigating using the encrypted username. Each username conversion is audited in the portal's **Governance log**.

Key points:

- No private information is stored or displayed. Only encrypted information.
- Private data is encrypted using AES-128 with a dedicated key per tenant.
- Resolving usernames is done ad-hoc, per-username by deciphering a given encrypted username.
- Anonymization capabilities aren't supported when using the "Defender for Cloud Apps Proxy" stream.
- As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate. Cloud discovery data anonymization uses a separate data pipeline that isn't yet integrated with the [Identity inventory](/en-us/defender-for-identity/identity-inventory). Correlations defined in the Identity inventory don't affect anonymization. For a full list of affected features, see [Enable Identity inventory integration](/en-us/defender-cloud-apps/general-setup#enable-identity-inventory-integration).

## Prerequisites

To resolve (deanonymize) usernames in Cloud Discovery data:

- You must have the [Cloud Discovery global admin](manage-admins#built-in-admin-roles-in-defender-for-cloud-apps) role with anonymization permissions enabled during role assignment.

Note

Microsoft recommends that you use roles with the fewest permissions. Using roles with the fewest permissions helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## How data anonymization works

1. There are three ways to apply data anonymization:

    - You can set the data from a specific log file to be anonymized, by selecting **Anonymize private information** when you [create a snapshot cloud discovery report](create-snapshot-cloud-discovery-reports). Select **Anonymize private information**.![Screenshot of the option to anonymize private information when creating a snapshot report.](media/anonymize-log.png)
    - You can anonymize data from a new data source by selecting **Anonymize private information** when you [set up an automated log upload](discovery-docker).![Screenshot of the option to anonymize private information for an automated data source upload.](media/anonymize-autolog.png)
    - You can set the default in Defender for Cloud Apps to anonymize all data from both snapshot reports from uploaded log files and continuous reports from log collectors as follows:

        1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
        2. Under **Cloud Discovery**, select **Anonymization**. To anonymize usernames by default, select **Anonymize private information by default in new reports and data sources**. You can also select **Anonymize device information by default in 'Defender-managed endpoints' report**.
2. When anonymization is selected, Defender for Cloud Apps parses the traffic log and extracts specific data attributes.
3. Defender for Cloud Apps replaces the username with an encrypted username.
4. Defender for Cloud Apps then analyzes cloud usage data and generates cloud discovery reports based on the anonymized data.

    ![Screenshot of the cloud discovery dashboard displaying anonymized usage data.](media/anonymize-dashboard.png)
5. For a specific investigation, such as an investigation of an anomalous usage alert, you can resolve the specific username in the portal and provide a business justification.

    Note

    The following steps also work for device names on the **Devices** tab.

    **To resolve a single username**:

    1. Select the three dots at the end of the row of the user you want to resolve and select **Deanonymize user**.

        ![Screenshot of the user table with the Deanonymize user option selected.](media/anonymize-user-table.png)
    2. In the pop-up, enter the justification for resolving the username and then select **Resolve**. In the relevant row, the resolved username is displayed.

        Note

        Resolving a username is audited.

        ![Screenshot of the Resolve dialog where a business justification is entered before selecting Resolve.](media/anonymize-resolve-dialog.png)

    You can also use the Anonymization settings page to resolve a single username or look up the encrypted username of a known username.

    1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
    2. Under **Cloud Discovery**, select **Anonymization**. Then, under **Anonymize and resolve usernames** enter a justification for why you're doing the resolution.
    3. Under **Enter username to resolve**, select **From anonymized** and enter the anonymized username, or select **To anonymized** and enter the original username to resolve. Select **Resolve**.

        ![Screenshot of the Resolve anonymization dialog for entering a username and confirming a deanonymization request.](media/anonymizer.png)

    **To resolve multiple usernames**:

    1. Either select the checkboxes that appear when you hover over the user icons by the users you want to resolve or, in the top-left, corner select the **Bulk selection** checkbox.

        ![Screenshot of the bulk selection checkboxes for resolving multiple anonymized users.](media/anonymize-bulk-resolve.png)
    2. Select **Deanonymize user**.
    3. In the pop-up, enter the justification for resolving the username and then select **Resolve**. In the relevant rows, the resolved usernames are displayed.

        Note

        Bulk username resolution is audited.

        ![Screenshot of the resolve dialog prompting for justification before deanonymizing multiple users.](media/anonymize-resolve-dialog.png)
6. Each username resolution action is audited in the portal's **Audit log**.

Note

Starting October, 2025 - **Resolve Anonymization** actions are no longer part of **Governance logs**. Instead, they will be audited in the **Activity log** only.