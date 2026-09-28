---
layout: Conceptual
title: Troubleshoot SIEM tool integration issues in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-siem
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot issues that might arise when using SIEM tools with Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: troubleshooting
ms.date: 2025-02-24T00:00:00.0000000Z
locale: en-us
document_id: 104add36-86b3-22e6-3b89-c3536424c407
document_version_independent_id: 104add36-86b3-22e6-3b89-c3536424c407
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-siem.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-siem
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-siem.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 53226016-8256-3d6c-fbdb-9546a7a11629
---

# Troubleshoot SIEM tool integration issues in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

The new Microsoft Defender XDR alerts API, released to public preview in MS Graph, is the official and recommended API for customers migrating from the SIEM API. See [Migrate from the MDE SIEM API to the Microsoft Defender XDR alerts API](configure-siem).

You might need to troubleshoot issues while pulling detections in your SIEM tools.

This page provides detailed steps to troubleshoot issues you might encounter.

## Learn how to get a new client secret

If your client secret expires or if you've misplaced the copy provided when you were enabling the SIEM tool application, you'll need to get a new secret.

1. Log in to the [Azure management portal](https://portal.azure.com).
2. Select **Microsoft Entra ID**.
3. Select your tenant.
4. Click **App registrations**. Then in the applications list, select the application.
5. Select **Certificates & Secrets** section, Click on New Client Secret, then provide a description and specify the validity duration.
6. Click **Save**. The key value is displayed.
7. Copy the value and save it in a safe place.

## Error when getting a refresh access token

If you encounter an error when trying to get a refresh token when using the threat intelligence API or SIEM tools, you'll need to add reply URL for relevant application in Microsoft Entra ID.

1. Log in to the [Azure management portal](https://ms.portal.azure.com).
2. Select **Microsoft Entra ID**.
3. Select your tenant.
4. Click **App Registrations**. Then in the applications list, select the application.
5. Add the following URL:

    - For the European Union: `https://winatpmanagement-eu.securitycenter.windows.com/UserAuthenticationCallback`
    - For the United Kingdom: `https://winatpmanagement-uk.securitycenter.windows.com/UserAuthenticationCallback`
    - For the United States: `https://winatpmanagement-us.securitycenter.windows.com/UserAuthenticationCallback`.
6. Click **Save**.

## Error while enabling the SIEM connector application

If you encounter an error when trying to enable the SIEM connector application, check the pop-up blocker settings of your browser. It might be blocking the new window being opened when you enable the capability.