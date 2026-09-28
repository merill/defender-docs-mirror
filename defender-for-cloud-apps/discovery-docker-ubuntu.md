---
layout: Conceptual
title: Configure automatic log upload using on-premises Docker on Linux - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/discovery-docker-ubuntu
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
description: Configure automatic log upload for continuous reports in Defender for Cloud Apps by deploying a Docker-based log collector on an on-premises Ubuntu or CentOS server. For RHEL 7.1 or higher, use Podman instead.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 23837e49-77ce-207c-a7b5-732a9c6af30a
document_version_independent_id: 23837e49-77ce-207c-a7b5-732a9c6af30a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/discovery-docker-ubuntu.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discovery-docker-ubuntu
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/discovery-docker-ubuntu.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 510729d6-15fe-195b-4665-c0ff7f468e90
---

# Configure automatic log upload using on-premises Docker on Linux - Microsoft Defender for Cloud Apps | Microsoft Learn

You can configure automatic log upload for continuous reports in Defender for Cloud Apps using a Docker on an on-premises Ubuntu or CentOS server. This article walks you through defining data sources in the Microsoft Defender portal, deploying a Docker-based log collector on your Linux server, configuring your network appliances to export logs, and verifying the deployment. Before you begin, confirm that your environment meets the following minimum requirements.

Important

If you're using RHEL version 7.1 or higher, you must use Podman for automatic log collection instead of Docker. For more information, see [Configure automatic log upload using Podman](discovery-linux-podman).

## Prerequisites

Your machine must meet the following minimum requirements to deploy the log collector:

| Specification | Description |
| --- | --- |
| **Operating system** | One of the following: - Ubuntu 20.04 and 22.04<br>- CentOS 7.2 or higher |
| **Disk space** | 250 GB |
| **CPU cores** | 2 |
| **CPU Architecture** | Intel 64 and AMD 64 |
| **RAM** | 4 GB |

Make sure to set your firewall as needed. For more information, see [Network requirements](network-requirements#log-collector).

## Remove an existing log collector

If you need to redeploy or replace the log collector, stop and remove the existing Docker container first.

Warning

The following commands permanently remove the existing log collector container. Make sure you no longer need the current deployment before continuing.

Run the following commands to stop the running container and delete it:

```console
docker stop <collector_name>
docker rm <collector_name>
```

## Log collector performance

The log collector can successfully handle log capacity of up to 50 GB per hour. The main bottlenecks in the log collection process are:

- Network bandwidth - Your network bandwidth determines the log upload speed.
- I/O performance of the virtual machine - Determines the speed at which logs are written to the log collector's disk. The log collector has a built-in safety mechanism that monitors the rate at which logs arrive and compares it to the upload rate. In cases of congestion, the log collector starts to drop log files. If your setup typically exceeds 50 GB per hour, it's recommended that you split the traffic between multiple log collectors.

## Step 1 – Web portal configuration: Define data sources and link them to a log collector

Perform the following steps in the Microsoft Defender portal to define data sources for your firewalls or proxies and associate them with a log collector.

1. In the Microsoft Defender portal, select **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Automatic log upload** &gt; **Data sources** tab.
2. For each firewall or proxy from which you want to upload logs, create a matching data source.

    1. Select **+Add data source**.

        ![Screenshot showing the Add data source option on the Data sources tab in Cloud Discovery settings.](media/add-data-source.png)
    2. **Name** your proxy or firewall.

        ![Screenshot of the Add data source dialog showing the Name field for entering a proxy or firewall name.](media/ubuntu1.png)
    3. Select the appliance from the **Source** list. If you select **Custom log format** to work with a network appliance that isn't listed, see [Working with the custom log parser](custom-log-parser) for configuration instructions.
    4. Compare your log with the sample of the expected log format. If your log file format doesn't match the expected log format sample shown in the portal, add your data source as **Other**.
    5. Set the **Receiver type** to either **FTP**, **FTPS**, **Syslog – UDP**, or **Syslog – TCP**, or **Syslog – TLS**.

        Note

        Integrating with secure transfer protocols (FTPS and Syslog – TLS) often requires additional settings for your firewall/proxy.
    6. Repeat the data source creation steps for each firewall and proxy whose logs can be used to detect traffic on your network. We recommend that you set up a dedicated data source per network device to enable you to:

    - Monitor the status of each device separately, for investigation purposes.
    - Explore Shadow IT Discovery per device, if each device is used by a different user segment.
3. At the top of the page, select the **Log collectors** tab and then select **Add log collector**.
4. In the **Create log collector** dialog:

    1. In the **Name** field, enter a meaningful name for your log collector.
    2. Give the log collector a **name** and enter the **Host IP address** (private IP address) of the machine you'll use to deploy the Docker. The host IP address can be replaced with the machine name, if there's a DNS server (or equivalent) that will resolve the host name.
    3. Select all **Data sources** that you want to connect to the collector, and select **Update** to save the configuration.

        Further deployment information appears in the **Next steps** section of the dialog, including a command you'll use later in Step 2 – On-premises deployment of your machine to deploy the collector on your Linux host and import the collector configuration. If you selected Syslog, the **Next steps** section also includes the port that the Syslog listener is listening on.
    4. Use the ![Icon for copying the collector configuration command to the clipboard.](media/copy-icon.png)**Copy** button to copy the command to the clipboard and save it to a separate location.
    5. Use the ![Icon for exporting the expected data source configuration.](media/export-icon.png)**Export** button to export the expected data source configuration. This configuration describes how you should set the log export in your appliances.

For users sending log data via FTP for the first time, we recommend changing the password for the FTP user. For more information, see [Changing the FTP password](log-collector-advanced-management#change-the-ftp-password).

## Step 2 – On-premises deployment of your machine

This section describes the on-premises Docker deployment procedure for Ubuntu. The deployment steps for other supported platforms might be slightly different.

1. Open a terminal on your Ubuntu machine.
2. Change to root privileges by running:

    ```bash
    sudo -i
    ```
3. To bypass a proxy in your network, run the following two commands:

    ```bash
    export http_proxy='<IP>:<PORT>' (e.g. 168.192.1.1:8888)
    export https_proxy='<IP>:<PORT>'
    ```
4. If you accept the software license terms, uninstall old versions and install Docker CE by running the commands appropriate for your environment:

# [CentOS](#tab/centos)
1. Remove old versions of Docker:

        ```bash
        yum erase docker docker-engine docker.io
        ```
    2. Install Docker engine prerequisites:

        ```bash
        yum install -y yum-utils
        ```
    3. Add Docker repository:

        ```bash
        yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
        yum makecache
        ```
    4. Install Docker engine:

        ```bash
        yum -y install docker-ce
        ```
    5. Start Docker:

        ```bash
        systemctl start docker
        systemctl enable docker
        ```
    6. Test Docker installation:

        ```bash
        docker run hello-world
        ```

# [Red Hat 7](#tab/red-hat)
1. Remove old versions of Docker:

        ```bash
        yum erase docker docker-engine docker.io
        ```
    2. Install Docker engine prerequisites:

        ```bash
        yum install -y yum-utils
        yum install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.3.7-3.1.el7.x86_64.rpm
        ```
    3. Add Docker repository:

        ```bash
        sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
        sudo yum-config-manager --setopt="docker-ce-stable.baseurl=https://download.docker.com/linux/centos/7/x86_64/stable" --save
        ```
    4. Install dependencies:

        ```bash
        wget http://mirror.centos.org/centos/7/extras/x86_64/Packages/slirp4netns-0.4.3-4.el7_8.x86_64.rpm
        sudo yum localinstall slirp4netns-0.4.3-4.el7_8.x86_64.rpm
        wget https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/f/fuse3-libs-3.6.1-2.el7.x86_64.rpm
        sudo yum localinstall fuse3-libs-3.6.1-2.el7.x86_64.rpm
        wget http://mirror.centos.org/centos/7/extras/x86_64/Packages/fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm
        sudo yum localinstall fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm
        wget http://mirror.centos.org/centos/7/extras/x86_64/Packages/container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm
        sudo yum localinstall container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm
        ```
    5. Install Docker engine:

        ```bash
        sudo yum install docker-ce
        ```
    6. Start Docker:

        ```bash
        systemctl start docker
        systemctl enable docker
        ```
    7. Test Docker installation: `docker run hello-world`

# [Red Hat 8](#tab/red-hat-8)
1. Remove the container-tools module:

        ```bash
        yum module remove container-tools
        ```
    2. Add the Docker CE repository:

        ```bash
        yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
        ```
    3. Modify the yum repo file to use CentOS 8 packages:

        ```bash
        sed -i s/7/8/g /etc/yum.repos.d/docker-ce.repo
        ```
    4. Install Docker CE:

        ```bash
        yum install docker-ce
        ```
    5. Start Docker:

        ```bash
        systemctl start docker
        systemctl enable docker
        ```
    6. Test Docker installation:

        ```bash
        docker run hello-world
        ```

# [Ubuntu](#tab/ubuntu)
1. Remove old versions of Docker:

        ```bash
        apt-get remove docker docker-engine docker.io
        ```
    2. If you're installing on Ubuntu 14.04, install the linux-image-extra package.

        ```bash
        apt-get update -y
        apt-get install -y linux-image-extra-$(uname -r) linux-image-extra-virtual
        ```
    3. Install Docker engine prerequisites:

        ```bash
        apt-get update -y
        (apt-get install -y apt-transport-https ca-certificates curl software-properties-common && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - )
        ```
    4. Verify that the apt-key fingerprint UID is docker@docker.com:

        ```bash
        apt-key fingerprint | grep uid
        ```
    5. Install the Docker engine:

        ```bash
        add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
        apt-get update -y
        apt-get install -y docker-ce
        ```
    6. Test Docker installation:

        ```bash
        docker run hello-world
        ```

---
5. Deploy the collector image on the hosting machine by importing the collector configuration. Import the configuration by copying the run command generated in the portal. If you need to configure a proxy, add the proxy IP address and port number. For example, if your proxy details are 172.31.255.255:8080, your updated run command is:

    ```bash
    (echo 6f19225ea69cf5f178139551986d3d797c92a5a43bef46469fcc997aec2ccc6f) | docker run --name MyLogCollector -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='10.255.255.255'" -e "PROXY=172.31.255.255:8080" -e "CONSOLE=tenant.portal.cloudappsecurity.com" -e "COLLECTOR=MyLogCollector" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    ```
6. Verify that the collector is running properly with the following command:

    ```bash
    docker logs <collector_name>
    ```

    You should see the message: **Finished successfully!** For example:

    ![Screenshot of terminal output showing the Finished successfully message, confirming the log collector container is running.](media/ubuntu8.png)

## Step 3 - On-premises configuration of your network appliances

Configure your network firewalls and proxies to periodically export logs to the dedicated Syslog port or the FTP directory according to the directions in the **Create log collector** dialog. For example, the following destination path shows the FTP folder structure for a data source named BlueCoat\_HQ on the log collector machine:

```text
BlueCoat_HQ - Destination path: \<<machine_name>>\BlueCoat_HQ\
```

## Step 4 - Verify the successful deployment in the portal

Check the collector status in the **Log collector** table and make sure the status is **Connected**. If it's **Created**, it's possible the log collector connection and parsing haven't completed.

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

    ![Screenshot of the custom continuous report configuration page with filter options for data source, user group, and IP address.](media/custom-continuous-report.png)