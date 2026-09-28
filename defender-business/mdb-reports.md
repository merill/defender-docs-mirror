---
layout: Conceptual
title: Reports in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-reports
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get an overview of security reports in Defender for Business. Reports show detected threats, alerts, vulnerabilities, and device status.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2025-09-11T00:00:00.0000000Z
ms.reviewer: efratka, nehabha
ms.collection:
- SMB
- m365-security
- tier1
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2ffaf0a4-04e8-19ef-d726-2d75f61631db
document_version_independent_id: 2ffaf0a4-04e8-19ef-d726-2d75f61631db
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-reports.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-reports.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: cc27df32-d53e-0bfd-2af0-d741032d322e
---

# Reports in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

Several reports are available in the Microsoft Defender portal (https://security.microsoft.com). These reports enable your security team to view information about detected threats, device status, and more.

This article describes these reports, how you can use them, and how to find them.

## Monthly security summary (preview)

[![Screenshot of monthly security summary report currently in preview.](media/mdb-monthly-security-summary-report.png)](media/mdb-monthly-security-summary-report.png#lightbox)

The monthly security summary report (currently in preview) shows:

- Threats detected and prevented by Defender for Business, so you can see how the service is working for you.
- Your current status from [Microsoft Secure Score](/en-us/defender-xdr/microsoft-secure-score), which gives you an indication of your organization's security posture.
- Recommended actions you can take to improve your score and your security posture.

To access this report, in the navigation pane, choose **Reports** &gt; **Endpoints** &gt; **Monthly Security Summary**.

## License report

[![Screenshot of licenses report in Defender for Business.](media/mdb-licenses.png)](media/mdb-licenses.png#lightbox)

The license report provides information about licenses bought and used by your organization.

To access this report, in the navigation pane, choose **Settings** &gt; **Endpoints** &gt; **Licenses**.

## Security report

[![Screenshot of the security report in Defender for Business.](media/mdb-security-report.png)](media/mdb-security-report.png#lightbox)

The security report provides information about your company's identities, devices, and apps.

To access this report, in the navigation pane, choose **Reports** &gt; **General** &gt; **Security report**.

Tip

You can view similar information on the home page of your Microsoft Defender portal (https://security.microsoft.com).

## Threat protection report

[![Screenshot of the threat protection report in Defender for Business.](media/mdb-threat-protection-report.png)](media/mdb-threat-protection-report.png#lightbox)

The threat protection report provides information about alerts and alert trends.

- Use the **Alert trends** column to view information about alerts that were triggered over the last 30 days.
- Use the **Alert status** column to view current snapshot information about alerts, such as categories of unresolved alerts and their classification.

To access this report, in the navigation pane, choose **Reports** &gt; **Endpoints** &gt; **Threat protection**.

## Incidents view

[![Screenshot of the incidents view in Defender for Business.](media/mdb-incidents.png)](media/mdb-incidents.png#lightbox)

You can use the **Incidents** list to view information about alerts. To learn more, see [View and manage incidents in Defender for Business](mdb-view-manage-incidents).

To access this report, in the navigation pane, choose **Incidents** to view and manage current incidents.

## Device health report

[![Screenshot of the device health report in Defender for Business.](media/mdb-device-health.png)](media/mdb-device-health.png#lightbox)

The device health report provides information about device health and trends. You can use this report to determine whether Defender for Business sensors are working correctly on devices and the current status of Microsoft Defender Antivirus.

To access this report, in the navigation pane, choose **Reports** &gt; **Endpoints** &gt; **Device health**.

## Device inventory list

[![Screenshot of the device inventory report in Defender for Business.](media/mdb-device-inventory.png)](media/mdb-device-inventory.png#lightbox)

You can use the **Devices** list to view information about your company's devices. To learn more, see [Manage devices in Defender for Business](mdb-manage-devices).

To access this report, in the navigation pane, go to **Assets** &gt; **Devices**.

## Vulnerable devices report

[![Screenshot of the vulnerable devices report in Defender for Business.](media/mdb-vulnerable-devices.png)](media/mdb-vulnerable-devices.png#lightbox)

The vulnerable devices report provides information about devices and trends.

- Use the **Trends** column to view information about devices that had alerts over the last 30 days.
- Use the **Status** column to view current snapshot information about devices that have alerts.

To access this report, in the navigation pane, choose **Reports** &gt; **Endpoints** &gt; **Vulnerable devices**.

## Web protection report

[![Screenshot of the web protection report in Defender for Business.](media/mdb-web-protection-report.png)](media/mdb-web-protection-report.png#lightbox)

The web protection report shows attempts to access phishing sites, malware vectors, exploit sites, untrusted or low-reputation sites, and sites that are explicitly blocked. Categories of blocked sites include adult content, leisure sites, legal liability sites, and more.

To access this report, in the navigation pane, choose **Reports** &gt; **Endpoints** &gt; **Web protection**.

Note

If you didn't configure web protection for your company, choose the **Settings** button in a report view. Then, under **Rules**, choose **Web content filtering**. To learn more about web content filtering, see [Web content filtering](/en-us/defender-endpoint/web-content-filtering).

## Firewall report

[![Screenshot of the firewall report in Defender for Business.](media/mdb-firewall-report.png)](media/mdb-firewall-report.png#lightbox)

When firewall protection is configured, the firewall report shows blocked inbound, outbound, and app connections. This report also shows remote IPs connected by multiple devices, and remote IPs with the most connection attempts.

To access this report, in the navigation pane, choose **Reports** &gt; **Endpoints** &gt; **Firewall**.

Note

If your firewall report has no data, it might be because you didn't configure firewall protection yet. In the navigation pane, choose **Endpoints** &gt; **Configuration management** &gt; **Device configuration**. To learn more, see [Firewall in Defender for Business](mdb-firewall).

## Device control report

[![Screenshot of the device control report in Defender for Business.](media/mdb-device-control.png)](media/mdb-device-control.png#lightbox)

The device control report shows information about media usage, such as the use of removable storage devices in your organization.

To access this report, in the navigation pane, choose **Reports** &gt; **Endpoints** &gt; **Device control**.

## Attack surface reduction rules report

[![Screenshot of the attack surface reduction rules report in Defender for Business.](media/mdb-asr-report.png)](media/mdb-asr-report.png#lightbox)

The attack surface reduction rules report has three tabs:

- **Detections**: Show blocked or audited detections.
- **Configuration**: Filter on standard protection rules or other attack surface reduction rules.
- **Add exclusions**: Define exclusions, if needed.

To learn more, see [Attack surface reduction (ASR) rules report in the Microsoft Defender portal](/en-us/defender-endpoint/attack-surface-reduction-rules-report).

To access this report, in the navigation pane, choose **Reports** &gt; **Endpoints** &gt; **Attack surface reduction rules**.