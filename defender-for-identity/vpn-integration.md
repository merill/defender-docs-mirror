---
layout: Conceptual
title: Integrate VPN with Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/vpn-integration
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to collect accounting information by integrating a VPN for Microsoft Defender for Identity in Microsoft Defender XDR.
ms.date: 2026-08-07T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: martin77s
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 4536e5aa-76a6-9efc-a32f-9f88bdad26d9
document_version_independent_id: 4536e5aa-76a6-9efc-a32f-9f88bdad26d9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/vpn-integration.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: vpn-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/vpn-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: b7d83603-923c-cfb8-d0ea-dd43c6d98339
---

# Integrate VPN with Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

Note

VPN integration is currently supported only by the Defender for Identity sensor version 2.x.

Microsoft Defender for Identity can integrate with your VPN solution by listening to RADIUS accounting events forwarded to Defender for Identity sensors, such as the IP addresses and locations where connections originated. VPN accounting data can help your investigations by providing more information about user activity, such as the locations from where computers are connecting to the network, and an extra detection for abnormal VPN connections.

Important

VPN integration isn't supported in environments adhering to Federal Information Processing Standards (FIPS).

Defender for Identity's VPN integration is based on standard RADIUS Accounting ([RFC 2866](https://tools.ietf.org/html/rfc2866)), and supports the following VPN vendors:

- Microsoft
- F5
- Check Point
- Cisco ASA

Defender for Identity's VPN integration supports both primary UPNs and alternate user principal names. Calls to resolve external IP addresses to a location are anonymous and no personal identifier is sent in the call.

## Prerequisites

Before you start, make sure that you have:

- [Microsoft Defender for Identity deployed](deploy-defender-identity)
- At least one connected and healthy Defender for Identity sensor version 2.x to receive RADIUS accounting events.
- Access to the **Settings** area in Microsoft Defender. For more information, see [Microsoft Defender for Identity role groups](role-groups).
- The ability to configure RADIUS on your VPN system.

    The following procedure provides an example of how to configure Microsoft Defender for Identity to collect accounting information from VPN solutions, using Microsoft Routing and Remote Access Server (RRAS). If you're using a third-party VPN solution, consult their documentation for instructions on how to enable RADIUS Accounting.

Note

When you enable VPN integration in Defender for Identity settings, the Defender for Identity sensor enables a pre-provisioned Windows firewall policy called **Microsoft Defender for Identity Sensor**. This policy allows incoming RADIUS Accounting on port UDP 1813.

## Configure RADIUS accounting on your VPN system

This procedure describes how to configure RADIUS accounting on an RRAS server for integrating a VPN system with Defender for Identity. Your system's instructions may differ.

### On your RRAS server

1. Open the **Routing and Remote Access** console.
2. Right-click the server name and select **Properties**.
3. In the **Security** tab, under **Accounting provider**, select **RADIUS Accounting** &gt; **Configure**. For example:

    ![Screenshot of the Security tab showing RADIUS Accounting selected as the accounting provider.](media/radius-setup.png)
4. In the **Add RADIUS Server** dialog, enter the **Server name** of the closest Defender for Identity sensor with network connectivity. For high availability, you can add additional Defender for Identity sensors as RADIUS accounting servers in RRAS.
5. Under **Port**, make sure the default value of `1813` is configured.
6. Select **Change** and enter a new shared secret string of alphanumeric characters. Take note of the new shared secret string. You'll enter it in the **Shared Secret** field in the Defender for Identity VPN integration settings.
7. Check the **Send RADIUS Account On and Accounting Off messages** box and select **OK** on all open dialog boxes. For example:

    ![Screenshot of RRAS accounting settings showing the Send RADIUS Account On and Accounting Off messages option enabled.](media/vpn-set-accounting.png)

## Configure VPN in Defender for Identity

This procedure describes how to configure Defender for Identity's VPN integration in Microsoft Defender.

1. Sign into [Microsoft Defender](https://security.microsoft.com) and select **Settings** &gt; **Identities** &gt; **VPN**.
2. Select **Enable radius accounting** and enter the **Shared Secret** you'd previously configured on your RRAS VPN server. For example:

    ![Screenshot of VPN integration settings with Enable radius accounting selected and Shared Secret field populated.](media/vpn-integration.png)
3. Select **Save** to continue.

After you've saved your selection, your Defender for Identity sensors start listening on port 1813 for RADIUS accounting events, and your VPN setup is complete.

When the Defender for Identity sensor receives VPN events and sends them to the Defender for Identity cloud service for processing, the entity profile indicates distinct VPN locations that were accessed, and profile activities indicate locations.