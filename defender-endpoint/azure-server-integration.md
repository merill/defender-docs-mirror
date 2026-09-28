---
layout: Conceptual
title: Integration with Microsoft Defender for Cloud - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/azure-server-integration
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about Microsoft Defender for Endpoint integration with Microsoft Defender for Cloud
ms.service: defender-endpoint
ms.subservice: onboard
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: concept-article
ms.date: 2025-03-27T00:00:00.0000000Z
locale: en-us
document_id: 49663056-840a-8b6b-ab4e-826adba83c08
document_version_independent_id: 49663056-840a-8b6b-ab4e-826adba83c08
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/azure-server-integration.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: azure-server-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/azure-server-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 817db59c-37d9-fa07-ed5d-ac8bd80554bc
---

# Integration with Microsoft Defender for Cloud - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint can integrate with Microsoft Defender for Cloud to provide a comprehensive Windows server protection solution. With this integration, Microsoft Defender for Cloud can use the power of Defender for Endpoint to provide improved threat detection for Windows Servers.

The following capabilities are included in this integration:

- Automated onboarding - Defender for Endpoint sensor is automatically enabled on Windows Servers that are onboarded to Microsoft Defender for Cloud. For more information on Microsoft Defender for Cloud onboarding, see [Use the integrated Microsoft Defender for Endpoint license](/en-us/azure/security-center/security-center-wdatp).

    Note

    The integration between Microsoft Defender for servers and Microsoft Defender for Endpoint has been expanded to support [Windows Server 2019 and Azure Virtual Desktop (AVD)](/en-us/azure/security-center/release-notes#microsoft-defender-for-endpoint-integration-with-azure-defender-now-supports-windows-server-2019-and-windows-10-virtual-desktop-wvd-in-preview).
- Windows servers monitored by Microsoft Defender for Cloud will also be available in Defender for Endpoint - Microsoft Defender for Cloud seamlessly connects to the Defender for Endpoint tenant, providing a single view across clients and servers. In addition, Defender for Endpoint alerts will be available in the Microsoft Defender for Cloud console.
- Server investigation - Microsoft Defender for Cloud customers can access the Microsoft Defender portal to perform detailed investigation to uncover the scope of a potential breach.

Important

- When you use Microsoft Defender for Cloud to monitor servers, a Defender for Endpoint tenant is automatically created (in the US for US users, in the EU for European and UK users). Data collected by Defender for Endpoint is stored in the geo-location of the tenant as identified during provisioning.
- If you use Defender for Endpoint before using Microsoft Defender for Cloud, your data will be stored in the location you specified when you created your tenant even if you integrate with Microsoft Defender for Cloud at a later time.
- Once configured, you cannot change the location where your data is stored. If you need to move your data to another location, you need to contact Microsoft Support to reset the tenant. Server endpoint monitoring utilizing this integration has been disabled for Office 365 GCC customers.