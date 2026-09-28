---
layout: Conceptual
title: Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel - AMA | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-custom-logs-ama
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
description: Collect text file-based logs from network or security applications installed on Windows- or Linux-based machines, using the Custom Logs via AMA data connector based on the Azure Monitor Agent (AMA).
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.custom: linux-related-content, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: dac8f72d-d465-b13e-c9c3-5921bd608947
document_version_independent_id: 08e4de02-4224-0188-635d-ed36d37101af
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-custom-logs-ama.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-custom-logs-ama
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-custom-logs-ama.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: e4d4a8ff-95d0-0304-c185-d03ea9bc5570
---

# Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel - AMA | Microsoft Learn

This article describes how to use the **Custom Logs via AMA** connector to filter and ingest text-file logs. These logs come from network or security applications installed on Windows or Linux machines. Before you set up the connector, review the Prerequisites section. That section covers required permissions, supported machines, and agent installation.

Many applications log data to text files instead of standard logging services like Windows Event log or Syslog. You can use the Azure Monitor Agent (AMA) to collect data from text files on both Windows and Linux computers. The AMA can also transform the data during collection to parse it into different fields.

For more information about the applications for which Microsoft Sentinel has solutions to support log collection, see [Custom Logs via AMA data connector - Configure data ingestion to Microsoft Sentinel from specific applications](unified-connector-custom-device).

For more general information about ingesting custom logs from text files, see [Collect logs from a text file with Azure Monitor Agent](/en-us/azure/azure-monitor/agents/data-collection-log-text).

Important

- The **Custom Logs via AMA** data connector is currently in PREVIEW. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.
- After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

    If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Prerequisites

Before configuring the Custom Logs via AMA connector, make sure the following resources and permissions are in place.

### Microsoft Sentinel prerequisites

- Install the Microsoft Sentinel solution that matches your application and make sure you have the permissions to complete the steps in this article. You can find these solutions in the **Content hub** in Microsoft Sentinel, and they all include the **Custom Logs via AMA** connector.

    For the list of applications that have solutions in the content hub, see [Specific instructions per application](unified-connector-custom-device#specific-instructions-per-application-type). If there isn't a solution available for your application, install the **Custom Logs via AMA** solution.

    For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).
- Have an Azure account with the following Azure role-based access control (Azure RBAC) roles:

    | Built-in role | Scope | Reason |
    | --- | --- | --- |
    | - [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles/compute#virtual-machine-contributor)- [Azure Connected Machine Resource Administrator](/en-us/azure/role-based-access-control/built-in-roles/management-and-governance#azure-connected-machine-resource-administrator) | - Virtual machines (VM)<br>- Virtual Machine Scale Sets<br>- Azure Arc-enabled servers | To deploy the agent |
    | Any role that includes the action*Microsoft.Resources/deployments/\** | - Subscription<br>- Resource group<br>- Existing data collection rule | To deploy Azure Resource Manager templates |
    | [Monitoring Contributor](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-contributor) | - Subscription<br>- Resource group<br>- Existing data collection rule | To create or edit data collection rules |

### Log forwarder prerequisites

Certain custom applications are hosted on closed appliances that necessitate sending their logs to an external log collector/forwarder. In such a scenario, the following prerequisites apply to the log forwarder:

- You must have a designated Linux VM as a log forwarder to collect logs.

    - [Create a Linux VM in the Azure portal](/en-us/azure/virtual-machines/linux/quick-create-portal).
    - [Supported Linux operating systems for Azure Monitor Agent](/en-us/azure/azure-monitor/agents/agents-overview#linux).
- If your log forwarder *isn't* an Azure virtual machine, it must have the Azure Arc [Connected Machine agent](/en-us/azure/azure-arc/servers/overview) installed on it.
- The Linux log forwarder VM must have Python 2.7 or 3 installed. Use the `python --version` or `python3 --version` command to check. If you're using Python 3, make sure it's set as the default command on the machine, or run scripts with the 'python3' command instead of 'python'.
- The log forwarder must have either the `syslog-ng` or `rsyslog` daemon enabled.
- For space requirements for your log forwarder, refer to the [Azure Monitor Agent Performance Benchmark](/en-us/azure/azure-monitor/agents/azure-monitor-agent-performance). You can also review [Designs for accomplishing Microsoft Sentinel scalable ingestion](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/designs-for-accomplishing-microsoft-sentinel-scalable-ingestion/ba-p/3741516).
- Your log sources, security devices, and appliances must be configured to send their log messages to the log forwarder's syslog daemon instead of to their local syslog daemon.

#### Machine security prerequisites

Configure the log forwarder machine's security according to your organization's security policy. For example, configure your network to align with your corporate network security policy and change the ports and protocols in the daemon to align with your requirements. To improve your machine security configuration, [secure your VM in Azure](/en-us/azure/virtual-machines/security-policy), or review these [best practices for network security](/en-us/azure/security/fundamentals/network-best-practices).

If your devices are sending logs over TLS because, for example, your log forwarder is in the cloud, you need to configure the syslog daemon (`rsyslog` or `syslog-ng`) to communicate in TLS. For more information, see:

- [Encrypt Syslog traffic with TLS – rsyslog](https://docs.rsyslog.com/doc/tutorials/tls_cert_summary.html)
- [Encrypt log messages with TLS – syslog-ng](https://support.oneidentity.com/technical-documents/syslog-ng-open-source-edition/3.22/administration-guide/60#TOPIC-1209298)

## Configure the data connector

The setup process for the Custom Logs via AMA data connector includes the following steps:

1. Create the destination table in Log Analytics (or Advanced Hunting if you're in the Defender portal).

    The table's name must end with `_CL` and it must consist of only the following two fields:

    - **TimeGenerated** (of type *DateTime*): the timestamp of the creation of the log message.
    - **RawData** (of type *String*): the log message in its entirety. (If you're collecting logs from a log forwarder and not directly from the device hosting the application, name this field **Message** instead of **RawData**.)
2. Install the Azure Monitor Agent and create a Data Collection Rule (DCR) by using either of the following methods:

    - [Azure or Defender portal](?tabs=portal#create-data-collection-rule-dcr)
    - [Azure Resource Manager template](?tabs=arm#install-the-azure-monitor-agent)
3. If you're collecting logs using a log forwarder, configure the syslog daemon on that machine to listen for messages from other sources, and open the required local ports. For details, see Configure the log forwarder to accept logs.

Select the appropriate tab for instructions.

# [Azure or Defender portal](#tab/portal)
Use the following steps in the Azure or Defender portal to create and configure the data collection rule.

### Create data collection rule (DCR)

To get started, open either the **Custom Logs via AMA** data connector in Microsoft Sentinel and create a data collection rule (DCR).

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Configuration**, select **Data connectors**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Data connectors**.
2. Type *custom* in the **Search** box. From the results, select the **Custom Logs via AMA** connector.
3. Select **Open connector page** on the details pane.

    [![Screenshot of custom logs AMA connector in gallery.](media/connect-custom-logs-ama/custom-logs-connector-open.png)](media/connect-custom-logs-ama/custom-logs-connector-open.png#lightbox)
4. In the **Configuration** area, select **+Create data collection rule**.

    [![Screenshot showing the Custom Logs via AMA connector page.](media/connect-custom-logs-ama/custom-logs-connector-page-create-dcr.png)](media/connect-custom-logs-ama/custom-logs-connector-page-create-dcr.png#lightbox)
5. In the **Basic** tab:

    - Type a DCR name.
    - Select your subscription.
    - Select the resource group where you want to locate your DCR.

    [![Screenshot showing the DCR details in the Basic tab.](media/connect-cef-ama/dcr-basics-tab.png)](media/connect-cef-ama/dcr-basics-tab.png#lightbox)
6. Select **Next: Resources &gt;**.

### Define VM resources

In the **Resources** tab, select the machines from which you want to collect the logs. These are either the machines on which your application is installed, or your log forwarder machines. If the machine you're looking for doesn't appear in the list, the machine might not be an Azure VM with the Azure Connected Machine agent installed.

1. Use the available filters or search box to find the machine you're looking for. Expand a subscription in the list to see its resource groups, and a resource group to see its VMs.
2. Select the machine that you want to collect logs from. The check box appears next to the VM name when you hover over it.

    [![Screenshot showing how to select resources when setting up the DCR.](media/connect-cef-ama/dcr-select-resources.png)](media/connect-cef-ama/dcr-select-resources.png#lightbox)

    If the machines you selected don't already have the Azure Monitor Agent installed on them, the agent is installed when the DCR is created and deployed.
3. Review your changes and select **Next: Collect &gt;**.

### Configure the DCR for your application

Important

If you select a listed application or device type, the **Transform** field is populated automatically. Do not edit the auto-populated transformation.

1. In the **Collect** tab, select your application or device type from the **Select device type (optional)** drop-down box, or leave it as **Custom new table** if your application or device isn't listed.
2. If you chose one of the listed applications or devices, the **Table name** field is automatically populated with the right table name. If you chose **Custom new table**, enter a table name under **Table name**. The name must end with the `_CL` suffix.
3. In the **File pattern** field, enter the path and file name of the text log files to be collected. To find the default file names and paths for each application or device type, see [Specific instructions per application type](unified-connector-custom-device#specific-instructions-per-application-type). You don't have to use the default file names or paths, and you can use wildcards in the file name.
4. In the **Transform** field, if you chose a custom new table in step 1, enter a Kusto query that applies a transformation of your choice to the data.

    If you chose one of the listed applications or devices in step 1, the **Transform** field is automatically populated with the proper transformation. DO NOT edit the transformation that appears there. Depending on the chosen type, the **Transform** field value should be one of the following:

    - `source` (the default—no transformation)
    - `source | project-rename Message=RawData` (for devices that send logs to a forwarder)
5. Review your selections and select **Next: Review + create**.

### Review and create the rule

After you complete all the tabs, review what you entered and create the data collection rule.

1. In the **Review and create** tab, select **Create**.

    ![Screenshot showing how to review the configuration of the DCR and create it.](media/connect-cef-ama/dcr-review-create.png)

    The connector installs the Azure Monitor Agent on the machines you selected when creating your DCR.
2. Check the notifications in the Azure portal or Microsoft Defender portal to see when the DCR is created and the agent is installed.
3. Select **Refresh** on the connector page to see the DCR displayed in the list.

# [Resource Manager template](#tab/arm)
Use this option to install the agent and create the data collection rule with ARM-based tooling.

### Install the Azure Monitor Agent

Follow the appropriate instructions from the Azure Monitor documentation to install the Azure Monitor Agent on the machine hosting your application, or on your log forwarder. Use the Windows instructions if the machine runs Windows, or the Linux instructions if it runs Linux.

- [Install the AMA using PowerShell](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-powershell)
- [Install the AMA using the Azure CLI](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-cli)
- [Install the AMA using an Azure Resource Manager template](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-resource-manager)

Create Data Collection Rules (DCRs) using the [Azure Monitor Logs Ingestion API](/en-us/rest/api/monitor/data-collection-rules). For more information, see [Data collection rules in Azure Monitor](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview).

### Create the data collection rule

Use the following ARM template to create or modify a data collection rule (DCR) for collecting text log files:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "type": "Microsoft.Insights/dataCollectionRules",
            "name": "{DCR_NAME}",
            "location": "{DCR_LOCATION}",
            "apiVersion": "2022-06-01",
            "properties": {
                "streamDeclarations": {
                    "Custom-Text-{TABLE_NAME}": {
                        "columns": [
                            {
                                "name": "TimeGenerated",
                                "type": "datetime"
                            },
                            {
                                "name": "RawData",
                                "type": "string"
                            },
                        ]
                    }
                },
                "dataSources": {
                    "logFiles": [
                        {
                            "streams": [
                                "Custom-Text-{TABLE_NAME}"
                            ],
                            "filePatterns": [
                                "{LOCAL_PATH_FILE_1}","{LOCAL_PATH_FILE_2}"
                            ],
                            "format": "text",
                            "name": "Custom-Text-{TABLE_NAME}"
                        }
                    ]
                },
                "destinations": {
                    "logAnalytics": [
                        {
                            "workspaceResourceId": "{WORKSPACE_RESOURCE_PATH}",
                            "workspaceId": "{WORKSPACE_ID}",
                            "name": "workspace"
                        }
                    ]
                },
                "dataFlows": [
                    {
                        "streams": [
                            "Custom-Text-{TABLE_NAME}"
                        ],
                        "destinations": [
                            "DataCollectionEvent"
                        ],
                        "transformKql": "source",
                        "outputStream": "Custom-{TABLE_NAME}"
                    }
                ]
            }
        }
    ]
}
```

Replace each placeholder enclosed in braces (for example, `{DCR_NAME}` and `{TABLE_NAME}`) with the appropriate value from the following table:

| Placeholder | Value |
| --- | --- |
| {DCR\_NAME} | The name you choose for your Data Collection Rule. It must be unique within your workspace. |
| {DCR\_LOCATION} | The region where the resource group containing the DCR is located. |
| {TABLE\_NAME} | The name of the destination table in Log Analytics. Must end with `_CL`. |
| {LOCAL\_PATH\_FILE\_1} *(required)*,{LOCAL\_PATH\_FILE\_2} *(optional)* | Paths and file names of the text files containing the logs you want to collect. These must be on the machine where the Azure Monitor Agent is installed. |
| {WORKSPACE\_RESOURCE\_PATH} | The Azure resource path of your Microsoft Sentinel workspace. |
| {WORKSPACE\_ID} | The GUID of your Microsoft Sentinel workspace. |

### Associate the DCR with the Azure Monitor Agent

If you create the DCR using an ARM template, you still must associate the DCR with the agents that will use it. You can edit the DCR in the Azure portal and select the agents as described in Define VM resources.

---

## Configure the log forwarder to accept logs

If you're collecting logs from an appliance using a log forwarder, configure the syslog daemon on the log forwarder to listen for messages from other machines, and open the necessary local ports.

1. Copy the following command line:

    ```python
    sudo wget -O Forwarder_AMA_installer.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Forwarder_AMA_installer.py&&sudo python Forwarder_AMA_installer.py
    ```
2. Sign in to the log forwarder machine where you just installed the AMA.
3. Paste the command you copied in the last step to launch the installation script. The script configures the `rsyslog` or `syslog-ng` daemon to use the required protocol and restarts the daemon. The script opens port 514 to listen to incoming messages in both UDP and TCP protocols. To change the listening port or protocol configuration, refer to the syslog daemon configuration file according to the daemon type running on the machine:

    - Rsyslog: `/etc/rsyslog.conf`
    - Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`

    If you're using Python 3, and it's not set as the default command on the machine, substitute `python3` for `python` in the pasted command. See Log forwarder prerequisites.

    Note

    To avoid [Full Disk scenarios](/en-us/azure/azure-monitor/agents/azure-monitor-agent-troubleshoot-linux-vm-rsyslog) where the agent can't function, we recommend that you set the `syslog-ng` or `rsyslog` configuration not to store unneeded logs. A Full Disk scenario disrupts the function of the installed AMA. For more information, see [RSyslog](https://docs.rsyslog.com/doc/configuration/actions.html) or [Syslog-ng](https://syslog-ng.github.io/).

## Configure the security device or appliance

To set up your security application or appliance, see [Custom Logs via AMA data connector - Configure data ingestion to Microsoft Sentinel from specific applications](unified-connector-custom-device).

If the product docs don't cover your device, contact the solution provider for help.