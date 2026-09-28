---
layout: Conceptual
title: Custom logs via AMA connector - Configure data ingestion to Microsoft Sentinel from specific applications | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/unified-connector-custom-device
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
description: Learn how to configure data ingestion into Microsoft Sentinel from specific or custom applications that produce logs as text files, using the Custom Logs via AMA data connector or manual configuration.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-07-31T00:00:00.0000000Z
locale: en-us
document_id: 7fb7620c-4616-bb66-a234-3fed73015acd
document_version_independent_id: ee4a2e7b-112b-b1ab-2aa7-7783942ad26b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/unified-connector-custom-device.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/unified-connector-custom-device
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/unified-connector-custom-device.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: d3148a63-1fcf-210d-1f38-15ad987c4beb
---

# Custom logs via AMA connector - Configure data ingestion to Microsoft Sentinel from specific applications | Microsoft Learn

Microsoft Sentinel's **Custom Logs via AMA** data connector supports the collection of logs from text files from several different network and security applications and devices.

This article supplies the configuration information, unique to each specific security application, that you need to supply when configuring this data connector. This information is provided by the application providers. Contact the provider for updates, for more information, or when information is unavailable for your security application. For the full instructions to install and configure the connector, see [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama), but refer back to this article for the unique information to supply for each application.

This article also shows you how to ingest data from these applications to your Microsoft Sentinel workspace without using the connector. These steps include installation of the Azure Monitor Agent. After the connector is installed, use the instructions appropriate to your application, shown later in this article, to complete the setup.

The devices from which you collect custom text logs fall into two categories:

- Applications installed on Windows or Linux machines

    The application stores its log files on the machine where it's installed. To collect these logs, the Azure Monitor Agent is installed on this same machine.
- Appliances that are self-contained on closed (usually Linux-based) devices

    These appliances store their logs on an external syslog server. To collect these logs, the Azure Monitor Agentis installed on this external syslog server, often called a log forwarder.

For more information about the related Microsoft Sentinel solution for each of these applications, search the [Azure Marketplace](https://azuremarketplace.microsoft.com/) for the **Product Type** &gt; **Solution Templates** or review the solution from the **Content hub** in Microsoft Sentinel.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## General instructions

The steps for collecting logs from machines hosting applications and appliances follow a general pattern:

1. Create the destination table in one of the following locations:

    - In the Defender portal, use the **Advanced Hunting** page.
    - In the Azure portal, use Log Analytics.
2. Create the data collection rule (DCR) for your application or appliance.
3. Deploy the Azure Monitor Agent to the machine hosting the application, or to the external server (log forwarder) that collects logs from appliances if it's not already deployed.
4. Configure logging on your application. If an appliance, configure it to send its logs to the external server (log forwarder) where the Azure Monitor Agent is installed.

These general steps (except for the last one) are automated when you use the **Custom Logs via AMA** data connector, and are described in detail in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama).

## Specific instructions per application type

The per-application information you need to complete these steps is presented in the rest of this article. Some of these applications are on self-contained appliances and require a different type of configuration, starting with the use of a log forwarder.

Each application section contains the following information:

- Unique parameters to supply to the configuration of the **Custom Logs via AMA** data connector, if you're using it.
- The outline of the procedure required to ingest data manually, without using the connector. For the details of this procedure, see [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama).
- Specific instructions for configuring the originating applications or devices themselves, and/or links to the instructions on the providers' web sites. These steps must be taken whether using the connector or not.

## Apache HTTP Server

Follow these steps to ingest log messages from Apache HTTP Server:

1. Table name: `ApacheHTTPServer_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Windows: `"C:\Server\bin\log\Apache24\logs\*.log"`
    - Linux: `"/var/log/httpd/*.log"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.

Back to top

## Apache Tomcat

Follow these steps to ingest log messages from Apache Tomcat:

1. Table name: `Tomcat_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Linux: `"/var/log/tomcat/*.log"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.

Back to top

## Cisco Meraki

Follow these steps to ingest log messages from Cisco Meraki:

1. Table name: `meraki_CL`
2. Log storage location: Create a log file on your external syslog server. Grant the syslog daemon write permissions to the file. Install the AMA on the external syslog server if it's not already installed. Enter this filename and path in the **File pattern** field in the connector, or in place of the `{LOCAL_PATH_FILE}` placeholder in the DCR.
3. Configure the syslog daemon to export its Meraki log messages to a temporary text file so the AMA can collect them.

# [rsyslog](#tab/rsyslog)
1. Create a custom configuration file for the rsyslog daemon and save it to `/etc/rsyslog.d/10-meraki.conf`. Add the following filtering conditions to this configuration file:

        ```bash
        if $rawmsg contains "flows" then {
            action(type="omfile" file="<LOG_FILE_Name>")
            stop
        }
        if $rawmsg contains "urls" then { 
            action(type="omfile" file="<LOG_FILE_Name>") 
            stop 
        } 
        if $rawmsg contains "ids-alerts" then { 
            action(type="omfile" file="<LOG_FILE_Name>") 
            stop 
        } 
        if $rawmsg contains "events" then { 
            action(type="omfile" file="<LOG_FILE_Name>") 
            stop 
        } 
        if $rawmsg contains "ip_flow_start" then { 
            action(type="omfile" file="<LOG_FILE_Name>") 
            stop 
        } 
        if $rawmsg contains "ip_flow_end" then { 
            action(type="omfile" file="<LOG_FILE_Name>") 
            stop 
        }
        ```

        (Replace `<LOG_FILE_Name>` with the name of the log file you created.)

        To learn more about filtering conditions for rsyslog, see [rsyslog: Filter conditions](https://rsyslog.readthedocs.io/en/latest/configuration/filters.html). We recommend testing and modifying the configuration based on your specific installation.
    2. Restart rsyslog. The typical command syntax is `systemctl restart rsyslog`.

# [syslog-ng](#tab/syslog-ng)
1. Edit the config file `/etc/syslog-ng/conf.d`, adding the following conditions:

        ```bash
        filter f_meraki {
            message("flows") or message("urls") or message("ids-alerts") or message("events") or message("ip_flow_start") or message("ip_flow_end"); 
        }; 
        
        destination d_meraki { 
            file("<LOG_FILE_NAME>"); 
        }; 
        
        log { 
            source(s_src); 
            filter(f_meraki); 
            destination(d_meraki); 
            flags(final); #Ensures that once a message matches the filter and is written to the specified destination, it will not be processed by subsequent log statements 
        }; 
        ```

        (Replace `<LOG_FILE_NAME>` with the name of the log file you created.)
    2. Restart syslog-ng. The typical command syntax is `systemctl restart syslog-ng`.

---
4. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    - Replace the column name `"RawData"` with the column name `"Message"`.
    - Replace the transformKql value `"source"` with the value `"source | project-rename Message=RawData"`.
    - Replace the `{TABLE_NAME}` and `{LOCAL_PATH_FILE}` placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.
5. Configure the machine where the Azure Monitor Agent is installed to open the syslog ports, and configure the syslog daemon there to accept messages from external sources. For detailed instructions and a script to automate this configuration, see [Configure the log forwarder to accept logs](connect-custom-logs-ama#configure-the-log-forwarder-to-accept-logs).
6. Configure and connect the Cisco Meraki device(s): follow the [instructions provided by Cisco](https://documentation.meraki.com/General_Administration/Monitoring_and_Reporting/Meraki_Device_Reporting_-_Syslog%2C_SNMP%2C_and_API) for sending syslog messages. Use the IP address or hostname of the virtual machine where the Azure Monitor Agent is installed.

Back to top

## JBoss Enterprise Application Platform

Follow these steps to ingest log messages from JBoss Enterprise Application Platform:

1. Table name: `JBossLogs_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns") - Linux only:

    - Standalone server: `"{EAP_HOME}/standalone/log/server.log"`
    - Managed domain: `"{EAP_HOME}/domain/servers/{SERVER_NAME}/log/server.log"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.

Back to top

## JuniperIDP

Follow these steps to ingest log messages from JuniperIDP:

1. Table name: `JuniperIDP_CL`
2. Log storage location: Create a log file on your external syslog server. Grant the syslog daemon write permissions to the file. Install the AMA on the external syslog server if it's not already installed. Enter this filename and path in the **File pattern** field in the connector, or in place of the `{LOCAL_PATH_FILE}` placeholder in the DCR.
3. Configure the syslog daemon to export its JuniperIDP log messages to a temporary text file so the AMA can collect them.

# [rsyslog](#tab/rsyslog)
1. Create custom configuration file for the rsyslog daemon, in the `/etc/rsyslog.d/` folder, with the following filtering conditions:

        ```bash
         # Define a new ruleset
        ruleset(name="<RULESET_NAME>") { 
            action(type="omfile" file="<LOG_FILE_NAME>") 
        } 
        
         # Set the input on port and bind it to the new ruleset 
        input(type="imudp" port="<PORT>" ruleset="<RULESET_NAME>") 
        ```

        (Replace `<parameters>` with the actual names of the objects represented. &lt;LOG\_FILE\_NAME&gt; is the file you created in step 2.)
    2. Restart rsyslog. The typical command syntax is `systemctl restart rsyslog`.

# [syslog-ng](#tab/syslog-ng)
1. Edit the config file `/etc/syslog-ng/conf.d`, adding the following conditions:

        ```bash
        source s_network {
            network ( 
                ip(“0.0.0.0”) 
                port(<PORT>) 
            ); 
        }; 
        destination d_file { 
            file(“<LOG_FILE_NAME>”); 
        }; 
        log { 
            source(s_network); 
            destination(d_file); 
        }; 
        ```

        (Replace `<LOG_FILE_NAME>` with the name of the log file you created.)
    2. Restart syslog-ng. The typical command syntax is `systemctl restart syslog-ng`.

---
4. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    - Replace the column name `"RawData"` with the column name `"Message"`.
    - Replace the `{TABLE_NAME}` and `{LOCAL_PATH_FILE}` placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.
    - Replace the transformKql value `"source"` with the following Kusto query (enclosed in double quotes):

        ```kusto
        source | parse RawData with tmp_time " " host_s " " ident_s " " tmp_pid " " msgid_s " " extradata | extend dvc_os_s = extract("\\[(junos\\S+)", 1, extradata) | extend event_end_time_s = extract(".*epoch-time=\"(\\S+)\"", 1, extradata) | extend message_type_s = extract(".*message-type=\"(\\S+)\"", 1, extradata) | extend source_address_s = extract(".*source-address=\"(\\S+)\"", 1, extradata) | extend destination_address_s = extract(".*destination-address=\"(\\S+)\"", 1, extradata) | extend destination_port_s = extract(".*destination-port=\"(\\S+)\"", 1, extradata) | extend protocol_name_s = extract(".*protocol-name=\"(\\S+)\"", 1, extradata) | extend service_name_s = extract(".*service-name=\"(\\S+)\"", 1, extradata) | extend application_name_s = extract(".*application-name=\"(\\S+)\"", 1, extradata) | extend rule_name_s = extract(".*rule-name=\"(\\S+)\"", 1, extradata) | extend rulebase_name_s = extract(".*rulebase-name=\"(\\S+)\"", 1, extradata) | extend policy_name_s = extract(".*policy-name=\"(\\S+)\"", 1, extradata) | extend export_id_s = extract(".*export-id=\"(\\S+)\"", 1, extradata) | extend repeat_count_s = extract(".*repeat-count=\"(\\S+)\"", 1, extradata) | extend action_s = extract(".*action=\"(\\S+)\"", 1, extradata) | extend threat_severity_s = extract(".*threat-severity=\"(\\S+)\"", 1, extradata) | extend attack_name_s = extract(".*attack-name=\"(\\S+)\"", 1, extradata) | extend nat_source_address_s = extract(".*nat-source-address=\"(\\S+)\"", 1, extradata) | extend nat_source_port_s = extract(".*nat-source-port=\"(\\S+)\"", 1, extradata) | extend nat_destination_address_s = extract(".*nat-destination-address=\"(\\S+)\"", 1, extradata) | extend nat_destination_port_s = extract(".*nat-destination-port=\"(\\S+)\"", 1, extradata) | extend elapsed_time_s = extract(".*elapsed-time=\"(\\S+)\"", 1, extradata) | extend inbound_bytes_s = extract(".*inbound-bytes=\"(\\S+)\"", 1, extradata) | extend outbound_bytes_s = extract(".*outbound-bytes=\"(\\S+)\"", 1, extradata) | extend inbound_packets_s = extract(".*inbound-packets=\"(\\S+)\"", 1, extradata) | extend outbound_packets_s = extract(".*outbound-packets=\"(\\S+)\"", 1, extradata) | extend source_zone_name_s = extract(".*source-zone-name=\"(\\S+)\"", 1, extradata) | extend source_interface_name_s = extract(".*source-interface-name=\"(\\S+)\"", 1, extradata) | extend destination_zone_name_s = extract(".*destination-zone-name=\"(\\S+)\"", 1, extradata) | extend destination_interface_name_s = extract(".*destination-interface-name=\"(\\S+)\"", 1, extradata) | extend packet_log_id_s = extract(".*packet-log-id=\"(\\S+)\"", 1, extradata) | extend alert_s = extract(".*alert=\"(\\S+)\"", 1, extradata) | extend username_s = extract(".*username=\"(\\S+)\"", 1, extradata) | extend roles_s = extract(".*roles=\"(\\S+)\"", 1, extradata) | extend msg_s = extract(".*message=\"(\\S+)\"", 1, extradata) | project-away RawData
        ```

        The following screenshot shows the complete query in the preceding example in a more readable format:

        [![Screenshot showing expanded Kusto query with line breaks for readability.](media/unified-connector-custom-device/kusto-query-screenshot.png)](media/unified-connector-custom-device/kusto-query-screenshot.png#lightbox)

        See more information on the following items used in the preceding examples, in the Kusto documentation:

        - [***parse*** operator](/en-us/kusto/query/parse-operator?view=microsoft-sentinel&amp;preserve-view=true)
        - [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
        - [***extract*** function](/en-us/kusto/query/extract-function?view=microsoft-sentinel&amp;preserve-view=true)
        - [***project-away*** operator](/en-us/kusto/query/project-away-operator?view=microsoft-sentinel&amp;preserve-view=true)

        For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

        Other resources:

        - [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
        - [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)
5. Configure the machine where the Azure Monitor Agent is installed to open the syslog ports, and configure the syslog daemon there to accept messages from external sources. For detailed instructions and a script to automate this configuration, see [Configure the log forwarder to accept logs](connect-custom-logs-ama#configure-the-log-forwarder-to-accept-logs).
6. For the instructions to configure the Juniper IDP appliance to send syslog messages to an external server, see [SRX Getting Started - Configure System Logging.](https://supportportal.juniper.net/s/article/SRX-Getting-Started-Configure-System-Logging).

Back to top

## MarkLogic Audit

Follow these steps to ingest log messages from MarkLogic Audit:

1. Table name: `MarkLogicAudit_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Windows: `"C:\Program Files\MarkLogic\Data\Logs\AuditLog.txt"`
    - Linux: `"/var/opt/MarkLogic/Logs/AuditLog.txt"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.
4. Configure MarkLogic Audit to enable it to write logs: (from MarkLogic documentation)

    1. Using your browser, navigate to MarkLogic Admin interface.
    2. Open the Audit Configuration screen under Groups &gt; group\_name &gt; Auditing.
    3. Mark the Audit Enabled radio button. Make sure it is enabled.
    4. Configure audit event and/or restrictions desired.
    5. Validate by selecting OK.
    6. Refer to MarkLogic documentation for [more details and configuration options](https://docs.marklogic.com/guide/admin/auditing).

Back to top

## MongoDB Audit

Follow these steps to ingest log messages from MongoDB Audit:

1. Table name: `MongoDBAudit_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Windows: `"C:\data\db\auditlog.json"`
    - Linux: `"/data/db/auditlog.json"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.
4. Configure MongoDB to write logs:

    1. For Windows, edit the configuration file `mongod.cfg`. For Linux, `mongod.conf`.
    2. Set the `dbpath` parameter to `data/db`.
    3. Set the `path` parameter to `/data/db/auditlog.json`.
    4. Refer to MongoDB documentation for [more parameters and details](https://www.mongodb.com/docs/manual/tutorial/configure-auditing/).

Back to top

## NGINX HTTP Server

Follow these steps to ingest log messages from NGINX HTTP Server:

1. Table name: `NGINX_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Linux: `"/var/log/nginx.log"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.

Back to top

## Oracle WebLogic Server

Follow these steps to ingest log messages from Oracle WebLogic Server:

1. Table name: `OracleWebLogicServer_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Windows: `"{DOMAIN_NAME}\Servers\{SERVER_NAME}\logs*.log"`
    - Linux: `"{DOMAIN_HOME}/servers/{SERVER_NAME}/logs/*.log"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.

Back to top

## PostgreSQL Events

Follow these steps to ingest log messages from PostgreSQL Events:

1. Table name: `PostgreSQL_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Windows: `"C:\*.log"`
    - Linux: `"/var/log/*.log"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.
4. Edit the PostgreSQL Events configuration file `postgresql.conf` to output logs to files.

    1. Set `log_destination='stderr'`
    2. Set `logging_collector=on`
    3. Refer to PostgreSQL documentation for [more parameters and details](https://www.postgresql.org/docs/current/runtime-config-logging.html).

Back to top

## SecurityBridge Threat Detection for SAP

Follow these steps to ingest log messages from SecurityBridge Threat Detection for SAP:

1. Table name: `SecurityBridgeLogs_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Linux: `"/usr/sap/tmp/sb_events/*.cef"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.

Back to top

## SquidProxy

Follow these steps to ingest log messages from SquidProxy:

1. Table name: `SquidProxy_CL`
2. Log storage location: Logs are stored as text files on the application's host machine. Install the AMA on the same machine to collect the files.

    Default file locations ("filePatterns"):

    - Windows: `"C:\Squid\var\log\squid\*.log"`
    - Linux: `"/var/log/squid/*.log"`
3. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    Replace the {TABLE\_NAME} and {LOCAL\_PATH\_FILE} placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.

Back to top

## Ubiquiti UniFi

Follow these steps to ingest log messages from Ubiquiti UniFi:

1. Table name: `Ubiquiti_CL`
2. Log storage location: Create a log file on your external syslog server. Grant the syslog daemon write permissions to the file. Install the AMA on the external syslog server if it's not already installed. Enter this filename and path in the **File pattern** field in the connector, or in place of the `{LOCAL_PATH_FILE}` placeholder in the DCR.
3. Configure the syslog daemon to export its Ubiquiti log messages to a temporary text file so the AMA can collect them.

# [rsyslog](#tab/rsyslog)
1. Create custom configuration file for the rsyslog daemon, in the `/etc/rsyslog.d/` folder, with the following filtering conditions:

        ```bash
         # Define a new ruleset
        ruleset(name="<RULESET_NAME>") { 
            action(type="omfile" file="<LOG_FILE_NAME>") 
        } 
        
         # Set the input on port and bind it to the new ruleset 
        input(type="imudp" port="<PORT>" ruleset="<RULESET_NAME>") 
        ```

        (Replace `<parameters>` with the actual names of the objects represented. &lt;LOG\_FILE\_NAME&gt; is the file you created in step 2.)
    2. Restart rsyslog. The typical command syntax is `systemctl restart rsyslog`.

# [syslog-ng](#tab/syslog-ng)
1. Edit the config file `/etc/syslog-ng/conf.d`, adding the following conditions:

        ```bash
        source s_network {
            network ( 
                ip(“0.0.0.0”) 
                port(<PORT>) 
            ); 
        }; 
        destination d_file { 
            file(“<LOG_FILE_NAME>”); 
        }; 
        log { 
            source(s_network); 
            destination(d_file); 
        }; 
        ```

        (Replace `<LOG_FILE_NAME>` with the name of the log file you created.)
    2. Restart syslog-ng. The typical command syntax is `systemctl restart syslog-ng`.

---
4. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    - Replace the column name `"RawData"` with the column name `"Message"`.
    - Replace the transformKql value `"source"` with the value `"source | project-rename Message=RawData"`.
    - Replace the `{TABLE_NAME}` and `{LOCAL_PATH_FILE}` placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.
5. Configure the machine where the Azure Monitor Agent is installed to open the syslog ports, and configure the syslog daemon there to accept messages from external sources. For detailed instructions and a script to automate this configuration, see [Configure the log forwarder to accept logs](connect-custom-logs-ama#configure-the-log-forwarder-to-accept-logs).
6. Configure and connect the Ubiquiti controller.

    1. Follow the [instructions provided by Ubiquiti](https://help.ui.com/hc/en-us/categories/6583256751383) to enable syslog and optionally debugging logs.
    2. Select Settings &gt; System Settings &gt; Controller Configuration &gt; Remote Logging and enable syslog.

Back to top

## VMware vCenter

Follow these steps to ingest log messages from VMware vCenter:

1. Table name: `vcenter_CL`
2. Log storage location: Create a log file on your external syslog server. Grant the syslog daemon write permissions to the file. Install the AMA on the external syslog server if it's not already installed. Enter this filename and path in the **File pattern** field in the connector, or in place of the `{LOCAL_PATH_FILE}` placeholder in the DCR.
3. Configure the syslog daemon to export its vCenter log messages to a temporary text file so the AMA can collect them.

# [rsyslog](#tab/rsyslog)
1. Edit the configuration file `/etc/rsyslog.conf` to add the following template line before the *directive* section:

        `$template vcenter,"%timestamp% %hostname% %msg%\ n"`
    2. Create custom configuration file for the rsyslog daemon, saved as `/etc/rsyslog.d/10-vcenter.conf` with the following filtering conditions:

        ```bash
        if $rawmsg contains "vpxd" then {
            action(type="omfile" file="/<LOG_FILE_NAME>")
            stop
        }
        if $rawmsg contains "vcenter-server" then { 
            action(type="omfile" file="/<LOG_FILE_NAME>") 
            stop 
        } 
        ```

        (Replace `<LOG_FILE_NAME>` with the name of the log file you created.)
    3. Restart rsyslog. The typical command syntax is `sudo systemctl restart rsyslog`.

# [syslog-ng](#tab/syslog-ng)
1. Edit the config file `/etc/syslog-ng/conf.d`, adding the following filtering conditions:

        ```bash
        filter f_vcenter {
            message("vpxd") or message("vcenter-server"); 
        }; 
        
        destination d_vcenter { 
            file("<LOG_FILE_NAME>"); 
        }; 
        
        log { 
            source(s_src); 
            filter(f_vcenter); 
            destination(d_vcenter); 
            flags(final); #Ensures that once a message matches the filter and is written to the specified destination, it will not be processed by subsequent log statements 
        }; 
        ```

        (Replace `<LOG_FILE_NAME>` with the name of the log file you created.)
    2. Restart syslog-ng. The typical command syntax is `systemctl restart syslog-ng`.

---
4. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    - Replace the column name `"RawData"` with the column name `"Message"`.
    - Replace the transformKql value `"source"` with the value `"source | project-rename Message=RawData"`.
    - Replace the `{TABLE_NAME}` and `{LOCAL_PATH_FILE}` placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.
    - dataCollectionEndpointId should be populated with your DCE. If you don't have one, define a new one. See [Create a data collection endpoint](/en-us/azure/azure-monitor/essentials/data-collection-endpoint-overview#create-a-data-collection-endpoint) for the instructions.
5. Configure the machine where the Azure Monitor Agent is installed to open the syslog ports, and configure the syslog daemon there to accept messages from external sources. For detailed instructions and a script to automate this configuration, see [Configure the log forwarder to accept logs](connect-custom-logs-ama#configure-the-log-forwarder-to-accept-logs).
6. Configure and connect the vCenter devices.

    1. Follow the [instructions provided by VMware](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.monitoring.doc/GUID-9633A961-A5C3-4658-B099-B81E0512DC21.html) for sending syslog messages.
    2. Use the IP address or hostname of the machine where the Azure Monitor Agent is installed.

Back to top

## Zscaler Private Access (ZPA)

Follow these steps to ingest log messages from Zscaler Private Access (ZPA):

1. Table name: `ZPA_CL`
2. Log storage location: Create a log file on your external syslog server. Grant the syslog daemon write permissions to the file. Install the AMA on the external syslog server if it's not already installed. Enter this filename and path in the **File pattern** field in the connector, or in place of the `{LOCAL_PATH_FILE}` placeholder in the DCR.
3. Configure the syslog daemon to export its ZPA log messages to a temporary text file so the AMA can collect them.

# [rsyslog](#tab/rsyslog)
1. Create custom configuration file for the rsyslog daemon, in the `/etc/rsyslog.d/` folder, with the following filtering conditions:

        ```bash
         # Define a new ruleset
        ruleset(name="<RULESET_NAME>") { 
            action(type="omfile" file="<LOG_FILE_NAME>") 
        } 
        
         # Set the input on port and bind it to the new ruleset 
        input(type="imudp" port="<PORT>" ruleset="<RULESET_NAME>") 
        ```

        (Replace `<parameters>` with the actual names of the objects represented.)
    2. Restart rsyslog. The typical command syntax is `systemctl restart rsyslog`.

# [syslog-ng](#tab/syslog-ng)
1. Edit the config file `/etc/syslog-ng/conf.d`, adding the following conditions:

        ```bash
        source s_network {
            network ( 
                ip(“0.0.0.0”) 
                port(<PORT>) 
            ); 
        }; 
        destination d_file { 
            file(“<LOG_FILE_NAME>”); 
        }; 
        log { 
            source(s_network); 
            destination(d_file); 
        }; 
        ```

        (Replace `<LOG_FILE_NAME>` with the name of the log file you created.)
    2. Restart syslog-ng. The typical command syntax is `systemctl restart syslog-ng`.

---
4. Create the DCR according to the directions in [Collect logs from text files with the Azure Monitor Agent and ingest to Microsoft Sentinel](connect-custom-logs-ama#configure-the-data-connector).

    - Replace the column name `"RawData"` with the column name `"Message"`.
    - Replace the transformKql value `"source"` with the value `"source | project-rename Message=RawData"`.
    - Replace the `{TABLE_NAME}` and `{LOCAL_PATH_FILE}` placeholders in the [DCR template](connect-custom-logs-ama?tabs=arm#create-the-data-collection-rule) with the values in steps 1 and 2. Replace the other placeholders as directed.
5. Configure the machine where the Azure Monitor Agent is installed to open the syslog ports, and configure the syslog daemon there to accept messages from external sources. For detailed instructions and a script to automate this configuration, see [Configure the log forwarder to accept logs](connect-custom-logs-ama#configure-the-log-forwarder-to-accept-logs).
6. Configure and connect the ZPA receiver.

    1. Follow the [instructions provided by ZPA](https://help.zscaler.com/zpa/configuring-log-receiver). Select JSON as the log template.
    2. Select Settings &gt; System Settings &gt; Controller Configuration &gt; Remote Logging and enable syslog.

Back to top