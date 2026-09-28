---
layout: Conceptual
title: Configure automatic log upload using Azure Kubernetes Service - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/discovery-kubernetes
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
description: This article describes the process configuring automatic log upload for continuous reports in Defender for Cloud Apps using Azure Kubernetes Service.
ms.date: 2024-06-02T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: 551ebe48-6720-0200-ed89-b3deb592ae4b
document_version_independent_id: 551ebe48-6720-0200-ed89-b3deb592ae4b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/discovery-kubernetes.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discovery-kubernetes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/discovery-kubernetes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 362dbd9b-fb3a-5c4c-21fd-5ca622122d76
---

# Configure automatic log upload using Azure Kubernetes Service - Microsoft Defender for Cloud Apps | Microsoft Learn

This article describes how to configure automatic log upload for continuous reports in Defender for Cloud Apps using a Docker container on Azure Kubernetes Service (AKS).

Note

Microsoft Defender for Cloud Apps is now part of [Microsoft Defender XDR](https://security.microsoft.com), which correlates signals from across the Microsoft Defender suite and provides incident-level detection, investigation, and powerful response capabilities. For more information, see [Microsoft Defender for Cloud Apps in Microsoft Defender XDR](/en-us/microsoft-365/security/defender/microsoft-365-security-center-defender-cloud-apps).

## Setup and configuration

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
6. Go to your AKS cluster configuration and run:

    ```AzureCLI
    kubectl config use-context <name of AKS cluster>
    ```
7. Run the helm command using the following syntax:

    ```AzureCLI
    helm install <release-name> oci://mcr.microsoft.com/mcas/helmchart/logcollector-chart --version 1.0.5 --set inputString="<generated id> ",env.PUBLICIP="<public ip>",env.SYSLOG="true",env.COLLECTOR="<collector-name>",env.CONSOLE="<Console-id>",env.INCLUDE_TLS="on" --set-file ca=<absolute path of ca.pem file> --set-file serverkey=<absolute path of server-key.pem file> --set-file servercert=<absolute path of server-cert.pem file> --set replicas=<no of replicas> -n <namespace>
    ```

    Find the values for the helm command using the docker command used when the collector is configured. For example:

    ```azurecli
    (echo <Generated ID>) | docker run --name SyslogTLStest
    ```

When successful, the logs show pulling an image from mcr.microsoft.com and continuing to create blobs for the container.