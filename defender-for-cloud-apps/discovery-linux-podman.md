---
layout: Conceptual
title: Configure automatic log upload using on-premises Podman on Linux - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/discovery-linux-podman
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
description: This article describes how to configure automatic log upload for continuous reports in Defender for Cloud Apps using a Podman container on Linux in an on-premises server.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 31ebfc8c-84bb-92c3-d9f5-3de0c39efe3c
document_version_independent_id: 31ebfc8c-84bb-92c3-d9f5-3de0c39efe3c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/discovery-linux-podman.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discovery-linux-podman
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/discovery-linux-podman.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 79a4f93f-650a-57a5-0a26-d25a1f32cb4c
---

# Configure automatic log upload using on-premises Podman on Linux - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

Microsoft Defender for Cloud Apps is now part of [Microsoft Defender XDR](https://security.microsoft.com), which correlates signals from across the Microsoft Defender suite and provides incident-level detection, investigation, and powerful response capabilities. For more information, see [Microsoft Defender for Cloud Apps in Microsoft Defender XDR](/en-us/microsoft-365/security/defender/microsoft-365-security-center-defender-cloud-apps).

This article describes how to configure automatic log upload for continuous reports in Defender for Cloud Apps using a Podman container on Linux in an on-premises server. Continuous reports automatically upload logs from your network firewalls and proxies to Cloud Discovery, providing ongoing visibility into cloud app usage across your organization. Use this Podman-based on-premises deployment when your environment runs RHEL 7.1 or higher, which requires Podman instead of Docker for automatic log collection. The configuration tasks include setting up a data source, deploying a log collector container, and verifying that logs are uploaded successfully.

## Prerequisites

Before you start:

- Make sure you're using a container with RHEL 7.1 and higher.
- Since Docker and Podman can't coexist on the same machine, make sure to uninstall any Docker installations before running Podman.
- Make sure that you're signed in to the RHEL machine as user `root` to deploy Podman

## Set up automatic log upload using Podman

1. Sign into the Defender portal and select **Settings &gt; Cloud Apps &gt; Cloud Discovery &gt; Automatic log upload**.
2. Make sure that you have a data source defined on the **Data sources** tab. If you don't, select **Add a data source** to add one.
3. Select the **Log collectors** tab, which lists all the log collectors deployed on your tenant.
4. Select the **Add log collector** link. Then, in the **Create log collector** dialog enter:

    | Field | Description |
    | --- | --- |
    | **Name** | Enter a meaningful name, based on key information that the log collector uses, such as your internal naming standard or a site location. |
    | **Host IP address or FQDN** | Enter your log collector's host machine or virtual machine (VM) IP address. Make sure that your syslog service or firewall can access the IP address / FQDN you enter. |
    | **Data source(s)** | Select the data source you want to use. If you're using multiple data sources, the selected source is applied to a separate port so that the log collector can continue to send data consistently. For example, the following list shows examples of data source and port combinations: - Palo Alto: 601 - CheckPoint: 602 - ZScaler: 603 |
5. Select **Create** to show further instructions on the screen for your specific situation.
6. Copy the command displayed and modify it as needed based on the container service you're using. For example:

    ```bash
    (echo <key>) | podman run --privileged --name PodmanTest -p 601:601/tcp -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='10.0.2.15'" -e "PROXY=" -e "SYSLOG=true" -e "CONSOLE= <tenant>.us3.portal.cloudappsecurity.com" -e "COLLECTOR=PodmanTest" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    ```
7. Run the modified command on your machine to deploy the container. When successful, the logs show pulling an image from mcr.microsoft.com and continuing to create blobs for the container.
8. When the container is fully deployed, verify that it's working by checking with the containerization service:

    ```bash
    podman ps
    ```

Note

Podman containers do not start automatically when the host server is rebooted. Restarting the Podman host machine requires you to start the container again too.

## Troubleshooting

If you're not getting firewall logs from your Podman container, check the following:

1. Make sure that rsyslog rotates on the log collector.
2. If you've changed the container configuration or firewall and syslog settings, wait a couple of hours and run the following command to see whether the log status changed:

    ```bash
    podman logs <container name>
    ```

    where `<container name>` is the name of the container you're using.
3. If the logs are still not sent, make sure that the container is deployed using the `--privileged` flag. If you haven't deployed your container with the `--privileged` flag, the container won't gather uploaded files to the host machine.