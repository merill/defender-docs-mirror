---
layout: Conceptual
title: Use a custom log parser - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/custom-log-parser
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
description: This article provides information about how to use the custom log parser to upload logs for devices that aren't supported to Defender for Cloud Apps.
ms.date: 2023-12-20T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange
locale: en-us
document_id: a6c734b9-2f68-e5ee-b47b-4412a80f9736
document_version_independent_id: a6c734b9-2f68-e5ee-b47b-4412a80f9736
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/custom-log-parser.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: custom-log-parser
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/custom-log-parser.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 5da656c3-98bb-c7a7-74eb-52f1456dd84f
---

# Use a custom log parser - Microsoft Defender for Cloud Apps | Microsoft Learn

Defender for Cloud Apps enables you to configure a custom parser to match and process the format of your logs so that they can be used for cloud discovery. Typically you would use a custom parser if the firewall or device is not explicitly supported by Defender for Cloud Apps. This can be a CSV parser or a custom key value parser.

The custom parser enables you to use logs from unsupported firewalls by following this process.

**To configure a custom parser**:

1. In the Microsoft Defender Portal, under **Cloud Apps**, select **Cloud Discovery** &gt; **Actions** &gt; **Create Cloud Discovery snapshot report**. For example:

    ![Screenshot of the Create new snapshot report option.](media/create-new-snapshot-report.png)
2. Enter a **Report name** and a **Description**
3. Under **Source**, scroll all the way down and select **Custom log format...**. For example:

    ![Screenshot of the Create new cloud discovery snapshot report dialog.](media/custom-log-upload.png)
4. Collect logs from your firewall and proxy, through which users in your organization access the Internet. Make sure to gather logs during times of peak traffic that are representative of all user activity in your organization.
5. Open the logs you want to process in a text editor. Review their format, making sure that the column names in the log correspond to the fields in the **Custom log format** dialog.

    Required fields are marked in the **Custom log format** dialog with an asterisk (\*), and must be present in the logs in the same sequence as presented in the **Custom log format** dialog. Logs are processed only if the required fields are found in the log. Extra fields, which aren't used by Defender for Cloud Apps, are discarded.
6. In the **Custom log format** dialog, fill in the fields based on your data to delineate which columns in the data correlate to specific fields in Defender for Cloud Apps. You may have to modify column names in your log file to correlate properly.

    Note

    The fields are case-sensitive. Make sure you spell and type the names of the columns identically in Defender for Cloud Apps and in the log file. Also, make sure that the date format you choose is identical.

    For example, the following images show a sample log file opened in a text editor, and the corresponding **Custom log format** dialog, populated.

    ![Screenshot of a log file opened in a text editor.](media/log-data.png)

    ![Screenshot of the Custom log format dialog, with populated values.](media/custom-log-parser.png)
7. Select **Save**. The custom log format your configured will be saved as the default custom parser. You can edit it at any time by selecting **Edit**.
8. Under **Upload traffic logs**, select the log file you modified and select **Upload logs** to upload it. You can upload up to 20 files at once. Compressed and zipped files are also supported.

After the upload completes, a status message shows at the top right-corner of your screen, letting you know that your log was successfully uploaded.

It'll take some time for your logs to be parsed and analyzed. A notification banner shows in the status bar at the top of the **Cloud Discovery &gt; Dashboard** tab, showing you the processing status of your log files. For example:

![Screenshot of a processing log file menu bar.](media/processing-log-file-menu-bar.png)

When the processing of your log files is complete, you'll receive an email to notify you that it's done.

View the report either by selecting the link in the status bar, or select **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Snapshot reports**. Select your snapshot report to open it. For example:

![Screenshot of a the Snapshot reports page.](media/snapshot-report-management.png)