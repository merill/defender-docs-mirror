---
layout: Conceptual
title: 'Tutorial: Forward Syslog data to Microsoft Sentinel and Azure Monitor by using Azure Monitor Agent | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/forward-syslog-monitor-agent
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: In this tutorial, you learn how to monitor Linux-based devices by forwarding Syslog data to a Log Analytics workspace.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: tutorial
ms.date: 2024-05-16T00:00:00.0000000Z
ms.custom: template-tutorial, linux-related-content
locale: en-us
document_id: cf5c41bf-c8a7-718e-2d94-65412dc0e9d6
document_version_independent_id: dee8aec9-ad8c-97fb-39f6-a134ba1ae88e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/forward-syslog-monitor-agent.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/forward-syslog-monitor-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/forward-syslog-monitor-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 07488160-1924-3530-e143-363f1a7cb5e4
---

# Tutorial: Forward Syslog data to Microsoft Sentinel and Azure Monitor by using Azure Monitor Agent | Microsoft Learn

In this tutorial, you configure a Linux virtual machine (VM) to forward Syslog data to your workspace by using Azure Monitor Agent. These steps allow you to collect and monitor data from Linux-based devices where you can't install an agent like a firewall network device.

Note

Container Insights now supports the automatic collection of Syslog events from Linux nodes in your AKS clusters. To learn more, see [Syslog collection with Container Insights](/en-us/azure/azure-monitor/containers/container-insights-syslog).

Configure your Linux-based device to send data to a Linux VM. Azure Monitor Agent on the VM forwards the Syslog data to the Log Analytics workspace. Then use Microsoft Sentinel or Azure Monitor to monitor the device from the data stored in the Log Analytics workspace.

In this tutorial, you learn how to:

- Create a data collection rule.
- Verify that Azure Monitor Agent is running.
- Enable log reception on port 514.
- Verify that Syslog data is forwarded to your Log Analytics workspace.

## Prerequisites

To complete the steps in this tutorial, you must have the following resources and roles:

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An Azure account with the following roles to deploy the agent and create the data collection rules.

    | Built-in role | Scope | Reason |
    | --- | --- | --- |
    | - [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles)- [Azure Connected Machine Resource Administrator](/en-us/azure/role-based-access-control/built-in-roles) | - Virtual machines- Scale sets- Azure Arc-enabled servers | To deploy the agent |
    | Any role that includes the action Microsoft.Resources/deployments/\* | - Subscription - Resource group- Existing data collection rule | To deploy Azure Resource Manager templates |
    | [Monitoring Contributor](/en-us/azure/role-based-access-control/built-in-roles) | - Subscription - Resource group - Existing data collection rule | To create or edit data collection rules |
- A Log Analytics workspace.
- A Linux server that's running an operating system that supports Azure Monitor Agent.

    - [Supported Linux operating systems for Azure Monitor Agent](/en-us/azure/azure-monitor/agents/agents-overview#linux).
    - [Create a Linux VM in the Azure portal](/en-us/azure/virtual-machines/linux/quick-create-portal) or [add an on-premises Linux server to Azure Arc](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm).
- A Linux-based device that generates event log data like a firewall network device.

## Create the DCR and add resources

To create the DCR and add resources, follow the steps in these articles:

- [Create the data collection rule](/en-us/azure/azure-monitor/vm/data-collection#create-a-data-collection-rule)
- [Add resources](/en-us/azure/azure-monitor/vm/data-collection#add-resources)

## Configure Syslog data source

On the **Collect and deliver** tab of the DCR, select **Linux Syslog** from the **Data source type** dropdown.

Select a **Minimum log level** for each facility or **NONE** to collect no events for that facility. You can configure multiple facilities at once by selecting their checkbox and then selecting a log level in **Set minimum log level for selected facilities**. Checkboxes are cleared each time you open an existing DCR, so they don't show which facilities are currently collected.

[![Screenshot that shows the page to select the data source type and minimum log level.](/en-us/azure/azure-monitor/vm/media/data-collection-syslog/create-rule-data-source.png)](/en-us/azure/azure-monitor/vm/media/data-collection-syslog/create-rule-data-source.png#lightbox)

All logs with the selected severity level and higher are collected for the facility. The supported severity levels and their relative severity are as follows:

1. Debug
2. Info
3. Notice
4. Warning
5. Error
6. Critical
7. Alert
8. Emergency

## Add destinations

Syslog data can only be sent to a Log Analytics workspace where it's stored in the [Syslog](/en-us/azure/azure-monitor/reference/tables/syslog) table. Add a destination of type **Azure Monitor Logs** and select a Log Analytics workspace. While you can add multiple workspaces, be aware that this will send duplicate data to each which will result in additional cost.

[![Screenshot that shows configuration of an Azure Monitor Logs destination in a data collection rule.](/en-us/azure/azure-monitor/vm/media/data-collection/destination-workspace.png)](/en-us/azure/azure-monitor/vm/media/data-collection/destination-workspace.png#lightbox)

## Verify data collection

To verify that data is being collected, check for records in the **Syslog** table. From the virtual machine or from the Log Analytics workspace in the Azure portal, select **Logs** and then click the **Tables** button. Under the **Virtual machines** category, click **Run** next to **Syslog**.

[![Screenshot that shows records returned from Syslog table.](/en-us/azure/azure-monitor/vm/media/data-collection-syslog/verify-syslog.png)](/en-us/azure/azure-monitor/vm/media/data-collection-syslog/verify-syslog.png#lightbox)

For the full procedure of configuring Syslog data collection, see [Collect Syslog events with Azure Monitor Agent](/en-us/azure/azure-monitor/agents/data-collection-syslog).

## Verify that Azure Monitor Agent is running

In Microsoft Sentinel or Azure Monitor, verify that Azure Monitor Agent is running on your VM.

1. In the Azure portal, search for and open **Microsoft Sentinel** or **Azure Monitor**.
2. If you're using Microsoft Sentinel, select the appropriate workspace.
3. Under **General**, select **Logs**.
4. Close the **Queries** page so that the **New Query** tab appears.
5. Run the following query where you replace the computer value with the name of your Linux VM.

    ```kusto
    Heartbeat
    | where Computer == "vm-linux"
    | take 10
    ```

## Enable log reception on port 514

Verify that the VM that's collecting the log data allows reception on port 514 TCP or UDP depending on the Syslog source. Then configure the built-in Linux Syslog daemon on the VM to listen for Syslog messages from your devices. After you finish those steps, configure your Linux-based device to send logs to your VM.

Note

If the firewall is running, a rule will need to be created to allow remote systems to reach the daemon’s syslog listener: `systemctl status firewalld.service`

1. Add for tcp 514 (your zone/port/protocol may differ depending on your scenario) `firewall-cmd --zone=public --add-port=514/tcp --permanent`
2. Add for udp 514 (your zone/port/protocol may differ depending on your scenario) `firewall-cmd --zone=public --add-port=514/udp --permanent`
3. Restart the firewall service to ensure new rules take effect `systemctl restart firewalld.service`

The following two sections cover how to add an inbound port rule for an Azure VM and configure the built-in Linux Syslog daemon.

### Allow inbound Syslog traffic on the VM

If you're forwarding Syslog data to an Azure VM, follow these steps to allow reception on port 514.

1. In the Azure portal, search for and select **Virtual Machines**.
2. Select the VM.
3. Under **Settings**, select **Networking**.
4. Select **Add inbound port rule**.
5. Enter the following values.

    | Field | Value |
    | --- | --- |
    | Destination port ranges | 514 |
    | Protocol | TCP or UDP depending on Syslog source |
    | Action | Allow |
    | Name | AllowSyslogInbound |

    Use the default values for the rest of the fields.
6. Select **Add**.

### Configure the Linux Syslog daemon

Connect to your Linux VM and configure the Linux Syslog daemon. For example, run the following command, adapting the command as needed for your network environment:

```bash
sudo wget -O Forwarder_AMA_installer.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Forwarder_AMA_installer.py&&sudo python3 Forwarder_AMA_installer.py
```

This script can make changes for both rsyslog.d and syslog-ng.

Note

To avoid [Full Disk scenarios](/en-us/azure/azure-monitor/agents/azure-monitor-agent-troubleshoot-linux-vm-rsyslog) where the agent can't function, you must set the `syslog-ng` or `rsyslog` configuration to not store logs, which are not needed by the agent. A Full Disk scenario disrupts the function of the installed Azure Monitor Agent. Read more about [rsyslog](https://www.rsyslog.com/doc/configuration/actions.html) or [syslog-ng](https://www.syslog-ng.com/technical-documents).

## Verify Syslog data is forwarded to your Log Analytics workspace

After you configure your Linux-based device to send logs to your VM, verify that Azure Monitor Agent is forwarding Syslog data to your workspace.

1. In the Azure portal, search for and open **Microsoft Sentinel** or **Azure Monitor**.
2. If you're using Microsoft Sentinel, select the appropriate workspace.
3. Under **General**, select **Logs**.
4. Close the **Queries** page so that the **New Query** tab appears.
5. Run the following query where you replace the computer value with the name of your Linux VM.

    ```kusto
    Syslog
    | where Computer == "vm-linux"
    | summarize by HostName
    ```

## Clean up resources

Evaluate whether you need the resources like the VM that you created. Resources you leave running can cost you money. Delete the resources you don't need individually. You can also delete the resource group to delete all the resources you created.