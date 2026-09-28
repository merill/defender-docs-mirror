---
layout: Conceptual
title: Troubleshoot the Microsoft Sentinel solution for SAP applications agentless data connector | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-deploy-troubleshoot
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: mapankra
description: Learn how to troubleshoot specific issues that might occur in your Microsoft Sentinel solution for SAP applications agentless data connector deployment.
ms.author: monaberdugo
author: mberdugo
ms.topic: troubleshooting
ms.date: 2026-09-16T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: d393aa5f-db11-d4ee-1fc8-408b39b8bede
document_version_independent_id: e8062a78-e8ac-4c8c-2365-6ac88d2885c1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/sap-deploy-troubleshoot.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/sap-deploy-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/sap-deploy-troubleshoot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 68904cdb-308c-2c44-fdec-c62872ad562b
---

# Troubleshoot the Microsoft Sentinel solution for SAP applications agentless data connector | Microsoft Learn

This article includes troubleshooting steps to help you ensure accurate and timely data ingestion and monitoring for your SAP environment with Microsoft Sentinel.

When working with the agentless data connector, most troubleshooting is done directly in the SAP Integration Suite, where the message log displays errors indicating the nature of the issue encountered.

Start by examining the message processing logs. For more information, see the [SAP documentation](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/monitor-message-processing-monitor). The error messages there can help you diagnose issues with missing permissions, connectivity errors, and other misconfigurations.

If you don't see a related error to your issue, turn on trace logging for more in-depth troubleshooting. For more information, see the [SAP documentation](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/setting-log-levels).

## Check for prerequisites

The agentless data connector package, deployed while [performing the initial connector configuration](preparing-sap#configure-the-connector-in-microsoft-sentinel-and-in-your-sap-system), includes a tool to help SAP admins diagnose and fix issues related to the SAP environment configuration.

**To configure and deploy the tool**:

1. Open the integration package, navigate to the **Artifacts** tab, and select the **Prerequisite checker** iflow &gt; **Configure**.
2. Set the target destination name for the remote function call (RFC) to the SAP system you want to check. For example, `A4H-100-Sentinel-RFC`.
3. Deploy the iflow as you would otherwise for your SAP systems.
4. For best results run the checker for **24 hours** with **1min frequency** to catch any anomalies like rogue overnight batch jobs, or any unknown usage spikes.

**To review the check status**:

1. In SAP Cloud Integration, open **Monitor** &gt; **Integrations** and locate the runs of the **Prerequisite checker** iflow as per your watch period (e.g. 24h). Confirm that the runs completed with status **Completed** (HTTP 200) and that the response payload doesn't contain warnings or errors. The scheduler may produce messages with state "Discarded" due to internal workings of SAP Cloud Integration. These messages can be ignored and contain text like "Message processing has been discarded because the triggering timer event was already handled by another process."
2. Inspect the message processing log (MPL) **Attachments** and properties for the per-check results. Open the file attached to the MPL entry.

[![Screenshot placeholder of the Prerequisite checker iflow run status in SAP Cloud Integration Monitor.](media/preparing-sap/agentless-prerequisite-checker-status.png)](media/preparing-sap/agentless-prerequisite-checker-status.png#lightbox)

Use the following table to interpret the results:

| Status | What it means | Next step |
| --- | --- | --- |
| **Completed**, no warnings | All prerequisites are met. | Continue connecting your SAP system to Microsoft Sentinel. |
| **Completed**, with warnings | Prerequisites are partially met. | Review the response details and remediate before connecting. |
| **Failed** or non-200 status | The checker couldn't reach the target SAP system or hit a configuration error. | Verify the RFC destination and credentials, then redeploy and rerun the iflow. |

If any findings remain, consult the response details for guidance on remediation steps. Legacy SAP systems often require extra SAP notes. Furthermore, see the [troubleshooting section](sap-deploy-troubleshoot) for common issues and resolutions.

Tip

It is a good practice to run the function module `RSAU_API_GET_LOG_DATA` manually to verify correct behavior on the SAP ERP source before further investigation of any upstream issues. Use the ["SAP Security Audit Log Smoke Test" article](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/SAP/Tools/IntegrationSuite/AUDIT-LOG-SMOKE-TEST.md) for more guidance.

**After completion**:

Undeploy the scheduled **Prerequisite checker** iflow once SAP system check was completed successfully. Repeat this sequence for every new SAP system that shall be onboarded.

## Missing functionality in legacy SAP systems

Some legacy SAP systems may be missing required functionality for the **RFC\_READ\_TABLE** function module. Make sure that your SAP admin has reviewed SAP notes 3390051 and 382318, and has patched the system accordingly.

For more information, see [Configure SAP Cloud Connector settings](preparing-sap#configure-sap-cloud-connector-settings).

## "Deploy required Azure resources" error when setting up the data connector

When you set up the Microsoft Sentinel for SAP - agentless data connector, under the **Initial connector configuration &gt; Step 1: Trigger automatic deployment of required Azure resources / SOC Engineer**, after you select **Deploy required resources**, you might see the "Deploy required Azure resources" error or similar (errors may vary). This error might indicate that you're missing the required permissions for the Entra ID app registration.

If you don't have the **Entra ID Application Developer** role or higher, you need to work with a colleague that has this permission to finish setting up the Azure resources. For more information, follow the procedure in the [agentless data connector connection](deploy-data-connector-agentless#connect-your-agentless-data-connector) step.

## Missing "Last address routed"

If you see an error in the security audit log that you're missing the last address routed (an IP address), follow the guidance in the SAP note 3566290.

## Incomplete SAP user master data

If you see an error that you have incomplete SAP user master data or no data in the **ABAPAuthorizationDetails** Microsoft Sentinel table, do the following:

1. Confirm that the **SIAG\_ROLE\_GET\_AUTH** SAP function module exists in the SAP source system.
2. Follow the guidance in SAP note 3088309 for the relevant solution.

## Status code 500 on SAP system connect on Sentinel

If you see an error with status code 500 during the connect process from Sentinel to SAP Cloud Integration, contact your SAP colleague monitoring the integration flow "Data Collector" on SAP Cloud Integration. By nature the error message details are only available on SAP's [Message Processing Log](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/message-processing-log).

## Long message processing times or message volume anomalies on SAP Cloud Integration

If you see sudden spikes in message volumes and processing times on SAP Cloud Integration, consider filtering responsible sources on the NetWeaver side. There are two options available.

1. Use transaction [SM19 and SAP's best practices](https://community.sap.com/t5/application-development-and-automation-blog-posts/analysis-and-recommended-settings-of-the-security-audit-log-sm19-rsau/ba-p/13297094) to apply filter settings on Users and message classes causing the spike
2. Use the [filter capabilities](deploy-data-connector-agentless#customize-data-connector-behavior-optional) of the Sentinel package on SAP Cloud Integration to apply filtering on log read. The parameter max-rows are pre-populated to protect the integration flow from message flooding by design.

Note that log filters on NetWeaver impact what is written to the audit log on the source while a filter on SAP Cloud Integration only chooses not to read the problematic entries.

## Timeouts during connector registration or log polling

The Microsoft Sentinel agentless poller enforces two timeouts when calling the SAP Cloud Integration **Data Collector** iflow. Exceeding either limit causes incomplete ingestion or repeated retries. Error messages on SAP Cloud Integration may vary based on which part of the data extraction pipeline fails first.

### Initial connect (45-second limit) – partial data and failed connector registration

When you connect a new SAP system in Microsoft Sentinel, the initial handshake to the Data Collector iflow must complete within **45 seconds**. If the SAP integration takes longer to respond, the connector ingests partial data and the connector registration fails.

To remediate:

1. Run the [Prerequisite checker](preparing-sap#run-the-prerequisite-checker) iflow and review its runtime measurements to identify the slow downstream call (RFC destination, audit log read, user master read).
2. Tune the SAP integration downstream of SAP Cloud Integration to bring the response time below 45 seconds. Common levers include audit log filter settings ([SM19/RSAU best practices](https://community.sap.com/t5/application-development-and-automation-blog-posts/analysis-and-recommended-settings-of-the-security-audit-log-sm19-rsau/ba-p/13297094)), data connector parameter overrides such as `max-rows` and `offset-in-seconds` (see [Customize data connector behavior](deploy-data-connector-agentless#customize-data-connector-behavior-optional)), and SAP Cloud Connector / RFC sizing.
3. If the response time still can't be reduced, switch to the **SAP CPI–internal scheduler** approach by deploying the **Data Collector Scheduler** iflow from the [Microsoft Sentinel for SAP community repository](https://github.com/Azure-Samples/Sentinel-For-SAP-Community). With the scheduler iflow, Microsoft Sentinel doesn't poll or register the connector; it only receives data pushed by SAP Cloud Integration. This approach trades real-time threat protection for higher tolerance to long-running SAP responses.

For an end-to-end discussion of the tradeoffs, see the blog post [Run agentless SAP connector cost-efficiently](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/run-agentless-sap-connector-cost-efficiently/4464781).

### Long-running iflow (180-second limit) – PROCESSING/ABANDONED states and retry snowball

For ongoing log polling, the Data Collector iflow must complete a single message within **180 seconds**. When the iflow exceeds this limit, you typically see message processing log states such as **PROCESSING** or **ABANDONED** in SAP Cloud Integration. Because the Microsoft Sentinel poller doesn't receive a successful response, it retries the **same time slice** repeatedly, which can snowball into overlapping long-running iflow runs and further slow down the SAP system.

To recover and prevent recurrence:

1. Delete the connector from Microsoft Sentinel and wait for the scheduled Sentinel requests to calm down. This breaks the retry snowball.
2. Run the [Prerequisite checker](preparing-sap#run-the-prerequisite-checker) iflow to identify the root cause of the slow audit log read response times on SAP (for example, missing indexes, oversized audit log, expensive user master reads on legacy releases).
3. Apply the relevant remediation — audit log filter tuning ([SM19/RSAU best practices](https://community.sap.com/t5/application-development-and-automation-blog-posts/analysis-and-recommended-settings-of-the-security-audit-log-sm19-rsau/ba-p/13297094)), Data Collector parameter overrides such as `max-rows`, `offset-in-seconds`, and `force-sal-filesystem` (see [Customize data connector behavior](deploy-data-connector-agentless#customize-data-connector-behavior-optional)) — before reconnecting the data connector in Microsoft Sentinel.
4. If response times still can't be reduced below the 180-second limit, deploy the **Data Collector Scheduler** iflow from the [Microsoft Sentinel for SAP community repository](https://github.com/Azure-Samples/Sentinel-For-SAP-Community). Switching to the SAP CPI–internal scheduler compromises real-time threat protection but avoids the retry pattern enforced by the Microsoft Sentinel poller.

### "Connection reset" or "Connection broken on handle" errors

The Data Collector iFlow might report `java.lang.Exception: Connection reset` when a connection to the SAP backend closes unexpectedly before processing completes. The `Connection broken on handle` error similarly indicates an upstream interruption in the log data pipeline when Microsoft Sentinel requests SAP logs.

These errors are typically caused by network interruptions, downtime, resource saturation, configuration changes, or misconfigurations in the connection path between SAP Cloud Integration, SAP Cloud Connector, and the SAP backend. If multiple SAP systems stop sending logs to Microsoft Sentinel at the same time, the shared SAP Cloud Connector or SAP Cloud Integration component is a likely cause.

To resolve these errors:

1. Engage your SAP Basis team to verify the operational state and connectivity of the affected SAP backend, SAP Cloud Connector, and SAP Cloud Integration.
2. Use SAP's application health monitors to verify connectivity between SAP Cloud Integration, SAP Cloud Connector, and the SAP system.
3. Enable [SAP Cloud Connector runtime monitoring](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/cloud-connector-monitoring).
4. Confirm the [sizing of the SAP Cloud Connector master instance](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/sizing-for-master-instance).
5. Review SAP Cloud Connector connection limits, and use SAP note [3403815](https://me.sap.com/notes/0003403815) to tune the limits.
6. Isolate the affected SID log data flow, and review the other timeout-related guidance in this section.

The Microsoft Sentinel log poller handles brief interruptions through limited retries, so no action is required if ingestion resumes. Longer downtime can result in abandoned time slices to preserve stable operation.

## "Memory Exhaustions" reported by SAP Cloud Integration

The **System** &gt; **Memory** &gt; **Usage** tile in SAP Cloud Integration may report memory exhaustions with the **Data collector** iflow as major contributor across several intervals. A considerable based-load allocation on its own is expected for a log-reading integration flow for multiple SIDs and isn't an error by default. Investigate when memory exhaustions are counted alongside it, when message processing times increase, a new system onboarding attempt, or recent SAP upgrade is happening.

Two patterns typically cause this:

- **Growing request backlog for a single SAP system (SID).** The SAP system responds more slowly than the requested log time slice, so requests accumulate and each subsequent poll adds load on top of the unfinished one. This is commonly a downstream effect of the retry pattern described in the Timeouts during connector registration or log polling section or too large polling interval configurations. It is recommended to keep the 1 min default setting for heavily used SAP systems.
- **Resource saturation on a shared tenant.** High parallel loads from other integration flows or SAP systems on the same SAP Cloud Integration tenant reduce the resources available to the Data Collector iflow, extending processing times across all flows.

To recover, first apply the remediation in the timeouts section to break the retry pattern and reduce the volume returned per message. If memory exhaustions continue, use SAP Cloud Integration monitoring to determine whether the pressure originates from one SAP system or from overall tenant load. Sustained saturation may require additional SAP Cloud Integration capacity, or distributing SAP systems across multiple Cloud Integration instances.

## Timeouts when SAP security audit logs are filesystem-backed

If Microsoft Sentinel integration requests time out during connector onboarding or ongoing log reads, review how your SAP Security Audit Log is recorded and retrieved, especially when recording is configured as **Filesystem and database**.

Selecting audit logs from SAP HANA database often provides the best performance. Other databases and filesystem-backed selection might require tuning.

To remediate:

1. Confirm with your SAP administrator whether Security Audit Log recording targets include filesystem storage.
2. Implement following SAP notes by using **SNOTE** or by importing the referenced support package (applies to **SAP\_BASIS 750+**):
    - **3726943 - RSAU\_API\_GET\_LOG\_DATA | Dataselection only from Filesystem details**
    - **3407647 - RSAU\_READ\_LOG | Optimization of reading audit log files**
3. After implementing the correction, use filesystem-only selection with required parameters `ID_FILESYSTEM_SEL_ONLY` and `ID_FILE_SEL_SIMPLE` for faster retrieval. For behavior details and explanation, see SAP note **3500090**.
4. Re-run connector validation.

Applying these SAP notes often improves retrieval performance significantly. If delays continue, they're typically related to SAP-side factors such as log shipping between application servers and network latency.

## SAP Cloud Connector sizing, throughput, and isolation guidance

If timeout or throughput issues persist, validate SAP Cloud Connector sizing and runtime health by using [Optimize SAP Cloud Connector sizing, throughput, and isolation](preparing-sap#optimize-sap-cloud-connector-sizing-throughput-and-isolation).

Use the following symptom-to-SAP-note mapping for incident triage:

| Symptom | Reference |
| --- | --- |
| CPI logs `IOError on tunnel socket during connect attempt`; ingestion stalls under parallel load | SAP note [3403815](https://me.sap.com/notes/0003403815) |
| SAP Cloud Connector sessions appear stale or unresponsive | SAP note [2485510](https://me.sap.com/notes/0002485510) |
| Repeated shared-connector saturation from other integrations | Isolate Microsoft Sentinel traffic on a dedicated SAP Cloud Connector instance |

## Invalid Credential or cannot get credential for example OAuth2 access token

Besides normal misconfigurations of credentials during registration of the SAP RFC destination on the data connector pane on Microsoft Sentinel, this could be a symptom of attempting integration with unsupported SAP Cloud Platform Integration in the NEO environment. See SAP note [3351844](https://me.sap.com/notes/3351844) for details the end-of-life of services in the NEO environment. Microsoft Sentinel Solution for SAP officially supports SAP Cloud Integration in the Cloud Foundry environment. See the reference on the [SAP preparation guide](preparing-sap#configure-sap-btp-settings).

Customers that want to protect their SAP landscape using Cloud Platform Integration in the NEO environment ahead of their migration to SAP Cloud Integration on the Cloud Foundry environment (Integration Suite), can do so by adopting the provided "Data Collector Scheduler" iflow.

It uses a simplified scheduler. The SAP threat protection scope remains the same. The Sentinel hosted Scheduler is dropped from the setup to avoid the mentioned handshake error with the downside of the Sentinel team having no insight on the healthiness of the Cloud Integration endpoints other than the SAP log data arrival. Often this is no concern, since the scope of monitoring resides with the SAP Cloud Platform Integration team anyways.

## CL\_SAL\_HELPER=&gt;TT\_R\_CLIENT type not found

This error can occur for various reasons in a variety of SAP Support Package levels that require import of SAP notes to fix the underlying bugs in the SAP standard code. Ensure the function module RSAU\_API\_GET\_LOG\_DATA is **remote enabled**, trigger a [manual run from the SAP transaction code SE37](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/SAP/Tools/IntegrationSuite/AUDIT-LOG-SMOKE-TEST.md), and **inspect the output**. The response must show at least one entry in ET\_LOG export parameters table.

The [connector prerequisites section](prerequisites-for-deploying-sap-continuous-threat-monitoring#sap-prerequisites-for-the-agentless-data-connector) lists typical SAP support notes that helped customers in such situations before. The list is not considered complete and only serves as entry point into a customer's individual path to fix SAP's standard functions, which may vary based on their current support package level and associated upgrade journey.