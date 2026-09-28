---
layout: Conceptual
title: Manage reports - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/reports
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
description: Learn how to download and schedule Microsoft Defender for Identity reports from Microsoft Defender XDR.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: LiorShapiraa
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 38b40e6c-d2e8-a591-96e1-e790ca05f8b0
document_version_independent_id: 38b40e6c-d2e8-a591-96e1-e790ca05f8b0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/reports.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/reports.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 3f6e708c-1ab7-2198-71cf-617bc8e40f27
---

# Manage reports - Microsoft Defender for Identity | Microsoft Learn

## Overview

Microsoft Defender XDR provides Defender for Identity reports, which you can either generate on demand or configure to be sent periodically by email. This article explains how to access, download, and schedule Defender for Identity reports in Microsoft Defender XDR. Available reports cover system activity summaries, modifications to sensitive groups, and passwords exposed in cleartext, helping you monitor identity-related risks in your environment.

## Access Defender for Identity reports in Microsoft Defender XDR

To access Defender for Identity reports in Microsoft Defender, from the navigation menu on the left, select **Reports** &gt; **Identities** &gt; **Report management**.

Available reports include:

| Report name | Description |
| --- | --- |
| **Summary** | Presents a dashboard of your system status, including: - **Summary**: A summary of detected network activity - **Open health issues**: Lists Defender for Identity health issues you should take care of.  Suspicious activities and health issues are listed by type. |
| **Modification to sensitive groups** | Lists every time a modification is made to sensitive groups, such as admins, or manually tagged accounts or groups. If you're using Defender for Identity standalone sensors, make sure that [events are forwarded from your domain controllers to the standalone sensors](deploy/configure-event-forwarding) in order to receive a full report about your sensitive groups. |
| **Passwords exposed in cleartext** | Lists all source computer and account passwords detected by Defender for Identity being sent in clear text. **Note**: Some services use the LDAP non-secure protocol to send account credentials in plain text. This can even happen for sensitive accounts. Attackers monitoring network traffic can catch and then reuse these credentials for malicious purposes. |

## Generate a report on demand

To generate a report on demand:

1. In Microsoft Defender XDR, select **Reports** &gt; **Identities** &gt; **Report management**.
2. On the **Identities reports** page, select a report and then select **Download**.
3. In the download report pane that appears on the right, define a time period for your report and then select **Download Report**.

Your report is downloaded by your browser, where you can open or save it. Downloaded reports include a maximum of 100,000 rows.

## Schedule a report by email

To define a schedule for a report to be sent to you by email:

1. In Microsoft Defender XDR, select **Reports** &gt; **Identities** &gt; **Report management**.
2. On the **Identities reports** page, select a report and then select **Schedule report**.
3. Use the wizard to define the following details:

    1. On the **Set schedule** page, define the conditions in which you want to send the report, and the time you want it sent.

        Your report is sent according to your Microsoft Defender time zone settings (*Local* or UTC). For more information, see [Set the time zone for Microsoft Defender](/en-us/microsoft-365/security/defender/m365d-time-zone).
    2. On the **Recipients** page, enter and add email addresses for anyone you want to receive the report. Select **Next** to complete the scheduling.
    3. The **Finish** page shows a confirmation message. Select **Close** to close the wizard.

Once the scheduling is configured, to edit the scheduled time or recipients, repeat the steps in To define a schedule for a report to be sent to you by email.

### Remove all scheduled reports

To remove a scheduled report and stop it from being sent:

Warning

Resetting the schedule stops future email delivery for this report until you configure a new schedule.

1. In Microsoft Defender XDR, select **Reports** &gt; **Identities** &gt; **Reports management**.
2. On the **Identities reports** page, select the report you want to stop sending and then select **Reset schedule**.
3. In the confirmation message, select **Reset** to complete the process.