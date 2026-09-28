---
layout: Conceptual
title: Configure automatic log upload for continuous reports in Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/discovery-docker
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
description: Set up a log collector to automatically upload logs over Syslog or FTP for continuous cloud discovery reports in Microsoft Defender for Cloud Apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: c58378b0-61ad-52d8-d23e-b4ca47e3cd1e
document_version_independent_id: c58378b0-61ad-52d8-d23e-b4ca47e3cd1e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/discovery-docker.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discovery-docker
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/discovery-docker.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: d1ac5020-3f5a-0349-dea9-17d458cbb37a
---

# Configure automatic log upload for continuous reports in Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn

Log collectors enable you to easily automate log upload from your network. The log collector runs on your network and receives logs over Syslog or FTP. Each log is automatically processed, compressed, and transmitted to the portal. FTP logs are uploaded to Microsoft Defender for Cloud Apps after the file finished the FTP transfer to the Log Collector. For Syslog, the Log Collector writes the received logs to the disk. Then the collector uploads the file to Defender for Cloud Apps when the file size is larger than 40 KB.

After a log is uploaded to Defender for Cloud Apps, it's moved to a backup directory. The backup directory stores the last 20 logs. When new logs arrive, the old ones are deleted. Whenever the log collector disk space is full, the log collector drops new logs until it has more free disk space (this shouldn't happen if prerequisites are properly met). You'll receive a warning on the **Log collectors** tab of the **Upload logs automatically** settings when the log collector drops new logs because disk space is full.

Before setting up automatic log file collection, verify your log matches the expected log type. You want to make sure Defender for Cloud Apps can parse your specific file. For more information, see [Using traffic logs for cloud discovery](create-snapshot-cloud-discovery-reports#log-format).

Note

- Defender for Cloud Apps provides support for forwarding logs from your SIEM server to the Log Collector assuming the logs are being forwarded in their original format. However, it is highly recommended that you integrate the log collector directly with your firewall and/or proxy.
- The log collector compresses data before it is uploaded. The outbound traffic on the log collector will be 10% of the size of the traffic logs it receives.
- If the log collector encounters issues, you will receive an alert after data wasn't received for 48 hours.

## Prerequisites

Make sure your environment meets the following system requirements:

- Disk space 250 GB
- CPU cores: 2
- CPU Architecture: Intel® 64 and AMD 64
- RAM: 4 GB
- Set your firewall as described in [Network requirements](/en-us/defender-cloud-apps/network-requirements)

Note

To install a new log collector version, you must stop the log collector, remove the current image, and then install the new one.

Note

If you have an existing log collector and want to remove the collector container before deploying the log collector again, or if you simply want to remove the collector container, run the following commands:

`docker stop <collector_name>`

`docker rm <collector_name>`

## Log collector performance

The Log collector can successfully handle log capacity of up to 50 GB per hour. The main bottlenecks in the log collection process are:

- Network bandwidth - Your network bandwidth determines the log upload speed.
- I/O performance of the virtual machine - Determines the speed at which logs are written to the log collector's disk. The log collector has a built-in safety mechanism that monitors the rate at which logs arrive and compares it to the upload rate. In cases of congestion, the log collector starts to drop log files. If your setup typically exceeds 50 GB per hour, it's recommended that you split the traffic between multiple log collectors.