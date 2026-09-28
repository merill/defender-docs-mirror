---
layout: Conceptual
title: CEF via AMA connector - Configure appliances and devices | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/unified-connector-cef-device
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
description: Learn how to configure specific devices that use the Common Event Format (CEF) via AMA data connector for Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-27T00:00:00.0000000Z
locale: en-us
document_id: 3b913de7-f734-b708-38ff-553db1829d37
document_version_independent_id: f6d32cda-6e12-ed56-3b10-1e0b2966c2b3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/unified-connector-cef-device.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/unified-connector-cef-device
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/unified-connector-cef-device.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 2ca2b478-ca15-569a-bd93-22866facd086
---

# CEF via AMA connector - Configure appliances and devices | Microsoft Learn

Log collection from many security appliances and devices is supported by the **Common Event Format (CEF) via AMA** data connector in Microsoft Sentinel. This article lists provider-supplied installation instructions for specific security appliances and devices that use this data connector. Contact the provider for updates, more information, or where information is unavailable for your security appliance or device.

To ingest data to your Log Analytics workspace for Microsoft Sentinel, complete the steps in [Ingest syslog and CEF messages to Microsoft Sentinel with the Azure Monitor Agent](connect-cef-syslog-ama). Those steps include the installation of the **Common Event Format (CEF) via AMA** data connector in Microsoft Sentinel. After the connector is installed, use the instructions appropriate to your device, shown later in this article, to complete the setup.

For more information about the related Microsoft Sentinel solution for each of these appliances or devices, search the [Azure Marketplace](https://azuremarketplace.microsoft.com/) for the **Product Type** &gt; **Solution Templates** or review the solution from the **Content hub** in Microsoft Sentinel.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## AI Analyst Darktrace

Configure Darktrace to forward syslog messages in CEF format to your Azure workspace via the syslog agent.

1. Within the Darktrace Threat Visualizer, navigate to the **System Config** page in the main menu under **Admin**.
2. From the left-hand menu, select **Modules** and choose Microsoft Sentinel from the available **Workflow Integrations**.
3. Locate Microsoft Sentinel syslog CEF and select **New** to reveal the configuration settings, unless already exposed.
4. In the **Server** configuration field, enter the location of the log forwarder and optionally modify the communication port. Ensure that the port selected is set to 514 and is allowed by any intermediary firewalls.
5. Configure any alert thresholds, time offsets or other settings as required.
6. Review any other configuration options you might wish to enable that alter the syslog syntax.
7. Enable **Send Alerts** and save your changes.

## Akamai Security Events

[Follow these steps](https://developer.akamai.com/tools/integrations/siem) to configure Akamai CEF connector to send syslog messages in CEF format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machine's IP address.

## AristaAwakeSecurity

Complete the following steps to forward Awake Adversarial Model match results to a CEF collector listening on TCP port 514 at IP **192.168.0.1**:

1. Navigate to the **Detection Management Skills** page in the Awake UI.
2. Select **+ Add New Skill**.
3. Set **Expression** to `integrations.cef.tcp { destination: "192.168.0.1", port: 514, secure: false, severity: Warning }`
4. Set **Title** to a descriptive name like, *Forward Awake Adversarial Model match result to Microsoft Sentinel*.
5. Set **Reference Identifier** to something easily discoverable like, *integrations.cef.sentinel-forwarder*.
6. Select **Save**.

Within a few minutes of saving the definition and other fields, the system begins to send new model match results to the CEF events collector as they're detected.

For more information, see the **Adding a Security Information and Event Management Push Integration** page from the **Help Documentation** in the Awake UI.

## Aruba ClearPass

Configure Aruba ClearPass to forward syslog messages in CEF format to your Microsoft Sentinel workspace via the syslog agent.

1. [Follow these instructions](https://www.arubanetworks.com/techdocs/ClearPass/6.7/PolicyManager/Content/CPPM_UserGuide/Admin/syslogExportFilters_add_syslog_filter_general.htm) to configure the Aruba ClearPass to forward syslog.
2. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

## Barracuda WAF

The Barracuda Web Application Firewall can integrate with and export logs directly to Microsoft Sentinel via the Azure Monitoring Agent (AMA).​

1. Go to [Barracuda WAF configuration](https://aka.ms/asi-barracuda-connector), and follow the instructions, using the following parameters to set up the connection.
2. Web Firewall logs facility: Go to the advanced settings for your workspace and on the **Data** &gt; **Syslog** tabs. Make sure that the facility exists.​

Notice that the data from all regions are stored in the selected workspace.

## Broadcom SymantecDLP

Configure Symantec DLP to forward syslog messages in CEF format to your Microsoft Sentinel workspace via the syslog agent.

1. [Follow these instructions](https://knowledge.broadcom.com/external/article/159509/generating-syslog-messages-from-data-los.html) to configure the Symantec DLP to forward syslog
2. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

## Cisco Firepower EStreamer

Install and configure the Firepower eNcore eStreamer client. For more information, see the full install [guide](https://www.cisco.com/c/en/us/td/docs/security/firepower/670/api/eStreamer_enCore/eStreamereNcoreSentinelOperationsGuide_409.html).

## CiscoSEG

Complete the following steps to configure Cisco Secure Email Gateway to forward logs via syslog:

1. Configure [Log Subscription](https://www.cisco.com/c/en/us/td/docs/security/esa/esa14-0/user_guide/b_ESA_Admin_Guide_14-0/b_ESA_Admin_Guide_12_1_chapter_0100111.html#con_1134718).
2. Select **Consolidated Event Logs** in Log Type field.

## Citrix Web App Firewall

Configure Citrix WAF to send syslog messages in CEF format to the proxy machine.

- Find guides to configure WAF and CEF logs from [Citrix Support](https://support.citrix.com/).
- Follow [this guide](https://docs.citrix.com/en-us/citrix-adc/13/system/audit-logging/configuring-audit-logging.html) to forward the logs to proxy. Make sure you to send the logs to port 514 TCP on the Linux machine's IP address.

## Claroty

Configure log forwarding using CEF.

1. Navigate to the **Syslog** section of the Configuration menu.
2. Select **+Add**.
3. In the **Add New Syslog Dialog** specify **Remote Server IP**, **Port**, **Protocol**.
4. Select **Message Format** - **CEF**.
5. Choose **Save** to exit the **Add Syslog dialog**.

## Contrast Protect

Configure the Contrast Protect agent to forward events to syslog as described here: https://docs.contrastsecurity.com/en/output-to-syslog.html. Generate some attack events for your application.

## CrowdStrike Falcon

Deploy the CrowdStrike Falcon SIEM Collector to forward syslog messages in CEF format to your Microsoft Sentinel workspace via the syslog agent.

1. [Follow these instructions](https://www.crowdstrike.com/blog/tech-center/integrate-with-your-siem/) to deploy the **SIEM Collector** and forward syslog.
2. Use the IP address or hostname for the Linux device with the Linux agent installed as the Destination IP address.

## CyberArk Enterprise Password Vault (EPV) Events

On the EPV, configure the dbparm.ini to send syslog messages in CEF format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machines IP address.

## Delinea Secret Server

Set your security solution to send syslog messages in CEF format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machine's IP address.

## ExtraHop Reveal(x)

Set your security solution to send syslog messages in CEF format to the proxy machine. Make sure to send the logs to port 514 TCP on the machine IP address.

1. Follow the directions to install the [ExtraHop Detection SIEM Connector bundle](https://learn.extrahop.com/) on your Reveal(x) system. The **SIEM Connector** is required for this integration.
2. Enable the trigger for **ExtraHop Detection SIEM Connector - CEF**.
3. Update the trigger with the ODS syslog targets you created.

The Reveal(x) system formats syslog messages in Common Event Format (CEF) and then sends data to Microsoft Sentinel.

## F5 Networks

Configure F5 to forward syslog messages in CEF format to your Microsoft Sentinel workspace via the syslog agent.

Go to [F5 Configuring Application Security Event Logging](https://aka.ms/asi-syslog-f5-forwarding), follow the instructions to set up remote logging, using the following guidelines:

1. Set the **Remote storage type** to **CEF**.
2. Set the **Protocol setting** to **UDP**.
3. Set the **IP address** to the syslog server IP address.
4. Set the **port number** to **514**, or the port your agent uses.
5. Set the **facility** to the one that you configured in the syslog agent. By default, the agent sets this value to **local4**.
6. You can set the **Maximum Query String Size** to be the same as you configured.

## FireEye Network Security

Complete the following steps to send data using CEF:

1. Sign into the FireEye appliance with an administrator account.
2. Select **Settings**.
3. Select **Notifications**. Select **rsyslog**.
4. Check the **Event type** check box.
5. Make sure Rsyslog settings are:

    - Default format: **CEF**
    - Default delivery: **Per event**
    - Default send as: **Alert**

## Forcepoint CASB

Set your security solution to send syslog messages in CEF format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machine's IP address.

## Forcepoint CSG

The integration is made available with two implementations options:

1. Uses docker images where the integration component is already installed with all necessary dependencies. Follow the instructions provided in the [Integration Guide](https://frcpnt.com/csg-sentinel).
2. Requires the manual deployment of the integration component inside a clean Linux machine. Follow the instructions provided in the [Integration Guide](https://frcpnt.com/csg-sentinel).

## Forcepoint NGFW

Set your security solution to send syslog messages in CEF format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machine's IP address.

## ForgeRock Common Audit for CEF

In ForgeRock, install and configure this Common Audit (CAUD) for Microsoft Sentinel per the documentation at https://github.com/javaservlets/SentinelAuditEventHandler. Next, in Azure, follow the steps to configure the CEF via AMA data connector.

## Fortinet

Set your Fortinet to send Syslog messages in CEF format to the proxy machine. Make sure you send the logs to port 514 TCP on the machine's IP address.

Copy the CLI commands below and:

- Replace "server &lt;ip address&gt;" with the Syslog agent's IP address.
- Set the "&lt;facility\_name&gt;" to use the facility you configured in the Syslog agent (by default, the agent sets this to local4).
- Set the Syslog port to 514, the port your agent uses.
- To enable CEF format in early FortiOS versions, you may need to run the command "set csv disable".For more information, go to the [Fortinet Document Library](https://aka.ms/asi-syslog-fortinet-fortinetdocumentlibrary), choose your version, and use the "Handbook" and "Log Message Reference" PDFs.

[Learn more &gt;](https://aka.ms/CEF-Fortinet)

Set up the connection using the CLI to run the following commands: `config log syslogd setting/n    set status enable/nset format cef/nset port 514/nset server <ip_address_of_Receiver>/nend`

## iboss

Set your Threat Console to send syslog messages in CEF format to your Azure workspace. Make note of your **Workspace ID** and **Primary Key** within your Log Analytics workspace. Select the workspace from the Log Analytics workspaces menu in the Azure portal. Then select **Agents management** in the **Settings** section.

1. Navigate to **Reporting & Analytics** inside your iboss Console.
2. Select **Log Forwarding** &gt; **Forward From Reporter**.
3. Select **Actions** &gt; **Add Service**.
4. Toggle to Microsoft Sentinel as a **Service Type** and input your **Workspace ID/Primary Key** along with other criteria. If a dedicated proxy Linux machine was configured, toggle to **Syslog** as a **Service Type** and configure the settings to point to your dedicated proxy Linux machine.
5. Wait one to two minutes for the setup to complete.
6. Select your Microsoft Sentinel service and verify the Microsoft Sentinel setup status is successful. If a dedicated proxy Linux machine is configured, you might validate your connection.

## Illumio Core

Configure event format.

1. From the PCE web console menu, choose **Settings &gt; Event Settings** to view your current settings.
2. Select **Edit** to change the settings.
3. Set **Event Format** to CEF.
4. (Optional) Configure **Event Severity** and **Retention Period**.

Configure event forwarding to an external syslog server.

1. From the PCE web console menu, choose **Settings** &gt; **Event Settings**.
2. Select **Add**.
3. Select **Add Repository**.
4. Complete the **Add Repository** dialog.
5. Select **OK** to save the event forwarding configuration.

## Illusive Platform

1. Set your security solution to send syslog messages in CEF format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machine's IP address.
2. Sign into the Illusive Console, and navigate to **Settings** &gt; **Reporting**.
3. Find **Syslog Servers**.
4. Supply the following information:

    - Host name: *Linux Syslog agent IP address or FQDN host name*
    - Port: *514*
    - Protocol: *TCP*
    - Audit messages: *Send audit messages to server*
5. To add the syslog server, select **Add**.

For more information about how to add a new syslog server in the Illusive platform, find the Illusive Networks Admin Guide in here: https://support.illusivenetworks.com/hc/en-us/sections/360002292119-Documentation-by-Version

## Imperva WAF Gateway

This connector requires an **Action Interface** and **Action Set** to be created on the Imperva SecureSphere MX. [Follow the steps](https://community.imperva.com/blogs/craig-burlingame1/2020/11/13/steps-for-enabling-imperva-waf-gateway-alert) to create the requirements.

1. Create a new **Action Interface** that contains the required parameters to send WAF alerts to Microsoft Sentinel.
2. Create a new **Action Set** that uses the **Action Interface** configured.
3. Apply the Action Set to any security policies you wish to have alerts for sent to Microsoft Sentinel.

## Infoblox Cloud Data Connector

Complete the following steps to configure the Infoblox CDC to send BloxOne data to Microsoft Sentinel via the Linux syslog agent.

1. Navigate to **Manage** &gt; **Data Connector**.
2. Select the **Destination Configuration** tab at the top.
3. Select **Create &gt; Syslog**.
    - **Name**: Give the new Destination a meaningful name, such as *Microsoft-Sentinel-Destination*.
    - **Description**: Optionally give it a meaningful description.
    - **State**: Set the state to **Enabled**.
    - **Format**: Set the format to **CEF**.
    - **FQDN/IP**: Enter the IP address of the Linux device on which the Linux agent is installed.
    - **Port**: Leave the port number at **514**.
    - **Protocol**: Select desired protocol and CA certificate if applicable.
    - Select **Save & Close**.
4. Select the **Traffic Flow Configuration** tab at the top.
5. Select **Create**.
    - **Name**: Give the new Traffic Flow a meaningful name, such as *Microsoft-Sentinel-Flow*.
    - **Description**: Optionally give it a meaningful description.
    - **State**: Set the state to **Enabled**.
    - Expand the **Service Instance**section.
        - **Service Instance**: Select your desired Service Instance for which the Data Connector service is enabled.
    - Expand the **Source Configuration**section.
        - **Source**: Select **BloxOne Cloud Source**.
        - Select all desired **log types**you wish to collect. Currently supported log types are:
            - Threat Defense Query/Response Log
            - Threat Defense Threat Feeds Hits Log
            - DDI Query/Response Log
            - DDI DHCP Lease Log
    - Expand the **Destination Configuration**section.
        - Select the **Destination** you created.
    - Select **Save & Close**.
6. Allow the configuration some time to activate.

## Infoblox SOC Insights

Complete the following steps to configure the Infoblox CDC to send BloxOne data to Microsoft Sentinel via the Linux syslog agent.

1. Navigate to **Manage &gt; Data Connector**.
2. Select the **Destination Configuration** tab at the top.
3. Select **Create &gt; Syslog**.
    - **Name**: Give the new Destination a meaningful name, such as *Microsoft-Sentinel-Destination*.
    - **Description**: Optionally give it a meaningful description.
    - **State**: Set the state to **Enabled**.
    - **Format**: Set the format to **CEF**.
    - **FQDN/IP**: Enter the IP address of the Linux device on which the Linux agent is installed.
    - **Port**: Leave the port number at **514**.
    - **Protocol**: Select desired protocol and CA certificate if applicable.
    - Select **Save & Close**.
4. Select the **Traffic Flow Configuration** tab at the top.
5. Select **Create**.
    - **Name**: Give the new Traffic Flow a meaningful name, such as *Microsoft-Sentinel-Flow*.
    - **Description**: Optionally give it a meaningful **description**.
    - **State**: Set the state to **Enabled**.
    - Expand the **Service Instance**section.
        - **Service Instance**: Select your desired service instance for which the data connector service is enabled.
    - Expand the **Source Configuration**section.
        - **Source**: Select **BloxOne Cloud Source**.
        - Select the **Internal Notifications** Log Type.
    - Expand the **Destination Configuration**section.
        - Select the **Destination** you created.
    - Select **Save & Close**.
6. Allow the configuration some time to activate.

## KasperskySecurityCenter

[Follow the instructions](https://support.kaspersky.com/KSC/13/en-US/89277.htm) to configure event export from Kaspersky Security Center.

## Morphisec

Set your security solution to send syslog messages in CEF format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machine's IP address.

## Netwrix Auditor

[Follow the instructions](https://www.netwrix.com/download/QuickStart/Netwrix_Auditor_Add-on_for_HPE_ArcSight_Quick_Start_Guide.pdf) to configure event export from Netwrix Auditor.

## NozomiNetworks

Complete the following steps to configure Nozomi Networks device to send alerts, audit, and health logs via syslog in CEF format:

1. Sign in to the Guardian console.
2. Navigate to **Administration** &gt; **Data Integration**.
3. Select **+Add**.
4. Select the **Common Event Format (CEF)** from the drop-down.
5. Create **New Endpoint** using the appropriate host information.
6. Enable **Alerts**, **Audit Logs**, and **Health Logs** for sending.

## Onapsis Platform

Refer to the Onapsis in-product help to set up log forwarding to the syslog agent.

1. Go to **Setup** &gt; **Third-party integrations** &gt; **Defend Alarms** and follow the instructions for Microsoft Sentinel.
2. Make sure your Onapsis Console can reach the proxy machine where the agent is installed. The logs should be sent to port 514 using TCP.

## OSSEC

[Follow these steps](https://www.ossec.net/docs/docs/manual/output/syslog-output.html) to configure OSSEC sending alerts via syslog.

## Palo Alto - XDR (Cortex)

Configure Palo Alto XDR (Cortex) to forward messages in CEF format to your Microsoft Sentinel workspace via the syslog agent.

1. Go to **Cortex Settings and Configurations**.
2. Select to add **New Server** under **External Applications**.
3. Then specify the name and give the public IP of your syslog server in **Destination**.
4. Give **Port number** as 514.
5. From **Facility** field, select **FAC\_SYSLOG** from dropdown.
6. Select **Protocol** as **UDP**.
7. Select **Create**.

## PaloAlto-PAN-OS

Configure Palo Alto Networks to forward syslog messages in CEF format to your Microsoft Sentinel workspace via the syslog agent.

1. Go to [configure Palo Alto Networks NGFW for sending CEF events](https://aka.ms/sentinel-paloaltonetworks-readme).
2. Go to [Palo Alto CEF Configuration](https://aka.ms/asi-syslog-paloalto-forwarding) and Palo Alto [Configure Syslog Monitoring](https://aka.ms/asi-syslog-paloalto-configure) steps 2, 3, choose your version, and follow the instructions using the following guidelines:

    1. Set the **Syslog server format** to **BSD**.
    2. Copy the text to an editor and remove any characters that might break the log format before pasting it. The copy/paste operations from the PDF might change the text and insert random characters.

[Learn more](https://aka.ms/CEFPaloAlto)

## PaloAltoCDL

[Follow the instructions](https://docs.paloaltonetworks.com/cortex/cortex-data-lake/cortex-data-lake-getting-started/get-started-with-log-forwarding-app/forward-logs-from-logging-service-to-syslog-server.html) to configure logs forwarding from Cortex Data Lake to a syslog Server.

## PingFederate

[Follow these steps](https://docs.pingidentity.com/) to configure PingFederate sending audit log via syslog in CEF format.

## RidgeSecurity

Configure the RidgeBot to forward events to syslog server as described [here](https://portal.ridgesecurity.ai/downloadurl/89x72912). Generate some attack events for your application.

## SonicWall Firewall

Set your SonicWall Firewall to send syslog messages in CEF format to the proxy machine. Make sure you send the logs to port 514 TCP on the machine's IP address.

Follow instructions. Then Make sure you select local use 4 as the facility. Then select ArcSight as the syslog format.

## Trend Micro Apex One

[Follow these steps](https://docs.trendmicro.com/en-us/enterprise/trend-micro-apex-central-2019-online-help/detections/logs_001/syslog-forwarding.aspx) to configure Apex Central sending alerts via syslog. While configuring, on step 6, select the log format **CEF**.

## Trend Micro Deep Security

Set your security solution to send syslog messages in CEF format to the proxy machine. Make sure to send the logs to port 514 TCP on the machine's IP address.

1. Forward Trend Micro Deep Security events to the syslog agent.
2. Define a new syslog Configuration that uses the CEF format by referencing [this knowledge article](https://aka.ms/Sentinel-trendmicro-kblink) for additional information.
3. Configure the **Deep Security Manager** to use this new configuration to forward events to the syslog agent using [these instructions](https://aka.ms/Sentinel-trendMicro-connectorInstructions).
4. Make sure to save the [TrendMicroDeepSecurity](https://aka.ms/TrendMicroDeepSecurityFunction) function so that it queries the Trend Micro Deep Security data properly.

## Trend Micro TippingPoint

Set your TippingPoint SMS to send syslog messages in ArcSight CEF Format v4.2 format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machine's IP address.

## vArmour Application Controller

Send syslog messages in CEF format to the proxy machine. Make sure you to send the logs to port 514 TCP on the machine's IP address.

## Vectra AI Detect

Configure Vectra (X Series) Agent to forward syslog messages in CEF format to your Microsoft Sentinel workspace via the syslog agent.

From the Vectra UI, navigate to Settings &gt; Notifications and Edit syslog configuration. Follow below instructions to set up the connection:

1. Add a new Destination (which is the host where the Microsoft Sentinel syslog agent is running).
2. Set the **Port** as *514*.
3. Set the **Protocol** as *UDP*.
4. Set the **format** to *CEF*.
5. Set **Log types**. Select all log types available.
6. Select on **Save**.
7. Select the **Test** button to send some test events.

For more information, see the Cognito Detect Syslog Guide, which can be downloaded from the resource page in Detect UI.

## Votiro

Set Votiro Endpoints to send syslog messages in CEF format to the Forwarder machine. Make sure you to send the logs to port 514 TCP on the Forwarder machine's IP address.

## WireX Network Forensics Platform

Contact WireX support (https://wirexsystems.com/contact-us/) in order to configure your NFP solution to send syslog messages in CEF format to the proxy machine. Make sure that they central manager can send the logs to port 514 TCP on the machine's IP address.

## WithSecure Elements via Connector

Connect your WithSecure Elements Connector appliance to Microsoft Sentinel. The WithSecure Elements Connector data connector allows you to easily connect your WithSecure Elements logs with Microsoft Sentinel, to view dashboards, create custom alerts, and improve investigation.

Note

Data is stored in the geographic location of the workspace on which you are running Microsoft Sentinel.

Configure With Secure Elements Connector to forward syslog messages in CEF format to your Log Analytics workspace via the syslog agent.

1. Select or create a Linux machine for Microsoft Sentinel to use as the proxy between your WithSecurity solution and Microsoft Sentinel. The machine can be an on-premises environment, Microsoft Azure, or other cloud based environment. Linux needs to have `syslog-ng` and `python`/`python3` installed.
2. Install the Azure Monitoring Agent (AMA) on your Linux machine and configure the machine to listen on the necessary port and forward messages to your Microsoft Sentinel workspace. The CEF collector collects CEF messages on port 514 TCP. You must have elevated permissions (sudo) on your machine.
3. Go to **EPP** in WithSecure Elements Portal. Then navigate to **Downloads**. In **Elements Connector** section, select **Create subscription key**. You can check your subscription key in **Subscriptions**.
4. In **Downloads** in WithSecure Elements **Connector** section, select the correct installer and download it.
5. When in EPP, open account settings from the top right hand corner. Then select **Get management API key**. If the key was created earlier, it can be read there as well.
6. To install Elements Connector, follow [Elements Connector Docs](https://help.f-secure.com/product.html#business/connector/latest/en/concept_BA55FDB13ABA44A8B16E9421713F4913-latest-en).
7. If API access isn't configured during installation, follow [Configuring API access for Elements Connector](https://help.f-secure.com/product.html#business/connector/latest/en/task_F657F4D0F2144CD5913EE510E155E234-latest-en).
8. Go to EPP, then **Profiles**, then use **For Connector** from where you can see the connector profiles. Create a new profile (or edit an existing not read-only profile). In **Event forwarding**, enable it. Set SIEM system address: **127.0.0.1:514**. Set format to **Common Event Format**. Protocol is **TCP**. Save profile and assign it to **Elements Connector** in **Devices** tab.
9. To use the relevant schema in Log Analytics for the WithSecure Elements Connector, search for **CommonSecurityLog**.
10. Continue with [validating your CEF connectivity](/en-us/azure/sentinel/troubleshooting-cef-syslog?tabs=rsyslog#validate-cef-connectivity).

## Zscaler

Set Zscaler product to send syslog messages in CEF format to your syslog agent. Make sure you to send the logs on port 514 TCP.

For more information, see [Zscaler Microsoft Sentinel integration guide](https://aka.ms/ZscalerCEFInstructions).