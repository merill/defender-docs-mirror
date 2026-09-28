---
layout: Conceptual
title: Microsoft Defender for Identity Notifications - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/notifications
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
description: Learn how to use and configure Microsoft Defender for Identity notifications in Microsoft Defender XDR.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: LiorShapiraa
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a34dccc9-902f-86f4-aae0-840629fec263
document_version_independent_id: a34dccc9-902f-86f4-aae0-840629fec263
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/notifications.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/notifications.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: dfc86433-254d-986c-ee17-619723770934
---

# Microsoft Defender for Identity Notifications - Microsoft Defender for Identity | Microsoft Learn

Note

Defender for Identity notifications are currently supported only by the Defender for Identity sensor version 2.x.

Microsoft Defender for Identity provides notifications for health issues and security alerts, either via email notifications or to a Syslog server.

This article describes how to configure Defender for Identity notifications so that you're aware of any health issues or security alerts detected.

Tip

In addition to email or Syslog notifications, we recommend that SOC admins use Microsoft Sentinel to view all alerts in a single portal. For more information, see [Microsoft Defender XDR integration with Microsoft Sentinel](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration). To integrate other SIEM tools, see [Integrate your SIEM tools with Microsoft Defender XDR](/en-us/microsoft-365/security/defender/configure-siem-defender).

## Configure email notifications

Use the following procedure to configure email notifications for Defender for Identity health issues.

1. In [Microsoft Defender](https://security.microsoft.com), select **Settings** &gt; **Identities**.
2. Under **Notifications**, select **Health issues notifications**.
3. In the **Add recipient email**, enter the email address(es) where you want to receive email notifications, and select **+ Add**.

Whenever Defender for Identity detects a health issue, configured recipients receive an email notification with the details, with a link to Microsoft Defender XDR for more details.

Note

To receive email notifications about Incidents, please use the [Email Notifications](https://security.microsoft.com/securitysettings/defender/email_notifications) page under Defender XDR Settings for new and existing notifications rules. [Learn more about incident email notifications in Defender XDR](https://aka.ms/IncidentsNotificationsDefenderXdr).

## Configure Syslog notifications

You can configure Defender for Identity to send health issues and security events to a Syslog server through a configured sensor.

Events aren't sent from the Defender for Identity service to your Syslog server directly, but only through the sensor.

Tip

If you use Syslog in TLS mode, install the required certificates on the designated sensor before completing this procedure.

**To configure Syslog notifications**:

1. In [Microsoft Defender XDR](https://security.microsoft.com), select **Settings** &gt; **Identities**.
2. Under **Notifications**, select **Syslog notifications**, then toggle on the **Syslog service** option.
3. Select **Configure service** to open the **Syslog service** pane.
4. Enter the following details:

    - **Sensor**: Select the sensor you want to send notifications to the Syslog server.
    - **Service endpoint** and **Port**: Enter the IP address or fully qualified domain name (FQDN) for the Syslog server, and then enter the port number. You can configure only one Syslog endpoint.
    - **Transport**: Select the **Transport** protocol (TCP or UDP).
    - **Format**: Select the format (RFC 3164 or RFC 5424).
5. Select **Send test SIEM notification** and verify the message is received in your Syslog infrastructure solution.
6. When you've confirmed that the test works, select **Save**.
7. After configuring the Syslog service, select the types of notifications to send to your Syslog server, including whenever:

    - A new security alert is detected
    - An existing security alert is updated
    - A new health issue is detected

## Creating automation scripts for Defender for Identity SIEM logs

When you create automation scripts for Defender for Identity SIEM logs, use the **externalId** field to identify the alert type. Alert names might change over time, but the **externalId** for each alert stays the same. For more information, see [Defender for Identity SIEM log reference](cef-format-sa).