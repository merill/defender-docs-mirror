---
layout: Conceptual
title: Syslog via AMA connector - configure appliances and devices | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/unified-connector-syslog-device
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
description: Learn how to configure specific appliances and devices that use the Syslog via AMA data connector for Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-27T00:00:00.0000000Z
locale: en-us
document_id: 075ab9ca-73dc-3cdc-1767-e47e23b57ad8
document_version_independent_id: 32436592-fdab-7af3-6fee-0648c09c541f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/unified-connector-syslog-device.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/unified-connector-syslog-device
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/unified-connector-syslog-device.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 407ce5fc-1f27-9fe6-2ac5-1bf105af4547
---

# Syslog via AMA connector - configure appliances and devices | Microsoft Learn

The **Syslog via AMA** data connector in Microsoft Sentinel collects logs from many security appliances and devices. This article lists provider-supplied installation instructions for specific security appliances and devices that use this data connector. Contact the provider for updates, more information, or where information is unavailable for your security appliance or device.

To forward data to your Log Analytics workspace for Microsoft Sentinel, complete the steps in [Ingest syslog and CEF messages to Microsoft Sentinel with the Azure Monitor Agent](connect-cef-syslog-ama). As you complete those steps, install the **Syslog via AMA** data connector in Microsoft Sentinel. Then, use the appropriate provider's instructions in this article to complete the setup.

For more information about the related Microsoft Sentinel solution for each of these appliances or devices, search the [Azure Marketplace](https://azuremarketplace.microsoft.com/) for the **Product Type** &gt; **Solution Templates** or review the solution from the **Content hub** in Microsoft Sentinel.

Important

Solutions provided by third-party vendors might still reference a deprecated **Log Analytics agent** connector. These connectors are not supported for new deployments. You can continue to use the same solutions with the **Syslog via AMA** data connector instead.

## Barracuda CloudGen Firewall

[Follow instructions](https://aka.ms/sentinel-barracudacloudfirewall-connector) to configure syslog streaming. Use the IP address or hostname for the Linux machine with the Microsoft Sentinel agent installed for the **Destination IP** address.

## Cisco Application Centric Infrastructure (ACI)

Configure Cisco ACI system to send logs via syslog to the remote server where you install the agent. [Follow these steps](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/aci/apic/sw/1-x/basic-config/b_ACI_Config_Guide/b_ACI_Config_Guide_chapter_010.html#d2933e4611a1635) to configure **Syslog Destination**, **Destination Group**, and **Syslog Source**.

This data connector was developed using Cisco ACI Release 1.x.

## Cisco Identity Services Engine (ISE)

[Follow these instructions](https://www.cisco.com/c/en/us/td/docs/security/ise/3-1/admin_guide/b_ise_admin_3_1.html#ID58) to configure remote syslog collection locations in your Cisco ISE deployment.

## Cisco Stealthwatch

Complete the following configuration steps to get Cisco Stealthwatch logs into Microsoft Sentinel.

1. Sign in to the Stealthwatch Management Console (SMC) as an administrator.
2. In the menu bar, select **Configuration** &gt; **Response Management**.
3. From the **Actions** section in the **Response Management** menu, select **Add &gt; Syslog Message**.
4. In the **Add Syslog Message Action** window, configure parameters.
5. Enter the following custom format:

    `|Lancope|Stealthwatch|7.3|{alarm_type_id}|0x7C|src={source_ip}|dst={target_ip}|dstPort={port}|proto={protocol}|msg={alarm_type_description}|fullmessage={details}|start={start_active_time}|end={end_active_time}|cat={alarm_category_name}|alarmID={alarm_id}|sourceHG={source_host_group_names}|targetHG={target_host_group_names}|sourceHostSnapshot={source_url}|targetHostSnapshot={target_url}|flowCollectorName={device_name}|flowCollectorIP={device_ip}|domain={domain_name}|exporterName={exporter_hostname}|exporterIPAddress={exporter_ip}|exporterInfo={exporter_label}|targetUser={target_username}|targetHostname={target_hostname}|sourceUser={source_username}|alarmStatus={alarm_status}|alarmSev={alarm_severity_name}`
6. Select the custom format from the list and **OK**.
7. Select **Response Management &gt; Rules**.
8. Select **Add** and **Host Alarm**.
9. Provide a rule name in the **Name** field.
10. Create rules by selecting values from the **Type** and **Options** menus. To add more rules, select the ellipsis icon. For a **Host Alarm**, combine as many possible types in a statement as possible.

This data connector was developed using Cisco Stealthwatch version 7.3.2

## Cisco Unified Computing Systems (UCS)

[Follow these instructions](https://www.cisco.com/c/en/us/support/docs/servers-unified-computing/ucs-manager/110265-setup-syslog-for-ucs.html#configsremotesyslog) to configure the Cisco UCS to forward syslog. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

Update the parser and specify the hostname of the source machines transmitting the logs in the parser's first line.

To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **CiscoUCS**. Alternatively, directly load the [function code](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Cisco%20UCS/Parsers/CiscoUCS.yaml). It might take about 15-minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

## Cisco Web Security Appliance (WSA)

Configure Cisco to forward logs via syslog to the remote server where you install the agent. [Follow these steps](https://www.cisco.com/c/en/us/td/docs/security/esa/esa14-0/user_guide/b_ESA_Admin_Guide_14-0/b_ESA_Admin_Guide_12_1_chapter_0100111.html#con_1134718) to configure Cisco WSA to forward logs via Syslog

Select **Syslog Push** as a Retrieval Method.

This data connector was developed using AsyncOS 14.0 for Cisco Web Security Appliance

## Citrix Application Delivery Controller (ADC)

Configure Citrix ADC (former NetScaler) to forward logs via Syslog.

1. Navigate to **Configuration tab &gt; System &gt; Auditing &gt; Syslog &gt; Servers tab**
2. Specify **Syslog action name**.
3. Set IP address of remote Syslog server and port.
4. Set **Transport type** as **TCP** or **UDP** depending on your remote syslog server configuration.

For more information, see the [Citrix ADC (former NetScaler) documentation](https://docs.netscaler.com/).

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation. To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **CitrixADCEvent**. Alternatively, you can directly load the [function code](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Citrix%20ADC/Parsers/CitrixADCEvent.yaml). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

This parser requires a watchlist named `Sources_by_SourceType`.

i. If you don't have watchlist already created, create a watchlist from Microsoft Sentinel in the [Azure portal](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FASIM%2Fdeploy%2FWatchlists%2FASimSourceType.json).

ii. Open watchlist `Sources_by_SourceType` and add entries for this data source.

ii. The SourceType value for CitrixADC is `CitrixADC`. For more information, see [Manage Advanced Security Information Model (ASIM) parsers](/en-us/azure/sentinel/normalization-manage-parsers?WT.mc_id=Portal-fx#configure-the-sources-relevant-to-a-source-specific-parser).

## Digital Guardian Data Loss Prevention

Complete the following steps to configure Digital Guardian to forward logs via Syslog:

1. Sign in to the Digital Guardian Management Console.
2. Select **Workspace** &gt; **Data Export** &gt; **Create Export**.
3. From the **Data Sources** list, select **Alerts** or **Events** as the data source.
4. From the **Export type** list, select **Syslog**.
5. From the **Type list**, select **UDP, or TCP** as the transport protocol.
6. In the **Server** field, type the IP address of your remote syslog server.
7. In the **Port** field, type 514 (or other port if your syslog server was configured to use nondefault port).
8. From the **Severity Level** list, select a severity level.
9. Select the **Is Active** check box.
10. Select **Next**.
11. From the list of available fields, add Alert or Event fields for your data export.
12. Select a Criteria for the fields in your data export and **Next**.
13. Select a group for the criteria and **Next**.
14. Select **Test Query**.
15. Select **Next**.
16. Save the data export.

## ESET Protect integration

Configure ESET PROTECT to send all events through Syslog.

1. Follow [these instructions](https://help.eset.com/protect_admin/latest/en-US/admin_server_settings_syslog.html) to configure syslog output. Make sure to select **BSD** as the format and **TCP** as the transport.
2. Follow [these instructions](https://help.eset.com/protect_admin/latest/en-US/admin_server_settings_export_to_syslog.html) to export all logs to syslog. Select **JSON** as the output format.

## Exabeam Advanced Analytics

[Follow these instructions](https://docs.exabeam.com/en/advanced-analytics/i56/advanced-analytics-administration-guide/125351-advanced-analytics.html#UUID-7ce5ff9d-56aa-93f0-65de-c5255b682a08) to send Exabeam Advanced Analytics activity log data via syslog.

This data connector was developed using Exabeam Advanced Analytics i54 (Syslog)

This data connector was developed using Forescout Syslog Plugin version: v3.6

## Gitlab

[Follow these instructions](https://docs.gitlab.com/omnibus/settings/logs.html#udp-log-forwarding) to send Gitlab audit log data via syslog.

## ISC Bind

1. Follow these instructions to configure the ISC Bind to forward syslog: [DNS Logs](https://kb.isc.org/docs/aa-01526).
2. Configure syslog to send the syslog traffic to the agent. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

## Infoblox Network Identity Operating System (NIOS)

[Follow these instructions](https://www.infoblox.com/wp-content/uploads/infoblox-deployment-guide-slog-and-snmp-configuration-for-nios.pdf) to enable syslog forwarding of Infoblox NIOS Logs. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **Infoblox**. Alternatively, you can directly load the [function code](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Infoblox%20NIOS/Parsers/Infoblox.yaml). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

This parser requires a watchlist named **`Sources_by_SourceType`**.

i. If you don't have watchlist already created, create a watchlist from Microsoft Sentinel in the [Azure portal](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FASIM%2Fdeploy%2FWatchlists%2FASimSourceType.json).

ii. Open watchlist **`Sources_by_SourceType`** and add entries for this data source.

ii. The SourceType value for InfobloxNIOS is **`InfobloxNIOS`**.

For more information, see [Manage Advanced Security Information Model (ASIM) parsers](/en-us/azure/sentinel/normalization-manage-parsers?WT.mc_id=Portal-fx#configure-the-sources-relevant-to-a-source-specific-parser).

## Ivanti Unified Endpoint Management

[Follow the instructions](https://help.ivanti.com/ld/help/en_US/LDMS/11.0/Windows/alert-t-define-action.htm) to set up Alert Actions to send logs to syslog server.

This data connector was developed using Ivanti Unified Endpoint Management Release 2021.1 Version 11.0.3.374

## Juniper SRX

1. Complete the following instructions to configure the Juniper SRX to forward syslog:

    - [Traffic Logs (Security Policy Logs)](https://kb.juniper.net/InfoCenter/index?page=content&amp;id=KB16509&amp;actp=METADATA)
    - [System Logs](https://kb.juniper.net/InfoCenter/index?page=content&amp;id=kb16502)
2. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

## McAfee Network Security Platform

Complete the following configuration steps to get McAfee® Network Security Platform logs into Microsoft Sentinel.

1. Forward alerts from the manager to a syslog server.
2. You must add a syslog notification profile. While creating profile, to make sure that events are formatted correctly, enter the following text in the Message text box:

    `<SyslogAlertForwarderNSP>:|SENSOR_ALERT_UUID|ALERT_TYPE|ATTACK_TIME|ATTACK_NAME|ATTACK_ID``|ATTACK_SEVERITY|ATTACK_SIGNATURE|ATTACK_CONFIDENCE|ADMIN_DOMAIN|SENSOR_NAME|INTERFACE``|SOURCE_IP|SOURCE_PORT|DESTINATION_IP|DESTINATION_PORT|CATEGORY|SUB_CATEGORY``|DIRECTION|RESULT_STATUS|DETECTION_MECHANISM|APPLICATION_PROTOCOL|NETWORK_PROTOCOL|`

This data connector was developed using McAfee® Network Security Platform version: 10.1.x.

## McAfee ePolicy Orchestrator

Contact the provider for guidance on how to register a syslog server.

## Microsoft Sysmon For Linux

This data connector depends on ASIM parsers based on a Kusto Functions to work as expected. [Deploy the parsers](https://aka.ms/ASimSysmonForLinuxARM).

The following functions are deployed:

- vimFileEventLinuxSysmonFileCreated, vimFileEventLinuxSysmonFileDeleted
- vimProcessCreateLinuxSysmon, vimProcessTerminateLinuxSysmon
- vimNetworkSessionLinuxSysmon

[Read more](https://aka.ms/AboutASIM)

## Nasuni

Follow the instructions in the [Nasuni Management Console Guide](https://view.highspot.com/viewer/629a633ae5b4caaf17018daa?iid=5e6fbfcbc7143309f69fcfcf) to configure Nasuni Edge Appliances to forward syslog events. Use the IP address or hostname of the Linux device running the Azure Monitor Agent in the Servers configuration field for the syslog settings.

## OpenVPN

Install the agent on the Server where the OpenVPN are forwarded. OpenVPN server logs are written into common syslog file (depending on the Linux distribution used: e.g. /var/log/messages).

## Oracle Database Audit

Complete the following steps.

1. Create the Oracle database [Follow these steps.](/en-us/azure/virtual-machines/workloads/oracle/oracle-database-quick-create)
2. Sign in to the Oracle database you created. [Follow these steps](https://docs.oracle.com/cd/F49540_01/DOC/server.815/a67772/create.htm).
3. Enable unified logging over syslog by **Alter the system to enable unified logging**[Following these steps](https://docs.oracle.com/en/database/oracle/oracle-database/21/refrn/UNIFIED_AUDIT_COMMON_SYSTEMLOG.html#GUID-9F26BC8E-1397-4B0E-8A08-3B12E4F9ED3A).
4. Create and **enable an Audit policy for unified auditing**[Follow these steps](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/CREATE-AUDIT-POLICY-Unified-Auditing.html#GUID-8D6961FB-2E50-46F5-81F7-9AEA314FC693).
5. **Enabling syslog and Event Viewer** Captures for the Unified Audit Trail [Follow these steps](https://docs.oracle.com/en/database/oracle/oracle-database/18/dbseg/administering-the-audit-trail.html#GUID-3EFB75DB-AE1C-44E6-B46E-30E5702B0FC4).

## Pulse Connect Secure

[Follow the instructions](https://help.ivanti.com/ps/help/en_US/IPS/22.x/ag/configuring_an_external_syslog_server.htm) to enable syslog streaming of Pulse Connect Secure logs. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

Update the parser and specify the hostname of the source machines transmitting the logs in the parser's first line.

To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **PulseConnectSecure**. Alternatively, directly load the [function code](https://aka.ms/sentinel-PulseConnectSecure-parser). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

## RSA SecurID

Complete the following steps to get RSA® SecurID Authentication Manager logs into Microsoft Sentinel. [Follow these instructions](https://community.rsa.com/t5/rsa-authentication-manager/configure-the-remote-syslog-host-for-real-time-log-monitoring/ta-p/571374) to forward alerts from the Manager to a syslog server.

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

Update the parser and specify the hostname of the source machines transmitting the logs in the parser's first line.

To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **RSASecurIDAMEvent**. Alternatively, you can directly load the [function code](https://aka.ms/sentinel-rsasecuridam-parser). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

This data connector was developed using RSA SecurID Authentication Manager version: 8.4 and 8.5

## Sophos XG Firewall

[Follow these instructions](https://doc.sophos.com/nsg/sophos-firewall/20.0/Help/en-us/webhelp/onlinehelp/AdministratorHelp/SystemServices/LogSettings/SyslogServerAdd/index.html) to enable syslog streaming. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

Update the parser and specify the hostname of the source machines transmitting the logs in the parser's first line. To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **SophosXGFirewall**. Alternatively, directly load the [function code](https://aka.ms/sentinel-SophosXG-parser). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

## Symantec Endpoint Protection

[Follow these instructions](https://techdocs.broadcom.com/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/Monitoring-Reporting-and-Enforcing-Compliance/viewing-logs-v7522439-d37e464/exporting-data-to-a-syslog-server-v8442743-d15e1107.html) to configure the Symantec Endpoint Protection to forward syslog. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

Update the parser and specify the hostname of the source machines transmitting the logs in the parser's first line. To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **SymantecEndpointProtection**. Alternatively, you can directly load the [function code](https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/Symantec%20Endpoint%20Protection/Parsers/SymantecEndpointProtection.yaml). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

## Symantec ProxySG

1. Sign in to the Blue Coat Management Console.
2. Select **Configuration** &gt; **Access Logging** &gt; **Formats**.
3. Select **New**.
4. Enter a unique name in the **Format Name** field.
5. Select the radio button for **Custom format string** and paste the following string into the field.

    `  1 $(date) $(time) $(time-taken) $(c-ip) $(cs-userdn) $(cs-auth-groups) $(x-exception-id) $(sc-filter-result) $(cs-categories) $(quot)$(cs(Referer))$(quot) $(sc-status) $(s-action) $(cs-method) $(quot)$(rs(Content-Type))$(quot) $(cs-uri-scheme) $(cs-host) $(cs-uri-port) $(cs-uri-path) $(cs-uri-query) $(cs-uri-extension) $(quot)$(cs(User-Agent))$(quot) $(s-ip) $(sr-bytes) $(rs-bytes) $(x-virus-id) $(x-bluecoat-application-name) $(x-bluecoat-application-operation) $(cs-uri-port) $(x-cs-client-ip-country) $(cs-threat-risk)`
6. Select **OK**.
7. Select **Apply**n.
8. [Follow these instructions](https://knowledge.broadcom.com/external/article/166529/sending-access-logs-to-a-syslog-server.html) to enable syslog streaming of **Access** logs. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

Update the parser and specify the hostname of the source machines transmitting the logs in the parser's first line.

To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **SymantecProxySG**. Alternatively, directly load the [function code](https://aka.ms/sentinel-SymantecProxySG-parser). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

## Symantec VIP

[Follow these instructions](https://aka.ms/sentinel-symantecvip-configurationsteps) to configure the Symantec VIP Enterprise Gateway to forward syslog. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

Update the parser and specify the hostname of the source machines transmitting the logs in the parser's first line.

To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias **SymantecVIP**. Alternatively, directly load the [function code](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Symantec%20VIP/Parsers/SymantecVIP.yaml). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

## VMware ESXi

1. Follow these instructions to configure the VMware ESXi to forward syslog:

    - [VMware ESXi 5.0+](https://docs.vmware.com/en/VMware-vSphere/5.5/com.vmware.vsphere.monitoring.doc/GUID-9F67DB52-F469-451F-B6C8-DAE8D95976E7.html)
2. Use the IP address or hostname for the Linux device with the Linux agent installed as the **Destination IP** address.

Note

The functionality of this data connector is reliant on a Kusto Function-based parser, which is integral to its operation. This parser is deployed as part of the solution installation.

Update the parser and specify the hostname of the source machines transmitting the logs in the parser's first line.

To access the function code within Log Analytics, navigate to the Log Analytics/Microsoft Sentinel Logs section, select Functions, and search for the alias VMwareESXi. Alternatively, directly load the [function code](https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/VMWareESXi/Parsers/VMwareESXi.yaml). It might take about 15 minutes post-installation to update. Although the solution references the deprecated **Log Analytics agent** connector, you can continue to use the same solution, including the referenced parser, with the **Syslog via AMA** data connector instead.

## WatchGuard Firebox

[Follow these instructions](https://www.watchguard.com/help/docs/help-center/en-US/Content/Integration-Guides/General/Microsoft%20Azure%20Sentinel.html?#SetUptheFirebox) to send WatchGuard Firebox log data via syslog.