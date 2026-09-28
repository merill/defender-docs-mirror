---
layout: Conceptual
title: Configure automatic log upload using on-premises Docker on Windows - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/discovery-docker-windows
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
description: Configure automatic log upload for continuous reports in Microsoft Defender for Cloud Apps using Docker on an on-premises Windows server.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ab601b7d-5f37-4d4f-ed95-a8e0c7422220
document_version_independent_id: ab601b7d-5f37-4d4f-ed95-a8e0c7422220
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/discovery-docker-windows.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discovery-docker-windows
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/discovery-docker-windows.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 67586f5a-495f-9826-e035-d7fe675c759e
---

# Configure automatic log upload using on-premises Docker on Windows - Microsoft Defender for Cloud Apps | Microsoft Learn

You can configure automatic log upload for continuous reports in Microsoft Defender for Cloud Apps using a Docker container on an on-premises Windows server. This article walks you through setting up data sources in the Microsoft Defender portal, deploying the Docker-based log collector, configuring your network appliances to forward logs, and verifying the deployment.

## Prerequisites

Before you deploy the log collector, make sure the following prerequisites are met:

- Firewall log forwarding must be configured to send logs to the log collector host machine.
- **Architecture specifications**:

    | Specification | Description |
    | --- | --- |
    | **Operating system** | Windows 10 (Fall creators update) |
    | **Disk space** | 250 GB |
    | **CPU cores** | 2 |
    | **CPU architecture** | Intel 64 and AMD 64 |
    | **RAM** | 4 GB |

    For a list of supported Docker architectures, see [Docker installation documentation](https://docs.docker.com/engine/install/).
- **Set your firewall** as needed. For more information, see [Network requirements](network-requirements#log-collector).
- **Virtualization** on the operating system must be enabled with Hyper-V.

Important

- Enterprise customers with more than 250 users or more than $10 million USD in annual revenue require a paid subscription to use Docker Desktop for Windows. For more information, see [Docker subscription overview](https://docs.docker.com/subscription/).
- A user must be signed in for Docker to collect logs. We recommend advising your Docker users to disconnect without signing out.
- Docker for Windows isn't officially supported in VMWare virtualization scenarios.
- Docker for Windows isn't officially supported in nested virtualization scenarios. If you still plan to use nested virtualization, refer to [Docker Desktop for Windows on a VM or VDI environment](https://docs.docker.com/desktop/setup/vm-vdi/).
- For information about additional configuration and implementation considerations for Docker for Windows, see [Install Docker Desktop on Windows](https://docs.docker.com/desktop/windows/install/).

## Remove an existing log collector

If you have an existing log collector and want to remove it before deploying it again, or if you simply want to remove it, use the following steps:

1. Stop the log collector:

    ```console
    docker stop <collector_name>
    ```
2. Remove the log collector:

    ```console
    docker rm <collector_name>
    ```

## Log collector performance

The log collector can successfully handle log capacity of up to 50 GB per hour. The main bottlenecks in the log collection process are:

- Network bandwidth - Your network bandwidth determines the log upload speed.
- I/O performance of the virtual machine - Determines the speed at which logs are written to the log collector's disk. The log collector has a built-in safety mechanism that monitors the rate at which logs arrive and compares it to the upload rate. In cases of congestion, the log collector starts to drop log files. If your setup typically exceeds 50 GB per hour, it's recommended that you split the traffic between multiple log collectors.

## Step 1 – Web portal configuration

Use the following steps to define your data sources and link them to a log collector. A single log collector can handle multiple data sources.

1. In the Microsoft Defender portal, select **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Automatic log upload** &gt; **Data sources** tab.
2. For each firewall or proxy from which you want to upload logs, create a matching data source:

    1. Select **+Add data source**.

        ![Screenshot of the Data sources tab showing the Add data source button in Cloud Discovery settings.](media/add-data-source.png)
    2. **Name** your proxy or firewall.

        ![Screenshot of the Add data source dialog with fields for name, source, and receiver type.](media/ubuntu1.png)
    3. Select the appliance from the **Source** list. If you select **Custom log format** to work with a network appliance that isn't listed, see [Working with the custom log parser](custom-log-parser) for configuration instructions.
    4. Compare your log with the sample of the expected log format. If your log file format doesn't match this sample, you should add your data source as **Other**.
    5. Set the **Receiver type** to either **FTP**, **FTPS**, **Syslog – UDP**, or **Syslog – TCP**, or **Syslog – TLS**.

        Note

        Integrating with secure transfer protocols (FTPS and Syslog – TLS) often requires additional settings for your firewall/proxy.
    6. Repeat these data source configuration steps for each firewall and proxy whose logs can be used to detect traffic on your network. We recommend that you set up a dedicated data source per network device to enable you to:

        - Monitor the status of each device separately, for investigation purposes.
        - Explore Shadow IT Discovery per device, if each device is used by a different user segment.
3. At the top of the page, select the **Log collectors** tab and then select **Add log collector**.
4. In the **Create log collector** dialog:

    1. In the **Name** field, enter a meaningful name for your log collector.
    2. Give the log collector a **name** and enter the **Host IP address** (private IP address) of the machine you'll use to deploy the Docker. The host IP address can be replaced with the machine name, if there's a DNS server (or equivalent) that will resolve the host name.
    3. Select all **Data sources** that you want to connect to the collector, and select **Update** to save the configuration.

        Further deployment information appears in the dialog's **Next steps** section, including a command used in Step 2 – On-premises deployment of your machine to import the collector configuration. If you selected Syslog, this information also includes data about which port the Syslog listener is listening on.
    4. Use the ![Copy command to clipboard](media/copy-icon.png)**Copy** button to copy the command to the clipboard and save it to a separate location.
    5. Use the ![Export data source configuration](media/export-icon.png)**Export** button to export the expected data source configuration. This configuration describes how you should set the log export in your appliances.

For users sending log data via FTP for the first time, we recommend changing the password for the FTP user. For more information, see [Changing the FTP password](log-collector-advanced-management#change-the-ftp-password).

## Step 2 – On-premises deployment of your machine

The following steps describe deployment of the Docker-based log collector on Windows. The deployment steps for other platforms are slightly different.

1. Open a PowerShell terminal as an administrator on your Windows machine.
2. Run the following command to download the Windows Docker installer PowerShell script file:

    ```powershell
    Invoke-WebRequest https://discoveryresources-cdn-prod.cloudappsecurity.com/prod1/public-files/LogCollectorInstaller.ps1 -OutFile (Join-Path $Env:Temp LogCollectorInstaller.ps1) 
    ```

    To validate that the installer is signed by Microsoft, see Validate installer signature.
3. To enable PowerShell script execution, run:

    ```powershell
    Set-ExecutionPolicy RemoteSigned`
    ```
4. To install the Docker client on your machine, run:

    ```powershell
    & (Join-Path $Env:Temp LogCollectorInstaller.ps1)`
    ```

    The machine automatically restarts after you run the command.
5. When the machine is up and running again, run the `LogCollectorInstaller.ps1` script again:

    ```powershell
    & (Join-Path $Env:Temp LogCollectorInstaller.ps1)`
    ```
6. Run the Docker installer, selecting to use WSL 2 instead of Hyper-V.

    After the installation is completed, the machine automatically restarts again.
7. After the restart is completed, open the Docker client and accept the Docker subscription agreement.
8. If the WSL 2 installation isn't completed, Docker Desktop displays a message indicating that the WSL 2 Linux kernel must be installed using a separate MSI update package.
9. Complete the installation by downloading the package. For more information, see [Download the Linux kernel update package](/en-us/windows/wsl/install-manual).
10. Open the Docker Desktop client again and make sure that it has started.
11. Open a command prompt as an administrator and enter the run command you copied from the portal in Step 1 – Web portal configuration.

    If you need to configure a proxy, add the proxy IP address and port number. For example, if your proxy details are 172.31.255.255:8080, your updated run command is:

    ```console
    (echo db3a7c73eb7e91a0db53566c50bab7ed3a755607d90bb348c875825a7d1b2fce) | docker run --name MyLogCollector -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='10.255.255.255'" -e "PROXY=172.31.255.255:8080" -e "CONSOLE=mod244533.us.portal.cloudappsecurity.com" -e "COLLECTOR=MyLogCollector" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    ```
12. To verify that the collector is running properly, run:

    ```bash
    docker logs <collector_name>
    ```

    You should see the message: **Finished successfully!** For example:

    ![Screenshot of docker logs output displaying the Finished successfully message, confirming the log collector is running.](media/ubuntu8.png)

## Step 3 - On-premises configuration of your network appliances

Configure your network firewalls and proxies to periodically export logs to the log collector according to the directions in the **Create log collector** dialog. For Syslog data sources, forward logs to the collector's assigned Syslog port. For FTP data sources, export logs to the collector's FTP destination directory. For example:

```console
BlueCoat_HQ - Destination path: \<<machine_name>>\BlueCoat_HQ\
```

## Step 4 - Verify the successful deployment in the portal

Check the collector status in the **log collector** table and make sure the status is **Connected**. If it's **Created**, it's possible the log collector connection and parsing haven't completed.

[![Verify that the collector status is Connected.](media/collector-status-connected.png)](media/collector-status-connected.png#lightbox)

You can also go to the **Governance log** and verify that logs are being periodically uploaded to the portal.

Alternatively, you can check the log collector status from within the docker container using the following commands:

1. Sign in to the container:

    ```bash
    docker exec -it <Container Name> bash
    ```
2. Verify the log collector status:

    ```bash
    collector_status -p
    ```

If you have problems during deployment, see [Troubleshooting cloud discovery](troubleshooting-cloud-discovery).

## Optional - Create custom continuous reports

Verify that the logs are being uploaded to Defender for Cloud Apps and that reports are generated. After verification, create custom reports. You can create custom discovery reports based on Microsoft Entra user groups. For example, if you want to see the cloud use of your marketing department, import the marketing group using the import user group feature. Then create a custom report for this group. You can also customize a report based on IP address tag or IP address ranges.

1. In the Microsoft Defender portal, select **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Continuous reports**.
2. Select the **Create report** button and fill in the fields.
3. Under the **Filters** you can filter the data by data source, by [imported user group](user-groups), or by [IP address tags and ranges](ip-tags).

    Note

    When applying filters on continuous reports, the selection will be included, not excluded. For example, if you apply a filter on a certain user group, only that user group will be included in the report.

    ![Screenshot of the custom continuous report configuration page showing filters for data source, user groups, and IP address tags or ranges.](media/custom-continuous-report.png)

## Optional - Validate installer signature

To make sure that the docker installer is signed by Microsoft:

1. Right-click on the file and select **Properties**.
2. Select **Digital Signatures** and make sure that it says **This digital signature is OK**.
3. Make sure that **Microsoft Corporation** is listed as the sole entry under **Name of signer**.

    ![Screenshot of digital signature details confirming the file is validly signed by Microsoft Corporation.](media/digital-signature-successful.png)

    If the digital signature isn't valid, it will say **This digital signature is not valid**:

    ![Screenshot of digital signature details indicating the signature verification failed.](media/digital-signature-unsuccessful.png)