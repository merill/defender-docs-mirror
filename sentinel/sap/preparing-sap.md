---
layout: Conceptual
title: Configure your SAP system for the Microsoft Sentinel solution - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/preparing-sap
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
description: Learn about extra preparations required in your SAP system to connect Microsoft Sentinel to your SAP system.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-08-04T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 46c6a389-105c-90fa-46d6-dca5ba7e94a1
document_version_independent_id: 85947a4c-c342-d5bd-43dd-ddb66cf30d67
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/preparing-sap.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/preparing-sap
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/preparing-sap.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: d76c51d2-152f-fb8f-74e0-535d1460f91c
---

# Configure your SAP system for the Microsoft Sentinel solution - Microsoft Sentinel | Microsoft Learn

This article describes how to prepare your SAP environment for connecting to the SAP data connector. Before you begin, make sure you've reviewed the [prerequisites for deploying the Microsoft Sentinel solution for SAP applications](prerequisites-for-deploying-sap-continuous-threat-monitoring).

This article is part of the second step in deploying the Microsoft Sentinel solution for SAP applications. While steps that are performed in Microsoft Sentinel require that the solution be installed first, other preparations in the SAP environment can happen in parallel.

![Diagram of the deployment flow for the Microsoft Sentinel solution for SAP applications, with the preparing SAP step highlighted.](media/deployment-steps/prepare-sap-environment-agentless.png)

Many of the procedures in this article are typically performed by your **SAP BASIS** team. Some steps include your **security** team too.

## Prerequisites

- Before you start, make sure to review the [prerequisites for deploying the Microsoft Sentinel solution for SAP applications](prerequisites-for-deploying-sap-continuous-threat-monitoring).
- Some steps are performed in Microsoft Sentinel and require that you [deploy the Microsoft Sentinel solution for SAP applications](deploy-sap-security-content) first.

## Configure the Microsoft Sentinel role

To allow the SAP data connector to connect to your SAP system, you must create an SAP system role specifically for this purpose.

Create a role using the [**MSFTSEN\_SENTINEL\_READER**](https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/Sample%20Authorizations%20Role%20File/MSFTSEN_SENTINEL_READER.SAP) template, which includes all the basic permissions for the data connector to operate.

For more information, see the SAP documentation on [creating roles](https://help.sap.com/docs/ABAP_PLATFORM_NEW/ad77b44570314f6d8c3a8a807273084c/4c93141f5c153c91e10000000a42189c.html).

### Create an SAP user for the Microsoft Sentinel role

The Microsoft Sentinel solution for SAP applications requires a user account to connect to your SAP system. When creating your user:

- Make sure to create a system user.
- Assign the **MSFTSEN\_SENTINEL\_READER** role to the user, which you created when you configured the Microsoft Sentinel role.

For more information, see the SAP documentation on [creating user accounts](https://help.sap.com/docs/ABAP_PLATFORM_NEW/ad77b44570314f6d8c3a8a807273084c/4cb5f7ac9cb33c94e10000000a42189c.html?version=LATEST).

## Configure SAP auditing

Some installations of SAP systems might not have audit logging enabled by default. For best results in evaluating the performance and efficacy of the Microsoft Sentinel solution for SAP applications, enable auditing of your SAP system and configure the audit parameters.

We recommend that you configure auditing for *all* messages from the audit log, instead of only specific logs. Ingestion cost differences are generally minimal and the data is useful for Microsoft Sentinel detections and in post-compromise investigations and hunting.

Tip

If you want to ingest SAP HANA DB logs, make sure to also enable auditing for SAP HANA DB. For more information, see [Collect SAP HANA audit logs in Microsoft Sentinel](collect-sap-hana-audit-logs)

Tip

For SAP systems managed by SAP RISE/ECS, Security Audit Log enablement is part of the shared responsibility agreement. Verify with your SAP contact if auditing is already active by default or if any additional steps need to be taken. [SAP S/4HANA Cloud public edition](https://azuremarketplace.microsoft.com/marketplace/apps/sap_jasondau.azure-sentinel-solution-s4hana-public?tab=Overview) systems have auditing enabled by default.

For full monitoring coverage with the agentless data connector, we recommend that you enable monitoring on all client IDs of your monitored SAP systems, including clients 000 and 066.

For more information, see [Analysis and recommended settings of the Security Audit Log (SM19/RSAU)](https://community.sap.com/t5/application-development-blog-posts/analysis-and-recommended-settings-of-the-security-audit-log-sm19-rsau/ba-p/13297094).

## Configure your system to use SNC for secure connections

By default, the SAP data connectors use a remote function call (RFC) connection and a username and password to authenticate to the SAP system.

To encrypt the RFC connection or use certificate-based authentication, configure SAP Smart Network Communications (SNC). Work with your SAP administrators and your organization's public key infrastructure (PKI) team to plan the SNC configuration. Follow SAP guidance for the SAP components, certificates, and trust relationships in your environment.

Before you configure the Microsoft Sentinel connection:

- Configure SNC for SAP NetWeaver Application Server for ABAP (AS ABAP). For an example that uses CommonCryptoLib, see [SAP Note 2979858: Example SNC Configuration for AS ABAP with COMMONCRYPTOLIB](https://me.sap.com/notes/2979858/E).
- Decide whether to use certificates signed by your organization's certification authority (CA) or self-signed certificates. Establish trust between the SAP system and the component that initiates the RFC connection. For SAP certificate guidance, see [SAP Note 2970934: How to create the CSR and how to import the certificate response for ABAP system](https://me.sap.com/notes/2970934/E).
- Validate the SNC connection according to SAP guidance before you connect Microsoft Sentinel.

For the agentless data connector, configure SNC in SAP Cloud Connector. For more information, see [SAP KBA 3536285: SAP Cloud Connector - How to set up general SNC settings for SAP Cloud Connector](https://me.sap.com/notes/3536285/E).

If you use SAP Cloud Connector high availability, also validate SNC after switching to the shadow instance.

For more information, see the SAP documentation on [configuring SNC](https://help.sap.com/docs/ABAP_PLATFORM_NEW/e73bba71770e4c0ca5fb2a3c17e8e229/e656f466e99a11d1a5b00000e835363f.html) and [Getting started with SAP SNC for RFC integrations](https://community.sap.com/t5/enterprise-resource-planning-blogs-by-members/getting-started-with-sap-snc-for-rfc-integrations/ba-p/13983462).

## Configure SAP BTP settings

To prepare SAP Business Technology Platform (BTP) for the agentless data connector, configure the following services and roles in your SAP BTP subaccount.

1. In your SAP BTP subaccount, add entitlements for the following services:

    - SAP Integration Suite
    - SAP Process Integration Runtime
    - Cloud Foundry Runtime

    Note

    This solution considers only SAP Cloud Integration in the Cloud Foundry environment.
2. Create an instance of Cloud Foundry Runtime, and then also create a Cloud Foundry space.
3. Create an instance of SAP Integration Suite.
4. Assign the SAP BTP **Integration\_Provisioner** role to your SAP BTP subaccount user account.
5. In the SAP Integration Suite, add the cloud integration capability.
6. Assign the following process integration roles to your user account:

    - **PI\_Administrator**
    - **PI\_Integration\_Developer**
    - **PI\_Business\_Expert**

    The **PI\_Administrator**, **PI\_Integration\_Developer**, and **PI\_Business\_Expert** roles are available only after you activate the cloud integration capability.
7. Create an instance of the SAP Process Integration Runtime in your subaccount using service plan **integration-flow** (not API!).
8. After verifying that the cloud integration capability is activated, create a service key for the SAP Process Integration Runtime and save the JSON contents to a secure location.

For more information, see the SAP documentation on [Initial Setup of SAP Integration Suite](https://help.sap.com/docs/integration-suite/sap-integration-suite/initial-setup).

## Configure the connector in Microsoft Sentinel and in your SAP system

This procedure has steps both in Microsoft Sentinel and your SAP system, and requires coordination with the SAP administrator.

1. In Microsoft Sentinel, go to the **Configuration &gt; Data connectors** page and locate the **Microsoft Sentinel for SAP - agentless** data connector.
2. In the **Configuration** section, expand and follow the instructions in the **Initial connector configuration - Run the steps below once:** section. These steps will require both your SecuritySOC engineer and the SAP admin.

    1. Trigger automatic deployment of Azure resources (SOC Engineer). If, after you deploy the Azure resources, the values in the steps 2 and 3 aren't automatically populated, close and re-expand step 1 to refresh the values in steps 2 and 3.
    2. Deploy an OAuth2 client credentials artifact in the SAP Integration (SAP Admin).
    3. Deploy the SAP agentless data connector package to the SAP Integration Suite (SAP Admin). This procedure is performed from the SAP Integration Suite portal ([SAP Cloud Integration Web UI](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/overview-of-sap-cloud-integration-web-ui)).

        1. Open the **Discover** section.
        2. Search for **Microsoft Sentinel Solution** and open it.
        3. Click on **Copy** to import the integration package into your Cloud Integration tenant.
        4. Open the package and go to the **Artifacts** tab. Then select the **Data Collector** configuration. For more information, see the SAP documentation on [importing integration packages](https://help.sap.com/docs/integration-suite/sap-integration-suite/importing-integration-packages).
        5. Configure the integration flow with the **LogIngestionURL** and the **DCRImmutableID**.
        6. Deploy the iflow using SAP Cloud Integration as the runtime service.

## Configure SAP Cloud Connector settings

Configure SAP Cloud Connector to enable communication between your SAP backend system and SAP BTP. Before you begin, make sure you have the credentials required to add your SAP BTP subaccount in SAP Cloud Connector.

1. Install the SAP Cloud Connector. For more information, see [Installation of SAP Cloud Connector](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/installation).
2. Sign in at the cloud connector interface, and add the subaccount using the relevant credentials. For more information, see the SAP documentation on [managing subaccounts in SAP Cloud Connector](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/managing-subaccounts).
3. In your cloud connector subaccount, add a new system mapping to the backend system to map the ABAP system to the RFC protocol.
4. Define load balancing options and enter your backend ABAP server details. Copy the name of the virtual host to a secure location to use when you create the SAP BTP destination.
5. Add new resources to the system mapping for each of the following function names:

    - **RSAU\_API\_GET\_LOG\_DATA**, to fetch SAP security audit log data
    - **BAPI\_USER\_GET\_DETAIL**, to retrieve SAP user details
    - **RFC\_READ\_TABLE**, to read data from required tables
    - **SIAG\_ROLE\_GET\_AUTH**, to retrieve security role authorizations
    - **/OSP/SYSTEM\_TIMEZONE**, to retrieve SAP system timezone details

    Note

    The **MSFTSEN\_SENTINEL\_READER** role described in Configure the Microsoft Sentinel role is configured for least privilege access. This ensures function modules such as RFC\_READ\_TABLE are used only as needed. Consider [SAP's best practices for RFC access](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/configure-access-control-rfc#loioca5868997e48468395cf0ca4882f5783__limit) and SAP Unified Connectivity (UCON) settings to control function module access beyond the controls of SAP Cloud Connector and the SAP role.
6. Add a new destination in SAP BTP that points the virtual host you'd created earlier. Use the following details to populate the new SAP BTP RFC destination for Microsoft Sentinel:

    - **Name**: Enter the name you want to use for the Microsoft Sentinel connection
    - **Type**: `RFC`
    - **Proxy Type**: `On-Premise`
    - **User**: Enter the ABAP user account you created earlier for Microsoft Sentinel
    - **Authorization Type**: `CONFIGURED USER`
    - **Additional properties**:

        - `jco.client.ashost = <virtual host name>`
        - `jco.client.client = <client e.g. 001>`
        - `jco.client.sysnr = <system number = 00>`
        - `jco.client.lang = EN`
    - **Location**: Only required when you connect multiple Cloud Connectors to the same BTP subaccount. For more information, see the SAP documentation on [parameters influencing communication behavior](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/parameters-influencing-communication-behavior).

## Optimize SAP Cloud Connector sizing, throughput, and isolation

Default SAP Cloud Connector settings suit most environments. Tune it before you go live when Microsoft Sentinel ingestion is high volume, bursty, or shares an SAP Cloud Connector with other integrations.

1. Confirm sizing for the Cloud Connector master instance: [Sizing for master instance](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/sizing-for-master-instance).
2. If SAP Cloud Integration (CPI) reports `IOError on tunnel socket during connect attempt`, use SAP note [3403815](https://me.sap.com/notes/0003403815) to tune throughput and request limits.
3. Enable runtime monitoring: [Cloud Connector monitoring](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/cloud-connector-monitoring).
4. Recover stale or stuck SAP Cloud Connector sessions by following SAP note [2485510](https://me.sap.com/notes/0002485510).

Tip

Dedicate an SAP Cloud Connector instance to Microsoft Sentinel traffic when the shared connector runs close to saturation, when other integrations cause volatile load patterns, or when security or regulatory requirements mandate isolation. A dedicated instance protects ingestion from noisy-neighbor incidents and simplifies capacity planning, change control, and audit scope.

## Run the prerequisite checker

Run the prerequisite checker to validate that your SAP system is ready for integration with Microsoft Sentinel.

1. The **Prerequisite checker** iflow is included in the Microsoft Sentinel Solution integration package. Configure and deploy this iflow before continuing to the next step, so your SAP system meets the system prerequisites before integration with Microsoft Sentinel. After deployment, the iflow runs on a schedule in SAP Cloud Integration; review the latest run status to confirm success.

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
2. On the Sentinel portal, scroll further down in the **Configuration** area, and expand and follow the instructions in the **Add monitored SAP Systems - Run the steps below for each monitored SAP system:** area for each SAP system you want to monitor.

    In the **Add monitored SAP Systems** wizard in Microsoft Sentinel, at the step named **Connect SAP System to Microsoft Sentinel / SOC Engineer**, continue with [Connect your SAP system to Microsoft Sentinel](deploy-data-connector-agentless).