---
layout: Conceptual
title: Troubleshooting cloud discovery errors - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/troubleshooting-cloud-discovery
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
description: This article provides a list of cloud discovery frequent errors and resolution recommendations for each.
ms.date: 2025-02-19T00:00:00.0000000Z
ms.topic: article
locale: en-us
document_id: da109332-38d1-da48-95d8-c9d0e275292e
document_version_independent_id: da109332-38d1-da48-95d8-c9d0e275292e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/troubleshooting-cloud-discovery.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshooting-cloud-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/troubleshooting-cloud-discovery.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 7cc9731c-7f14-2652-5139-e07271f76df3
---

# Troubleshooting cloud discovery errors - Microsoft Defender for Cloud Apps | Microsoft Learn

This article provides a list of cloud discovery errors and resolution recommendations for each.

Even after Discovery is set up, customers might continue hardening the Operating System in order to meet compliance standards. However, this action might cause interference with the containerization service itself.

## Microsoft Defender for Endpoint integration errors

If you integrated Microsoft Defender for Endpoint with Defender for Cloud Apps, and you don't see the results of the integration.

| Issue | Resolution |
| --- | --- |
| **Defender-managed endpoints** reports don't appear in the list | Make sure the devices you're connecting to are Windows 10 version 1809 or later, and that you waited the necessary two hours that it takes before your data is accessible. |
| **Discovery reports are empty** | If the endpoint device is behind a forward proxy, you can send logs from your forward proxy using a log collector |

## Log parsing errors

You can track the processing of cloud discovery logs using the governance log. This article provides resolution actions to be taken for each error that can be displayed there.

### Governance log errors

| Error | Description | Resolution |
| --- | --- | --- |
| Unsupported file type | The file uploaded isn't a valid log file (for example, an image file). | Upload a **text**, **zip**, or **gzip** file that was directly exported from your firewall or proxy. |
| The log format doesn't match | The log format you uploaded didn't match the expected log format for this data source. | 1. Verify that the log isn't corrupt.  2. Compare and match your log to the sample format shown in the upload page. |
| Transactions are more than 90 days old | All transactions are more than 90 days old and are being ignored. | Export a new log with recent events and reupload it. |
| No transactions to cataloged cloud apps | No transactions to any recognized cloud apps are found in the log. | Verify that the log contains outbound traffic information. |
| Unsupported log type | When you select **Data source = Other (unsupported)**, the log isn't parsed. Instead, it's sent for review to the Defender for Cloud Apps technical team. | The Defender for Cloud Apps technical team builds a dedicated parser per each data source. Most popular data sources are [already supported](set-up-cloud-discovery). Each upload of an unsupported data source is reviewed and added to the pipeline for new data source parsers. New parser notifications are published as part of the Defender for Cloud Apps [release notes](release-notes). |

## Log collector errors

The [Log collector Diagnostic script](https://github.com/microsoft/Microsoft-Defender-for-Cloud-Apps/tree/main/Sample%20scripts/Log-Collector-Diag-Script) automates the collection and compression of logs and diagnostic data for troubleshooting Log Collector containers on Linux (Docker/Podman) to improve workflow efficiency. If you need to contact support, run the script and share the generated log bundle for faster case resolution.

| Issue | Resolution |
| --- | --- |
| Couldn't connect to the log collector over FTP | 1. Verify that you're using FTP credentials and not SSH credentials. 2. Verify that the FTP client you're using isn't set to SFTP (Secure File Transfer Protocol). |
| Failed updating collector configuration | 1. Verify that you entered the latest access token. 2. Verify in your firewall that the log collector is allowed to initiate outbound traffic on port 443. |
| Logs sent to the collector don't appear in the portal | 1. Check to see if there are failed parsing tasks in the Governance log.  If so, troubleshoot the error with the Log Parsing error table above. 2. If not, check the data sources and Log collector configuration in the portal.  a. In the Log collectors page, verify that the data source is linked to the right log collector.  3. Check the local configuration of the on-premises log collector machine.  a. Log in to the log collector over SSH and run the collector\_config utility. b. Confirm that your firewall or proxy is sending logs to the log collector using the protocol you defined (Syslog/TCP, Syslog/UDP, or FTP) and that it's sending them to the correct port and directory. c. Run netstat on the machine and verify that it receives incoming connections from your firewall or proxy  4. Verify that the log collector is allowed to initiate outbound traffic on port 443. |
| Log collector status: Created | The log collector deployment wasn't completed. Complete the on-premises deployment steps according to the deployment guide. |
| Log collector status: Disconnected | If you see this issue, it means no data has been received in the last 24 hours from any of the linked data sources. Contact Microsoft Defender for Cloud Apps support and provide the log files for investigation. Our team analyzes the logs to identify when the last sync occurred and what caused the disconnection. |
| Failed pulling latest collector image | If you get this error during Docker deployment, it could be that you don't have enough memory on the host. To check this, run this command on the host: `docker pull mcr.microsoft.com/mcas/logcollector`. If it returns this error: `failed to register layer: Error processing tar file(exist status 1): write /opt/jdk/jdk1.8.0_152/src.zip: no space left on device` contact your host machine administrator to provide more space. |

## Discovery dashboard errors

| Issue | Resolution |
| --- | --- |
| Discovery data was uploaded and parsed successfully but the cloud discovery dashboard looks empty | The Dashboard might be filtered on data your logs don't have so there's no data to show. Try changing the filters in the cloud discovery dashboard to show different types of data to see the results. |

The [Log collector Diagnostic script](https://github.com/microsoft/Microsoft-Defender-for-Cloud-Apps/tree/main/Sample%20scripts/Log-Collector-Diag-Script) automates the collection and compression of logs and diagnostic data for troubleshooting Log Collector containers on Linux (Docker/Podman) to improve workflow efficiency. If you need to contact support, run the script and share the generated log bundle for faster case resolution.