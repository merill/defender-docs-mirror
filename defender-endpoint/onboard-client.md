---
layout: Conceptual
title: Onboard Windows client devices to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/onboard-client
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Find out how to onboard Windows client devices to Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.reviewer: pahuijbr
ms.collection:
- m365-security
- tier2
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2025-11-17T00:00:00.0000000Z
locale: en-us
document_id: eff3e7ed-6894-dc4d-4d4e-1fe94ee9749c
document_version_independent_id: eff3e7ed-6894-dc4d-4d4e-1fe94ee9749c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/onboard-client.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: onboard-client
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/onboard-client.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6b2459d9-1b58-a57b-50cf-fb4fd0d7f1f2
---

# Onboard Windows client devices to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

## Overview of onboarding client devices

Note

The Defender deployment tool can be used to deploy Defender endpoint security on Windows and Linux devices. The tool is a lightweight, self-updating application that streamlines the deployment process. For more information, see [Deploy Microsoft Defender endpoint security to Windows devices using the Defender deployment tool](/en-us/defender-endpoint/defender-deployment-tool-windows) and [Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview)](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).

To onboard Windows client devices, follow this general process:

1. Make sure to review the [Minimum requirements for Defender for Endpoint](minimum-requirements).
2. In the [Microsoft Defender portal](https://security.microsoft.com), go to **System** &gt; **Settings** &gt; **Endpoints**, and then, under **Device management**, select **Onboarding**.

    [![Screenshot showing device onboarding in the Microsoft Defender portal for Defender for Endpoint.](media/mde-device-onboarding-ui.png)](media/mde-device-onboarding-ui.png#lightbox)
3. Under **Select operating system to start onboarding process**, select the operating system for the device.
4. Under **Connectivity type**, select either **Streamlined** or **Standard**. (See [prerequisites for streamlined connectivity](configure-device-connectivity#prerequisites).)
5. Under **Deployment method**, select an option. Then download the onboarding package (and installation package, if there's one available). Follow the instructions to onboard your devices. The following table lists available deployment methods:

    | Operating system | Deployment method |
    | --- | --- |
    | Windows 11Windows 10 Windows 365 | [Local script (up to 10 devices)](configure-endpoints-script)[Microsoft Intune / Mobile Device Management](configure-endpoints-mdm)[Microsoft Configuration Manager](configure-endpoints-sccm)[Group Policy](configure-endpoints-gp)[VDI scripts](configure-endpoints-vdi) |
    | Windows 8.1 Enterprise or ProWindows 7 SP1 Enterprise or Pro | [Microsoft Monitoring Agent](update-agent-mma-windows) |

Warning

Repackaging the Defender for Endpoint installation package is not a supported scenario. Doing so can negatively impact the integrity of the product and lead to adverse results, including but not limited to triggering tampering alerts and updates failing to apply.