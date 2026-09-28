---
layout: Conceptual
title: Create snapshot cloud discovery reports - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/create-snapshot-cloud-discovery-reports
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides information about how to upload logs manually to create a snapshot report of your cloud discovery apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: cd1577ea-7b40-f30d-758d-96d85c8fccff
document_version_independent_id: cd1577ea-7b40-f30d-758d-96d85c8fccff
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/create-snapshot-cloud-discovery-reports.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: create-snapshot-cloud-discovery-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/create-snapshot-cloud-discovery-reports.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: f8a1ae4f-9999-b9fe-4045-660dc5b7ba63
---

# Create snapshot cloud discovery reports - Microsoft Defender for Cloud Apps | Microsoft Learn

## Create a Cloud Discovery snapshot report

It's important to upload a log manually and let Microsoft Defender for Cloud Apps parse it before trying to use the automatic log collector. For information on how the log collector works and the expected log format, including required traffic log attributes and conditions, see Using traffic logs for cloud discovery.

This article explains how to create a Cloud Discovery snapshot report in Microsoft Defender for Cloud Apps by manually uploading traffic logs from your firewall or proxy. Use a snapshot report to validate your log format and get initial visibility into cloud app usage before setting up the automatic log collector.

If you don't have a log yet and you want to see an example of what your log should look like, download a sample log file. Follow the snapshot report creation procedure to see what your log should look like.

To create a snapshot report:

1. Collect log files from your firewall and proxy, through which users in your organization access the Internet. Make sure to gather logs during times of peak traffic that are representative of all user activity in your organization.
2. In the Microsoft Defender Portal, under **Cloud Apps**, select **Cloud discovery**.
3. In the top-right corner, pull down **Actions**, and select **Create Cloud Discovery snapshot report.**

    ![Screenshot of the Create Cloud Discovery snapshot report option.](media/create-new-snapshot-report.png)
4. Select **Next**.
5. Enter a **Report name** and a **Description**

    ![Screenshot of the new snapshot report name and description fields.](media/new-snapshot-report.png)
6. Select the **Source** from which you want to upload the log files. If your source isn't supported (see [Supported firewalls and proxies](set-up-cloud-discovery#supported-firewalls-and-proxies-) for the full list), you can create a custom parser. For more information, see [Use a custom log parser](custom-log-parser).
7. Verify your log format to make sure that it's formatted properly according to the sample log you can download. Under **Verify your log format**, select **View log format** then select **Download sample log**. Compare your log with the sample provided to make sure it's compatible.

    ![Screenshot of the verify your log format section in cloud discovery.](media/cloud-discovery-snapshot-verify.png)

    Note

    The FTP sample format is supported in snapshots and automated upload while syslog is supported in automated upload only. Downloading a sample log downloads a sample FTP log.
8. **Upload traffic logs** that you want to upload. You can upload up to 20 files at once. Compressed and zipped files are also supported.

    ![Screenshot of the upload traffic logs section in cloud discovery.](media/upload-traffic-logs.png)
9. Select **Upload logs**.
10. After upload completes, the status message will appear at the top-right corner of your screen letting you know that your log was successfully uploaded.
11. After you upload your log files, it will take some time for them to be parsed and analyzed. After processing of your log files completes, you'll receive an email to notify you that it's done.
12. A notification banner will appear in the status bar at the top of the **Cloud Discovery** dashboard. The banner updates you with the processing status of your log files. ![Screenshot of the processing log file notification menu bar.](media/processing-log-file-menu-bar.png)
13. After the logs are uploaded successfully, you should see a notification letting you know that the log file processing completed successfully. At this point, you can view the report by selecting the link in the status bar. Or, in the Microsoft Defender Portal, select **Settings**.
14. Then under **Cloud Discovery**, select **Snapshot reports**, and select your snapshot report.

    ![Screenshot of the snapshot report management page in cloud discovery.](media/snapshot-report-management.png)

## Using traffic logs for cloud discovery

Cloud discovery uses the data in your traffic logs. The more detailed your log, the better visibility you get. Cloud discovery requires web-traffic data with the following attributes:

- Date of the transaction
- Source IP
- Source user - highly recommended
- Destination IP address
- Destination URL **recommended** (URLs provide higher accuracy for cloud app detection than IP addresses)
- Total amount of data (data information is highly valuable)
- Amount of uploaded or downloaded data (provides insights about the usage patterns of the cloud apps)
- Action taken (allowed/blocked)

Cloud discovery can't show or analyze attributes that aren't included in your logs. For example, **Cisco ASA Firewall** standard log format doesn't have the **number of uploaded bytes per transaction**, **Username**, and **Target URL** (only target IP). Therefore, these attributes won't be shown in cloud discovery data for these logs, and the visibility into the cloud apps will be limited. For Cisco ASA firewalls, it's necessary to set the information level to 6.

To successfully generate a cloud discovery report, your traffic logs must meet the following conditions:

1. [Supported firewalls and proxies for cloud discovery](set-up-cloud-discovery#supported-firewalls-and-proxies).
2. Log format matches the expected standard format (format checked upon upload by the Log tool).
3. Events aren't more than 90 days old.
4. The log file is valid and includes outbound traffic information.
5. Configure the appliance to forward only traffic logs. Including unrelated logs in the configuration can inflate the ingested traffic volume.

Important

ZIP upload is supported **only for a single compressed file.** ZIP archives containing multiple log files are **not supported.** Individual log files larger than **1 GB** cannot be uploaded. Split large logs before uploading. You can upload up to 20 files per batch.