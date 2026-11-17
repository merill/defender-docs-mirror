---
layout: Conceptual
title: Configure integration profiles for generated playbooks - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/siem-defender-configure-integration-profiles
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to configure integration profiles for generated playbooks in the Microsoft Defender portal.
ms.service: microsoft-defender
ms.subservice: unified-security-operations
author: guywi-ms
ms.author: guywild
ms.date: 2026-07-15T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: 29766b93-0d8a-8519-e93d-8a8a882bc590
document_version_independent_id: 29766b93-0d8a-8519-e93d-8a8a882bc590
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/siem-defender-configure-integration-profiles.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: siem-defender-configure-integration-profiles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/siem-defender-configure-integration-profiles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 4100e613-6e07-39d7-2bd5-14e53e789602
---

# Configure integration profiles for generated playbooks - Microsoft Defender XDR | Microsoft Learn

Integration profiles define the API connection details used by generated playbooks. Configure integration profiles before you create or run generated playbooks that call Microsoft or third-party services.

Each integration profile includes connection details such as the base API URL, authentication method, and required credentials.

## Prerequisites

Before you begin, make sure that:

- You have access to the [Microsoft Defender portal](https://security.microsoft.com/).
- You have the **Automation Integration** Unified RBAC permission with **Read** and **Write** access.
- You have the credentials required for the target API.
- To run automation on third-party data ingested through Log Analytics, you have a [Microsoft Sentinel workspace](/en-us/azure/sentinel/quickstart-onboard).

## Create an integration profile

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation**.
3. Select the **Integration Profiles** tab.
4. Select **Create**.
5. Enter an integration name.
6. Enter a description.
7. Enter the base API URL for the service.
8. Select the authentication method.

    Supported authentication methods include:

    - OAuth2 Client Credentials
    - API Key
    - AWS Auth
    - User and Password
    - Bearer/JWT Authentication
    - Hawk
9. Enter the required authentication details.
10. Review the integration profile settings.
11. Select **Create**.

## Create a Microsoft Graph integration profile

Use a Microsoft Graph integration profile when a generated playbook needs to call Microsoft Graph APIs.

1. In the Azure portal, go to **Microsoft Entra ID** &gt; **App registrations**.
2. Select **New registration**.
3. Enter a name for the application.
4. Complete the app registration.
5. Copy the **Application (client) ID** and **Directory (tenant) ID**.
6. Go to **Certificates & secrets**.
7. Select **New client secret**.
8. Copy the client secret value and store it securely.

    Important

    You can't retrieve the client secret value after leaving the page.
9. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
10. Go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation**.
11. Select the **Integration Profiles** tab.
12. Select **Create**.
13. Configure the profile with the following values:

    | Field | Value |
    | --- | --- |
    | Integration name | Enter a descriptive name, such as `Graph Integration`. |
    | Description | Enter a short description. |
    | Base API URL | `https://graph.microsoft.com` |
    | Authentication method | OAuth2 |
    | Client ID | Enter the Application client ID. |
    | Client secret | Enter the client secret value. |
    | Token endpoint | `https://login.microsoftonline.com/{TENANT_ID}/oauth2/v2.0/token` |
    | Scopes | `https://graph.microsoft.com/.default` |
14. Replace `{TENANT_ID}` with the Directory tenant ID.
15. Select **Create**.

## Edit an integration profile

You can edit the integration name and description after the profile is created.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation**.
3. Select the **Integration Profiles** tab.
4. Select the integration profile.
5. Update the name or description.
6. Save your changes.

Note

The API URL and authentication method can't be changed after an integration profile is created. To change the API URL or authentication method, create a new integration profile.

## Limitations

Integration profiles have the following limitations:

- Microsoft Graph and Azure Resource Manager integrations aren't enabled by default and must be manually created.
- The API URL and authentication method can't be changed after an integration profile is created.
- The maximum number of integrations per tenant is 500.