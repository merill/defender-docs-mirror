---
layout: Conceptual
title: Secure OAuth apps accessing non-Graph APIs using app governance - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-secure-apps-access-non-graph-api
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
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
description: Learn how to secure apps accessing other APIs using app governance in the Microsoft Defender portal.
ms.reviewer: shragar
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: bb9908e2-6cbf-f547-8cb5-2383db22ec44
document_version_independent_id: bb9908e2-6cbf-f547-8cb5-2383db22ec44
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-secure-apps-access-non-graph-api.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-secure-apps-access-non-graph-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-secure-apps-access-non-graph-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 68392880-d57d-95de-95ff-7e545cc5dc7d
---

# Secure OAuth apps accessing non-Graph APIs using app governance - Microsoft Defender for Cloud Apps | Microsoft Learn

## Overview

Many apps use APIs other than Microsoft Graph to access Microsoft 365 and other resources. With visibility over such apps, you can identify and defend against risks inherent to these apps, including the APIs that the apps access. Some non-Microsoft Graph APIs might receive limited support and updates.

App governance provides visibility over OAuth apps registered on Microsoft Entra ID, regardless of whether they access Graph API or other APIs. Additionally, you can monitor these apps and automatically take action if the apps are noncompliant or exhibit suspicious behavior.

You can better protect your organization with the new functionalities and enhancements in the following ways:

- Get improved coverage of OAuth apps with powerful app governance insights and monitoring capabilities.
- Automatically get alerted for any threats or anomalies from apps using non-Graph or legacy APIs.
- Get an enhanced experience for investigation of apps with more filters, columns, and properties.

## Identify apps that use non-Graph APIs

To view Microsoft 365 apps that access non-Graph APIs:

1. Go to **Settings** &gt; **Cloud apps** &gt; **[Apps governance](https://security.microsoft.com/cloudapps/app-governance?viewid=allApps)** in the [Microsoft Defender portal](https://security.microsoft.com).
2. Select the **Microsoft 365** tab
3. Open the **API access** filter
4. Select one of the options:
    - Office 365 Exchange Online
    - Office 365 SharePoint Online
    - Windows Azure Active Directory
    - Other APIs
5. Select **Apply**.

[![Screenshot that shows the list of APIs plus the option to view other APIs.](media/app-governance-secure-apps-access-non-graph-api/other-apis-app-governance.png)](media/app-governance-secure-apps-access-non-graph-api/other-apis-app-governance.png#lightbox)

## View APIs used by an app

The **Permissions** tab in the app details pane lists all permissions granted to an app, including both Graph API and non-Graph API permissions. To view the APIs that an app uses:

1. In the App governance page, select the app you want to investigate.
2. In the app details pane, select the **Permissions** tab.

[![Screenshot that shows the list of APIs and their assigned permissions.](media/app-governance-secure-apps-access-non-graph-api/other-apis-permissions.png)](media/app-governance-secure-apps-access-non-graph-api/other-apis-permissions.png#lightbox)

## Create policies for apps accessing non-graph APIs

You can create app governance policies to monitor and take action on apps that access non-Graph APIs. To create a custom policy or use an existing template, follow these steps:

1. In the App governance page, select the **Policies** tab.
2. Select **+ Create policy**.
3. To create a custom policy, select **Custom policy** and then configure the policy settings as needed. Select the **Non-Graph API permissions** policy condition to identify and monitor apps that access non-Graph APIs.

    ![Screenshot that shows the option to create a custom policy.](media/app-governance-secure-apps-access-non-graph-api/choose-policy-template.png)
4. To use a template, select **usage** and then the template **New app with Non-Graph API permissions**.

    ![Screenshot that shows the option to use a template for a new policy.](media/app-governance-secure-apps-access-non-graph-api/new-policy-non-graph-api.png)
5. Configure the policy settings as follows:

    - Give the policy a name and description
    - Set the severity level to low, medium, or high.
    - Set policy scope and conditions, you can choose to apply the default settings or customize the policy.
    - Choose an action you'd like to take on apps that match the conditions in this policy. For example, disabling the app.
    - Set the policy actions to active or disabled.