---
layout: Conceptual
title: Security Operations Guide for Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mde-sec-ops-guide
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: joshbregman, mattcall, pahuijbr, hayhov
description: A prescriptive playbook for SecOps personnel to manage Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2025-03-26T00:00:00.0000000Z
ms.topic: concept-article
author: limwainstein
ms.author: lwainstein
ms.custom:
- nextgen
- admindeeplinkDEFENDER
- mde-ngp
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
locale: en-us
document_id: 4f1d416a-e9bd-3b02-1c0d-afaf76263a33
document_version_independent_id: 4f1d416a-e9bd-3b02-1c0d-afaf76263a33
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mde-sec-ops-guide.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-sec-ops-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mde-sec-ops-guide.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a3ff913a-46ae-1ad0-f77c-4d4914bc0925
---

# Security Operations Guide for Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

This article gives an overview of the requirements and tasks for successfully operating Microsoft Defender for Endpoint in your organization. These tasks help your security operations center (SOC) effectively detect and respond to Microsoft Defender for Endpoint detected security threats.

This article also describes daily, weekly, monthly, and ad-hoc tasks your security team can perform for your organization.

Note

These are recommended steps; check them against your own policies and environment to make sure they are fit for purpose.

## Prerequisites

The Microsoft Defender Endpoint should be set up to support your regular security operations process. Although not covered in this document, the following articles provide configuration and setup information:

- [**Configure general Defender for Endpoint settings**](preferences-setup)

    - General
    - Permissions
    - Rules
    - Device management
    - Configure Microsoft Defender Security Center time zone settings
- **Set up Microsoft Defender XDR incident notifications**

    To get email notifications on defined Microsoft Defender XDR incidents, we recommend that you configure email notifications. For more information, see [Incident notifications by email](/en-us/defender-xdr/incidents-overview#incident-notifications-by-email).
- **Connect to SIEM (Sentinel)**

    If you have existing security information and event management (SIEM) tools, you can integrate them with Microsoft Defender XDR. For more information, see [Integrate your SIEM tools with Microsoft Defender XDR](/en-us/defender-xdr/configure-siem-defender) and [Microsoft Defender XDR integration with Microsoft Sentinel](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration).
- **Review data discovery configuration**

    Review the Microsoft Defender for Endpoint device discovery configuration to ensure it's configured as required. For more information, see [Device discovery overview](device-discovery).

## Daily activities

### General

- **Review actions**

    In the action center, review the actions that have been taken in your environment, both automated and manual. This information helps you validate that automated investigation and response (AIR) is performing as expected and identify any manual actions that need to be reviewed. For more information, see [Visit the Action center to see remediation actions](auto-investigation-action-center).

### Security operations team

- **Monitor the Microsoft Defender XDR Incidents queue**

    When Microsoft Defender for Endpoint identifies Indicators of compromise (IOCs) or Indicators of attack (IOAs) and generates an alert, the alert is included in an incident and displayed in the **Incidents** queue in the Microsoft Defender portal (https://security.microsoft.com).

    Review these incidents to respond to any Microsoft Defender for Endpoint alerts and resolve once the incident has been remediated. For more information, see [Incident notifications by email](/en-us/defender-xdr/incidents-overview#incident-notifications-by-email) and [View and organize the Microsoft Defender for Endpoint Incidents queue](view-incidents-queue).
- **Manage false positive and false negative detections**

    Review the incident queue, identify false positive and false negative detections and submit them for review. This helps you effectively manage alerts in your environment and make your alerts more efficient. For more information, see [Address false positives/negatives in Microsoft Defender for Endpoint](defender-endpoint-false-positives-negatives).
- **Review threat analytics high-impact threats**

    Review threat analytics to identify any campaigns that are impacting your environment. The "High-impact threats" table lists the threats that have had the highest impact to the organization. This section ranks threats by the number of devices that have active alerts. For more information, see [Track and respond to emerging threats through threat analytics](threat-analytics#view-the-threat-analytics-dashboard).

### Security administration team

- **Review health reports**

    Review health reports to identify any device health trends that need to be addressed. The device health reports cover Microsoft Defender for Endpoint AV signature, platform health, and EDR health. For more information, see [Device health reports in Microsoft Defender for Endpoint](device-health-reports).
- **Check Endpoint detection and response (EDR) sensor health**

    EDR health is maintaining the connection to the EDR service to make sure that Defender for Endpoint is receiving the required signals to alert and identify vulnerabilities.

    Review unhealthy devices. For more information, see [Device health, Sensor health & OS report](device-health-sensor-health-os).
- **Check Microsoft Defender Antivirus health**

    Viewing the status of Microsoft Defender Antivirus updates is critical for the best performance of Defender for Endpoint in your environment and up-to-date detections. The device health page shows current status for platform, intelligence, and engine version. For more information, see the [Device health, Microsoft Defender Antivirus health report](device-health-microsoft-defender-antivirus-health).

## Weekly activities

### General

- **Message Center**

    Microsoft Defender uses the Microsoft 365 Message center to notify you of upcoming changes, such as new and changed features, planned maintenance, or other important announcements.

    Review the Message center messages to understand any upcoming changes that impact your environment.

    You can access this in the Microsoft 365 admin center under the Health tab. For more information, see [How to check Microsoft 365 service health](/en-us/Microsoft-365//enterprise/view-service-health).

### Security operations team

- **Review threat reporting**

    Review health reports to identify any device threat trends that need to be addressed. For more information, see [Threat protection report](threat-protection-reports).
- **Review threat analytics**

    Review threat analytics to identify any campaigns that affect your environment. For more information, see [Track and respond to emerging threats through threat analytics](threat-analytics).

### Security administration team

- **Review threat and vulnerability (TVM) status**

    Review TVM to identify any new vulnerabilities and recommendations that require action. For more information, see [Vulnerability management dashboard.](/en-us/defender-vulnerability-management/tvm-dashboard-insights)
- **Review attack surface reduction reporting**

    Review ASR reports to identify any files that affect your environment. For more information, see [Attack surface reduction (ASR) rules report](attack-surface-reduction-rules-report).
- **Review web protection events**

    Review the web defense report to identify any IP addresses or URLs that are blocked. For more information, see [Web protection](web-protection-overview).

## Monthly activities

### General

Review the following articles to understand recently released updates:

- [What's new in Microsoft Defender for Endpoint](whats-new-in-microsoft-defender-endpoint)
- [Microsoft Defender for Endpoint versions](microsoft-defender-endpoint-releases)

### Security administration team

- **Review device excluded from policy**

    If any devices are excluded from Defender for Endpoint policies, review and determine whether the device still needs to be excluded from the policy.

    Note

    Review troubleshooting mode for troubleshooting. For more information, see [Enable and use troubleshooting mode in Microsoft Defender for Endpoint](troubleshooting-mode-enable).

## Periodically

These tasks are seen as maintenance for your security posture and are critical for your ongoing protection. But as they may take time and effort, it's recommended that you set a standard schedule that you can maintain to perform these tasks.

- **Review exclusions**

    Review exclusions that have been set in your environment to confirm you haven't created a protection gap by excluding things that are no longer required to be excluded.
- **Review Defender policy configurations**

    Periodically review your Defender configuration settings to confirm that they're set as required.
- **Review automation levels**

    Review automation levels in automated investigation and remediation capabilities. For more information, see [Automation levels in automated investigation and remediation](automation-levels).
- **Review custom detections**

    Periodically review whether the custom detections that have been created are still valid and effective. For more information, see [Review custom detection](/en-us/defender-xdr/custom-detection-rules).
- **Review alerts suppression**

    Periodically review any alert suppression rules that have been created to confirm they're still required and valid. For more information, see [Review alerts suppression](/en-us/defender-xdr/investigate-alerts?toc=/defender-endpoint/toc.json&amp;bc=/defender-endpoint/breadcrumb/toc.json#built-in-alert-tuning-rules).

## Troubleshooting

The following articles provide guidance to troubleshoot and fix errors that you may experience when setting up your Microsoft Defender for Endpoint service.

- [Troubleshoot Sensor state](check-sensor-status)
- [Troubleshoot sensor health issues using Client Analyzer](fix-unhealthy-sensors)
- [Troubleshoot live response issues](troubleshoot-live-response)
- [Collect support logs using LiveAnalyzer](troubleshoot-collect-support-log)
- [Troubleshoot attack surface reduction issues](troubleshoot-asr)
- [Troubleshoot onboarding issues](troubleshoot-onboarding)