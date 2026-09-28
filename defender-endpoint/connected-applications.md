---
layout: Conceptual
title: Connected applications in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/connected-applications
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: View connected partner applications that use standard OAuth 2.0 protocol to authenticate and provide tokens for use with Microsoft Defender for Endpoint APIs.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: concept-article
ms.subservice: onboard
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: a2c91dd2-7c05-6a61-f40e-986edbe51564
document_version_independent_id: a2c91dd2-7c05-6a61-f40e-986edbe51564
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/connected-applications.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: connected-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/connected-applications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: e22dafe5-c374-ee3d-003b-09f1ee2abb91
---

# Connected applications in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Connected applications integrates with the Defender for Endpoint platform using APIs.

Applications use standard OAuth 2.0 protocol to authenticate and provide tokens for use with Microsoft Defender for Endpoint APIs. In addition, Microsoft Entra applications allow tenant admins to set explicit control over which APIs can be accessed using the corresponding app.

You'll need to follow [these steps](api/apis-intro) to use the APIs with the connected application.

From the left navigation menu, select **Partners & APIs** (under **Endpoints**) &gt; **Connected applications**.

## View connected application details

The Connected applications page provides information about the Microsoft Entra applications connected to Microsoft Defender for Endpoint in your organization. You can review the usage of the connected applications: last seen, number of requests in the past 24 hours, and request trends in the last 30 days.

[![The connected applications](media/connected-apps.png)](media/connected-apps.png#lightbox)

## Edit, reconfigure, or delete a connected application

The **Open application settings** link opens the corresponding Microsoft Entra application management page in the Azure portal. From the Azure portal, you can manage permissions, reconfigure, or delete the connected applications.