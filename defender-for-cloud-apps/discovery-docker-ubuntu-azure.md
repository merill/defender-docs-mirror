---
layout: Conceptual
title: Configure automatic log upload using Docker in Azure - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/discovery-docker-ubuntu-azure
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
description: Set up automatic log uploads for continuous reports in Defender for Cloud Apps by deploying a Docker-based log collector on Ubuntu or CentOS in Azure. Covers prerequisites, data source configuration, and deployment steps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 097dafe5-b187-6e50-f225-1a6fd8d8e5fb
document_version_independent_id: 097dafe5-b187-6e50-f225-1a6fd8d8e5fb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/discovery-docker-ubuntu-azure.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discovery-docker-ubuntu-azure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/discovery-docker-ubuntu-azure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d3083624-c541-32cd-fb32-e1a96ffaf2d2
---

# Configure automatic log upload using Docker in Azure - Microsoft Defender for Cloud Apps | Microsoft Learn

This article describes how to configure automatic log uploads for continuous reports in Defender for Cloud Apps using a Docker on Ubuntu or CentOS in Azure.

## Prerequisites

Before you start, make sure that your environment meets the following requirements:

| Requirement | Description |
| --- | --- |
| **OS** | One of the following: - Ubuntu 14.04, 16.04, 18.04, and 20.04 - CentOS 7.2 or higher |
| **Disk space** | 250 GB |
| **CPU cores** | 2 |
| **CPU architecture** | Intel 64 and AMD 64 |
| **RAM** | 4 GB |
| **Firewall configuration** | As defined in [Network requirements](network-requirements#log-collector) |
| **Root access** | Root access to the log collector machine is required for Docker deployment |

### Plan your log collectors by performance

Each log collector can successfully handle log capacity of up to 50 GB per hour comprised of up to 10 data sources. The main bottlenecks in the log collection process are:

- Network bandwidth - Your network bandwidth determines the log upload speed.
- I/O performance of the virtual machine - Determines the speed at which logs are written to the log collector's disk. The log collector has a built-in safety mechanism that monitors the rate at which logs arrive and compares it to the upload rate. In cases of congestion, the log collector starts to drop log files. If your setup typically exceeds 50 GB per hour, we recommend that you split the traffic between multiple log collectors.

If you require more than 10 data sources, we recommend that you split the data sources between multiple log collectors.

## Define your data sources

Perform the following steps to define your data sources:

1. In the Microsoft Defender Portal, select **Settings &gt; Cloud Apps &gt; Cloud Discovery &gt; Automatic log upload**.
2. On the **Data sources** tab, create a matching data source for each firewall or proxy from which you want to upload logs:

    1. Select **Add data source**.
    2. In the **Add data source** dialog, enter a name for your data source, and then select the source and receiver type.

        Before selecting a source, select **View sample of expected log file** and compare your log with the expected format. If your log file format doesn't match this sample, add your data source as **Other**.

        To work with a network appliance that isn't listed, select **Other &gt; Customer log format** or **Other (manual only)**. For more information, see [Working with the custom log parser](custom-log-parser).

    Note

    Integrating with secure transfer protocols (FTPS and Syslog – TLS) often requires additional settings on your firewall/proxy. For more information, see [Advanced log collector management](log-collector-advanced-management).

Repeat these data source creation steps for each firewall and proxy whose logs can be used to detect traffic on your network.

We recommend that you set up a dedicated data source per network device, enabling you to monitor the status of each device separately for investigation purposes, and to explore Shadow IT Discovery per device if each device is used by a different user segment.

## Create a log collector

Perform the following steps to create a log collector:

1. In the Microsoft Defender Portal, select **Settings &gt; Cloud Apps &gt; Cloud Discovery &gt; Automatic log upload**.
2. On the **Log collectors** tab, select **Add log collector**.
3. In the **Create log collector** dialog, enter the following details:

    - A name for your log collector
    - The host IP address, which is the private IP address of the machine you'll use to deploy the Docker. The host IP address can also be replaced with the machine name, if there is a DNS server or equivalent to resolve the host name.

    Then select the **Data source(s)** box to select the data sources you want to connect to the collector, and select **Update** to save your changes. Each log collector can handle multiple data sources.

    The **Create log collector** dialog shows further deployment details, including a command to import the collector configuration. For example:

    ![Screenshot of the command to copy from the Create log collector dialog.](media/discovery-docker-ubuntu-azure/import-collector.png)
4. Select the ![Copy the command to clipboard icon.](media/copy-icon.png)**Copy** icon next to the command to copy it to your clipboard.

    The details displayed in the **Create log collector** dialog differ, depending on the source type and receiver type you chose when creating each data source. For example, if you selected Syslog, the dialog includes details about which port the syslog listener is listening on.

    Copy the contents of the screen and save them locally, as you'll need them when you configure the log collector to communicate with Defender for Cloud Apps.
5. Select **Export** to export the source configuration to a .CSV file that describes how to configure the log export in your appliances.

Tip

For users sending log data via FTP for the first time, we recommend changing the password for the FTP user. For more information, see [Changing the FTP password](log-collector-advanced-management#change-the-ftp-password).

## Deploy your machine in Azure

This procedure describes how to deploy the log collector host machine with Ubuntu. The deployment steps for other platforms are slightly different. Docker CE is installed later in this procedure during the Docker installation step. Make sure you have root access to the machine before you begin.

1. Create a new Ubuntu machine in your Azure environment.
2. After the machine is up, open the ports:

    1. In the machine view, go to **Networking** select the relevant interface by double-clicking on it.
    2. Go to **Network security group** and select the relevant network security group.
    3. Go to **Inbound security rules** and click **Add**.
    4. Add the following rules (in **Advanced** mode):

        | Name | Destination port ranges | Protocol | Source | Destination |
        | --- | --- | --- | --- | --- |
        | caslogcollector\_ftp | 21 | TCP | `Your appliance's IP address's subnet` | Any |
        | caslogcollector\_ftp\_passive | 20000-20099 | TCP | `Your appliance's IP address's subnet` | Any |
        | caslogcollector\_syslogs\_tcp | 601-700 | TCP | `Your appliance's IP address's subnet` | Any |
        | caslogcollector\_syslogs\_udp | 514-600 | UDP | `Your appliance's IP address's subnet` | Any |

    For more information, see [Work with security rules](/en-us/azure/virtual-network/manage-network-security-group#work-with-security-rules).
3. Go back to the machine and click **Connect** to open a terminal on the machine.
4. Change to root privileges using `sudo -i`.
5. If you accept the software license terms, uninstall old versions and install Docker CE by running the commands appropriate for your environment:

# [CentOS](#tab/centos)
1. Remove old versions of Docker: `yum erase docker docker-engine docker.io`
    2. Install Docker engine prerequisites: `yum install -y yum-utils`
    3. Add Docker repository:

        ```bash
        yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
        yum makecache
        ```
    4. Install Docker engine: `yum -y install docker-ce`
    5. Start Docker

        ```bash
        systemctl start docker
        systemctl enable docker
        ```
    6. Test Docker installation: `docker run hello-world`

# [Ubuntu](#tab/ubuntu)
1. Remove old versions of Docker: `apt-get remove docker docker-engine docker.io`
    2. If you are installing on Ubuntu 14.04, install the linux-image-extra package.

        ```bash
        apt-get update -y
        apt-get install -y linux-image-extra-$(uname -r) linux-image-extra-virtual
        ```
    3. Install Docker engine prerequisites:

        ```bash
        apt-get update -y
        (apt-get install -y apt-transport-https ca-certificates curl software-properties-common && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - )
        ```
    4. Verify that the apt-key fingerprint UID is docker@docker.com: `apt-key fingerprint | grep uid`
    5. Install Docker engine:

        ```bash
        add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
        apt-get update -y
        apt-get install -y docker-ce
        ```
    6. Test Docker installation: `docker run hello-world`

---
6. Run the collector configuration command that you copied from the **Create log collector** dialog. For example:

    ```bash
    (echo db3a7c73eb7e91a0db53566c50bab7ed3a755607d90bb348c875825a7d1b2fce) | docker run --name MyLogCollector -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='192.168.1.1'" -e "PROXY=192.168.10.1:8080" -e "CONSOLE=mod244533.us.portal.cloudappsecurity.com" -e "COLLECTOR=MyLogCollector" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    ```
7. To verify that the log collector is running properly, run the following command: `docker logs <collector_name>`. You should get the results: **Finished successfully!**

## Configure on-premises network appliance settings

Configure your network firewalls and proxies to periodically export logs to the dedicated Syslog port of the FTP directory according to the directions in the **Create log collector** dialog. The following example shows the destination path format for a data source named `BlueCoat_HQ`, where `<machine_name>` is the name of your log collector machine:

```text
BlueCoat_HQ - Destination path: \<<machine_name>>\BlueCoat_HQ\
```

### Verify your deployment in Defender for Cloud Apps

If the status is **Created**, the log collector connection and parsing might still be in progress. Check the collector status in the **Log collector** table and confirm that the status changes to **Connected**.

For example:

[![Screenshot of a connected collector status.](media/collector-status-connected.png)](media/collector-status-connected.png#lightbox)

You can also go to the **Governance log** and verify that logs are being periodically uploaded to the portal.

Alternatively, you can check the log collector status from within the docker container using the following commands:

1. Log in to the container by using this command: `docker exec -it <Container Name> bash`
2. Verify the log collector status using this command: `collector_status -p`

If you have problems during deployment, see [Troubleshooting cloud discovery](troubleshooting-cloud-discovery).

## Optional - Create custom continuous reports

Verify that the logs are being uploaded to Defender for Cloud Apps and that reports are generated. After verification, create custom reports. You can create custom discovery reports based on Microsoft Entra user groups. For example, if you want to see the cloud use of your marketing department, import the marketing group using the import user group feature. Then create a custom report for this group. You can also customize a report based on IP address tag or IP address ranges.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Cloud Discovery**, select **Continuous reports**.
3. Click the **Create report** button and fill in the fields.
4. Under the **Filters** you can filter the data by data source, by [imported user group](user-groups), or by [IP address tags and ranges](ip-tags).

    Note

    When applying filters on continuous reports, the selection will be included, not excluded. For example, if you apply a filter on a certain user group, only that user group will be included in the report.

    ![Screenshot of the custom continuous report configuration page with filter options for data source, user group, and IP address ranges.](media/custom-continuous-report.png)

## Remove your log collector

Warning

Removing the log collector container stops all log ingestion for the associated data sources. No logs are uploaded until you redeploy or reconfigure a new log collector.

If you have an existing log collector and want to remove it before deploying it again, or if you simply want to remove it, run the following commands to stop and delete the log collector Docker container:

```console
docker stop <collector_name>
docker rm <collector_name>
```