---
layout: Conceptual
title: Ingest syslog and CEF messages to Microsoft Sentinel - AMA | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-cef-syslog-ama
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
description: Ingest syslog messages from linux machines and from network and security devices and appliances to Microsoft Sentinel, using data connectors based on the Azure Monitor Agent (AMA).
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.custom: linux-related-content, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: 033e365e-134b-3a3f-084a-c8f05fb7b3c8
document_version_independent_id: 4467d087-0f04-77ed-f3d5-688aba8fce34
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-cef-syslog-ama.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-cef-syslog-ama
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-cef-syslog-ama.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3166ca87-595a-a55f-73e2-4a711fbc291c
---

# Ingest syslog and CEF messages to Microsoft Sentinel - AMA | Microsoft Learn

This article shows you how to use the **Syslog via AMA** and **Common Event Format (CEF) via AMA** connectors to filter and ingest syslog and CEF messages from Linux machines, network devices, and security appliances. Before you begin, make sure you have the required permissions, agents, and log forwarder setup as described in the Prerequisites. To learn more about these data connectors, see [Syslog and Common Event Format (CEF) via AMA connectors for Microsoft Sentinel](cef-syslog-ama-overview).

Note

Container Insights supports automatic collection of syslog events from Linux nodes in your AKS clusters. Learn more in [Syslog collection with Container Insights](/en-us/azure/azure-monitor/containers/container-insights-syslog).

## Prerequisites

Before you begin, review the following Microsoft Sentinel, log forwarder, and machine security prerequisites to ensure you have the resources configured and the appropriate permissions assigned as described in the Microsoft Sentinel prerequisites, Log forwarder prerequisites, and Machine security prerequisites sections.

### Microsoft Sentinel prerequisites

Install the appropriate Microsoft Sentinel solution and make sure you have the permissions to complete the steps in this article.

- Install the appropriate solution from the **Content hub** in Microsoft Sentinel. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).
- Identify which data connector the Microsoft Sentinel solution requires **Syslog via AMA** or **Common Event Format (CEF) via AMA** and whether you need to install the **Syslog** or **Common Event Format** solution. To fulfill this prerequisite,

    - In the **Content hub**, select **Manage** on the installed solution and review the data connector listed.
    - If either **Syslog via AMA** or **Common Event Format (CEF) via AMA** isn't installed with the solution, identify whether you need to install the **Syslog** or **Common Event Format** solution by finding your appliance or device from one of the following articles:

        - [CEF via AMA data connector - Configure specific appliance or device for Microsoft Sentinel data ingestion](unified-connector-cef-device)
        - [Syslog via AMA data connector - Configure specific appliance or device for Microsoft Sentinel data ingestion](unified-connector-syslog-device)

        Then install either the **Syslog** or **Common Event Format** solution from the content hub to get the related AMA data connector.
- Have an Azure account with the following Azure role-based access control (Azure RBAC) roles:

    | Built-in role | Scope | Reason |
    | --- | --- | --- |
    | - [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles/compute#virtual-machine-contributor)- [Azure Connected Machine Resource Administrator](/en-us/azure/role-based-access-control/built-in-roles/management-and-governance#azure-connected-machine-resource-administrator) | - Virtual machines (VM)<br>- Virtual Machine Scale Sets<br>- Azure Arc-enabled servers | To deploy the agent |
    | Any role that includes the action*Microsoft.Resources/deployments/\** | - Subscription<br>- Resource group<br>- Existing data collection rule | To deploy Azure Resource Manager templates |
    | [Monitoring Contributor](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-contributor) | - Subscription<br>- Resource group<br>- Existing data collection rule | To create or edit data collection rules |

### Log forwarder prerequisites

If you're collecting messages from a log forwarder, the following prerequisites apply:

- You must have a designated Linux VM as a log forwarder to collect logs.

    - [Create a Linux VM in the Azure portal](/en-us/azure/virtual-machines/linux/quick-create-portal).
    - [Supported Linux operating systems for Azure Monitor Agent](/en-us/azure/azure-monitor/agents/agents-overview#linux).
- If your log forwarder *isn't* an Azure virtual machine, it must have the Azure Arc [Connected Machine agent](/en-us/azure/azure-arc/servers/overview) installed on it.
- The Linux log forwarder VM must have Python 2.7 or 3 installed. Use the `python --version` or `python3 --version` command to check. If you're using Python 3, make sure it's set as the default command on the machine, or run scripts with the 'python3' command instead of 'python'.
- The log forwarder must have either the `syslog-ng` or `rsyslog` daemon enabled.
- For space requirements for your log forwarder, refer to the [Azure Monitor Agent Performance Benchmark](/en-us/azure/azure-monitor/agents/azure-monitor-agent-performance). You can also review [Designs for accomplishing Microsoft Sentinel scalable ingestion](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/designs-for-accomplishing-microsoft-sentinel-scalable-ingestion/ba-p/3741516).
- Your log sources, security devices, and appliances, must be configured to send their log messages to the log forwarder's syslog daemon instead of to their local syslog daemon.

Note

When deploying the AMA to a Virtual Machine Scale Set (VMSS), you're strongly encouraged to use a load balancer that supports the round-robin method to ensure load distribution across all deployed instances.

### Machine security prerequisites

Configure the machine's security according to your organization's security policy. For example, configure your network to align with your corporate network security policy and change the ports and protocols in the daemon to align with your requirements. To improve your machine security configuration, [secure your VM in Azure](/en-us/azure/virtual-machines/security-policy), or review these [best practices for network security](/en-us/azure/security/fundamentals/network-best-practices).

If your devices are sending syslog and CEF logs over TLS because, for example, your log forwarder is in the cloud, you need to configure the syslog daemon (`rsyslog` or `syslog-ng`) to communicate in TLS. For more information, see:

- [Encrypt Syslog traffic with TLS – rsyslog](https://docs.rsyslog.com/doc/tutorials/tls_cert_summary.html)
- [Encrypt log messages with TLS – syslog-ng](https://support.oneidentity.com/technical-documents/syslog-ng-open-source-edition/3.22/administration-guide/60#TOPIC-1209298)

## Configure the data connector

The setup process for the Syslog via AMA or Common Event Format (CEF) via AMA data connectors includes the following steps:

1. Install the Azure Monitor Agent and create a Data Collection Rule (DCR) by using either of the following methods:
    - [Azure or Defender portal](?tabs=syslog,portal#create-data-collection-rule-dcr)
    - [Azure Monitor Logs Ingestion API](?tabs=syslog,api#install-the-azure-monitor-agent)
2. If you're collecting logs from other machines using a log forwarder, **run the "installation" script** on the log forwarder to configure the syslog daemon to listen for messages from other machines, and to open the necessary local ports.

Select the appropriate tab for instructions.

# [Azure or Defender portal](#tab/portal)
Use the Azure or Defender portal to create a data collection rule (DCR) and install the Azure Monitor Agent on your log forwarder.

### Create data collection rule (DCR)

To get started, open either the **Syslog via AMA** or **Common Event Format (CEF) via AMA** data connector in Microsoft Sentinel and create a data collection rule (DCR).

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Configuration**, select **Data connectors**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Data connectors**.
2. For syslog, type *Syslog* in the **Search** box. From the results, select the **Syslog via AMA** connector.  For CEF, type *CEF* in the **Search** box. From the results, select the **Common Event Format (CEF) via AMA** connector.
3. Select **Open connector page** on the details pane.
4. In the **Configuration** area, select **+Create data collection rule**.

    [![Screenshot showing the Syslog via AMA connector page.](media/connect-cef-ama/syslog-connector-page-create-dcr.png)](media/connect-cef-ama/syslog-connector-page-create-dcr.png#lightbox)

    [![Screenshot showing the CEF via AMA connector page.](media/connect-cef-ama/cef-connector-page-create-dcr.png)](media/connect-cef-ama/cef-connector-page-create-dcr.png#lightbox)
5. In the **Basic** tab:

    - Type a DCR name.
    - Select your subscription.
    - Select the resource group where you want to locate your DCR.

    [![Screenshot showing the DCR details in the Basic tab.](media/connect-cef-ama/dcr-basics-tab.png)](media/connect-cef-ama/dcr-basics-tab.png#lightbox)
6. Select **Next: Resources &gt;**.

### Define VM resources

In the **Resources** tab, select the machines on which you want to install the AMA. For this procedure, select your log forwarder machine. If your log forwarder doesn't appear in the list, it might not have the Azure Connected Machine agent installed.

1. Use the available filters or search box to find your log forwarder VM. Expand a subscription in the list to see its resource groups, and a resource group to see its VMs.
2. Select the log forwarder VM that you want to install the AMA on. The check box appears next to the VM name when you hover over it.

    [![Screenshot showing how to select resources when setting up the DCR.](media/connect-cef-ama/dcr-select-resources.png)](media/connect-cef-ama/dcr-select-resources.png#lightbox)
3. Review your changes and select **Next: Collect &gt;**.

### Select facilities and severities

Be aware that using the same facility for both syslog and CEF messages might result in data ingestion duplication. For more information, see [Data ingestion duplication avoidance](cef-syslog-ama-overview#data-ingestion-duplication-avoidance).

1. In the **Collect** tab, select the minimum log level for each facility. When you select a log level, Microsoft Sentinel collects logs for the selected level and other levels with higher severity. For example, if you select **LOG\_ERR**, Microsoft Sentinel collects logs for the **LOG\_ERR**, **LOG\_CRIT**, **LOG\_ALERT**, and **LOG\_EMERG** levels.

    ![Screenshot showing how to select log levels when setting up the DCR.](media/connect-cef-ama/dcr-log-levels.png)
2. Review your selections and select **Next: Review + create**.

### Review and create the rule

After you complete all the tabs, review what you entered and create the data collection rule.

1. In the **Review and create** tab, select **Create**.

    ![Screenshot showing how to review the configuration of the DCR and create it.](media/connect-cef-ama/dcr-review-create.png)

    The connector installs the Azure Monitor Agent on the machines you selected when creating your DCR.
2. Check the notifications in the Azure portal or Microsoft Defender portal to see when the DCR is created and the agent is installed.
3. Select **Refresh** on the connector page to see the DCR displayed in the list.

# [Logs Ingestion API](#tab/api)
Use the Logs Ingestion API to install the Azure Monitor Agent, create the data collection rule, and associate the rule with your log forwarder.

### Install the Azure Monitor Agent

Follow the appropriate instructions from the Azure Monitor documentation to install the Azure Monitor Agent on your log forwarder. Remember to use the instructions for Linux, not for Windows.

- [Install the AMA using PowerShell](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-powershell)
- [Install the AMA using the Azure CLI](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-cli)
- [Install the AMA using an Azure Resource Manager template](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-resource-manager)

You can create Data Collection Rules (DCRs) using the [Azure Monitor Logs Ingestion API](/en-us/rest/api/monitor/data-collection-rules). For more information, see [Data collection rules in Azure Monitor](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview).

### Create the data collection rule

Create a JSON file for the data collection rule, create an API request, and send the request.

1. Prepare a DCR file in JSON format. The contents of the DCR JSON file are the request body in your API request.

    For an example, see [Syslog/CEF DCR creation request body](api-dcr-reference#syslogcef-dcr-creation-request-body). To collect syslog and CEF messages in the same data collection rule, see the example Syslog and CEF streams in the same DCR.

    - Verify that the `streams` field is set to `Microsoft-Syslog` for syslog messages, or to `Microsoft-CommonSecurityLog` for CEF messages.
    - Add the filter and facility log levels in the `facilityNames` and `logLevels` parameters. See Examples of facilities and log levels sections.
2. Create an API request in a REST API client of your choosing.

    1. For the **request URL and header**, copy the following request URL and header.

        ```http
        PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/dataCollectionRules/{dataCollectionRuleName}?api-version=2022-06-01
        ```

        - Substitute the appropriate values for the `{subscriptionId}` and `{resourceGroupName}` placeholders.
        - Enter a name of your choice for the DCR in place of the `{dataCollectionRuleName}` placeholder.
    2. For the **request body**, copy and paste the contents of the DCR JSON file that you prepared earlier in this procedure into the request body.
3. Send the request.

    For an example of the response that you should receive, see [Syslog/CEF DCR creation response](api-dcr-reference#syslogcef-dcr-creation-response).

### Associate the DCR with the log forwarder

Now you need to create a DCR Association (DCRA) that ties the DCR to the VM resource that hosts your log forwarder.

1. Create an API request in a REST API client of your choosing.
2. For the **request URL and header**, copy the following request URL and the header.

    ```http
    PUT 
    https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{virtualMachineName}/providers/Microsoft.Insights/dataCollectionRuleAssociations/{dataCollectionRuleAssociationName}?api-version=2022-06-01
    ```

    - Substitute the appropriate values for the `{subscriptionId}`, `{resourceGroupName}`, and `{virtualMachineName}` placeholders.
    - Enter a name of your choice for the DCR in place of the `{dataCollectionRuleAssociationName}` placeholder.
3. For the **request body**, copy the following request body.

    ```json
    {
      "properties": {
        "dataCollectionRuleId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/dataCollectionRules/{dataCollectionRuleName}"
      }
    }
    ```

    - Substitute the appropriate values for the `{subscriptionId}` and `{resourceGroupName}` placeholders.
    - Enter a name of your choice for the DCR in place of the `{dataCollectionRuleName}` placeholder.
4. Send the request.

### Examples of facilities and log levels sections

Review these examples of the facilities and log levels settings. The `name` field includes the filter name.

For CEF message ingestion, the value for `"streams"` should be `"Microsoft-CommonSecurityLog"` instead of `"Microsoft-Syslog"`.

This example collects events from the `cron`, `daemon`, `local0`, `local3` and `uucp` facilities, with the `Warning`, `Error`, `Critical`, `Alert`, and `Emergency` log levels:

```json
    "dataSources": {
      "syslog": [
        {
        "name": "SyslogStream0",
        "streams": [
          "Microsoft-Syslog"
        ],
        "facilityNames": [ 
          "cron",
          "daemon",
          "local0",
          "local3", 
          "uucp"
        ],
        "logLevels": [ 
          "Warning", 
          "Error", 
          "Critical", 
          "Alert", 
          "Emergency"
        ]
      }
    ]
  }
```

### Syslog and CEF streams in the same DCR

This example shows how you can collect syslog and CEF messages in the same DCR.

The DCR collects CEF event messages for:

- The `authpriv` and `mark` facilities with the `Info`, `Notice`, `Warning`, `Error`, `Critical`, `Alert`, and `Emergency` log levels
- The `daemon` facility with the `Warning`, `Error`, `Critical`, `Alert`, and `Emergency` log levels

It collects syslog event messages for:

- The `kern`, `local0`, `local5`, and `news` facilities with the `Critical`, `Alert`, and `Emergency` log levels
- The `mail` and `uucp` facilities with the `Emergency` log level

```json
    "dataSources": {
      "syslog": [
        {
          "name": "CEFStream1",
          "streams": [ 
            "Microsoft-CommonSecurityLog"
          ],
          "facilityNames": [ 
            "authpriv", 
            "mark"
          ],
          "logLevels": [
            "Info",
            "Notice", 
            "Warning", 
            "Error", 
            "Critical", 
            "Alert", 
            "Emergency"
          ]
        },
        {
          "name": "CEFStream2",
          "streams": [ 
            "Microsoft-CommonSecurityLog"
          ],
          "facilityNames": [ 
            "daemon"
          ],
          "logLevels": [ 
            "Warning", 
            "Error", 
            "Critical", 
            "Alert", 
            "Emergency"
          ]
        },
        {
          "name": "SyslogStream3",
          "streams": [ 
            "Microsoft-Syslog"
          ],
          "facilityNames": [ 
            "kern",
            "local0",
            "local5", 
            "news"
          ],
          "logLevels": [ 
            "Critical", 
            "Alert", 
            "Emergency"
          ]
        },
        {
          "name": "SyslogStream4",
          "streams": [ 
            "Microsoft-Syslog"
          ],
          "facilityNames": [ 
            "mail",
            "uucp"
          ],
          "logLevels": [ 
            "Emergency"
          ]
        }
      ]
    }

```

---

## Run the "installation" script

If you're using a log forwarder, configure the syslog daemon to listen for messages from other machines, and open the necessary local ports.

1. From the connector page, copy the command line that appears under **Run the following command to install and apply the CEF collector:**.

    ![Screenshot of command line on connector page.](media/connect-cef-ama/run-install-script.png)

    Or copy it from here:

    ```python
    sudo wget -O Forwarder_AMA_installer.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Forwarder_AMA_installer.py&&sudo python Forwarder_AMA_installer.py
    ```
2. Sign in to the log forwarder machine where the AMA is installed.
3. Paste the installation command you copied from the connector page to launch the installation script. The script configures the `rsyslog` or `syslog-ng` daemon to use the required protocol and restarts the daemon. The script opens port 514 to listen to incoming messages in both UDP and TCP protocols. To change this setting, refer to the syslog daemon configuration file according to the daemon type running on the machine:

    - Rsyslog: `/etc/rsyslog.conf`
    - Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`

    If you're using Python 3, and it's not set as the default command on the machine, substitute `python3` for `python` in the pasted command. See Log forwarder prerequisites.

    Note

    To avoid [Full Disk scenarios](/en-us/azure/azure-monitor/agents/azure-monitor-agent-troubleshoot-linux-vm-rsyslog) where the agent can't function, we recommend that you set the `syslog-ng` or `rsyslog` configuration not to store unneeded logs. A Full Disk scenario disrupts the function of the installed AMA. For more information, see [RSyslog](https://docs.rsyslog.com/doc/configuration/actions.html) or [Syslog-ng](https://syslog-ng.github.io/).
4. Check the service status.

    Check the AMA service status on your log forwarder:

    ```bash
    sudo systemctl status azuremonitoragent.service
    ```

    Check the rsyslog service status:

    ```bash
    sudo systemctl status rsyslog.service
    ```

    For syslog-ng environments, check:

    ```bash
    sudo systemctl status syslog-ng.service
    ```

## Configure the security device or appliance

For instructions to configure your security device or appliance, see one of the following articles:

- [CEF via AMA data connector - Configure specific appliances and devices for Microsoft Sentinel data ingestion](unified-connector-cef-device)
- [Syslog via AMA data connector - Configure specific appliances and devices for Microsoft Sentinel data ingestion](unified-connector-syslog-device)

For more information about your appliance or device, contact the solution provider.

## Test the connector

Verify that log messages from your Linux machine or security devices and appliances are ingested into Microsoft Sentinel.

1. To validate that the syslog daemon is listening on the required UDP port and that the AMA is ready to receive logs on the Linux forwarder, run the following command to display active listeners and their associated ports:

    ```bash
     netstat -lnptv
    ```

    You should see the `rsyslog` or `syslog-ng` daemon listening on port 514.
2. To capture messages sent from a logger or a connected device, run this command in the background:

    ```bash
    sudo tcpdump -i any port 514 or 28330 -A -vv &
    ```
3. After you complete the validation, stop `tcpdump`. Type `fg`, and then select Ctrl+C.

### Send test messages

To send demo messages, complete one of the following steps:

1. Use the `nc` netcat utility. In this example, the utility reads data posted through the `echo` command with the newline switch turned off. The utility then writes the data to UDP port `514` on the localhost with no timeout. To execute the netcat utility, you might need to install another package.

    ```
    echo -n "<164>CEF:0|Mock-test|MOCK|common=event-format-test|end|TRAFFIC|1|rt=$common=event-formatted-receive_time" | nc -u -w0 localhost 514
    ```
2. Use the `logger` command. This example writes the message to the `local 4` facility, at severity level `Warning`, to port `514`, on the local host, in the CEF RFC format. The `-t` and `--rfc3164` flags are used to comply with the expected RFC format.

    ```
    logger -p local4.warn -P 514 -n 127.0.0.1 --rfc3164 -t CEF "0|Mock-test|MOCK|common=event-format-test|end|TRAFFIC|rt=$common=event-formatted-receive_time"
    ```

    Test Cisco ASA ingestion using the following command:

    ```bash
    echo -n "<164>%ASA-7-106010: Deny inbound TCP src inet:1.1.1.1 dst inet:2.2.2.2" | nc -u -w0 localhost 514
    ```

    After you run these commands, messages arrive on port 514 and forward to port 28330.
3. After sending test messages, query your Log Analytics workspace. Logs can take up to 20 minutes to appear in your workspace.

For CEF logs:

```kusto
CommonSecurityLog
| where TimeGenerated > ago(1d)
| where DeviceProduct == "MOCK"
```

For Cisco ASA logs:

```kusto
CommonSecurityLog
| where TimeGenerated > ago(1d)
| where DeviceVendor == "Cisco"
| where DeviceProduct == "ASA"
```

## Additional troubleshooting

If you don't see traffic on port 514 or your test messages aren't ingested, see [Troubleshoot Syslog and CEF via AMA connectors for Microsoft Sentinel](cef-syslog-ama-troubleshooting) to troubleshoot.