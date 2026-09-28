---
layout: Conceptual
title: Overview of the ServiceNow integration - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/integration-servicenow
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn about integrating ServiceNow with Microsoft Defender for Cloud to protect Azure, hybrid, and multicloud machines.
ms.topic: overview
ms.date: 2025-05-20T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 50faff91-1f49-4456-4727-b7825b494f6a
document_version_independent_id: 9b4cfef3-056a-cbbc-bb08-775ff8e2a585
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/integration-servicenow.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/integration-servicenow
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/integration-servicenow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 25fea889-f9d8-806d-3ad9-e3a0b40f3830
---

# Overview of the ServiceNow integration - Microsoft Defender for Cloud | Microsoft Learn

ServiceNow is a cloud-based workflow automation and enterprise-oriented solution that enables organizations to manage and track digital workflows within a unified, robust platform. ServiceNow helps to improve operational efficiencies by streamlining and automating routine work tasks and delivers resilient services that help increase your productivity.

ServiceNow can be integrated with Microsoft Defender for Cloud to allow customers to prioritize remediation of recommendations that affect your business. Defender for Cloud integrates workflows with the following ServiceNow modules:

- **IT Service Management (ITSM)** -For incident management. As part of this connection, customers can create and view ServiceNow tickets, that are linked to recommendations generated in Defender for Cloud.
- **Configuration Compliance** - For compliance management. As part of this connection, customers can review and address Defender for Cloud's CSPM plan's findings in ServiceNow's portal.

## IT Service Management (ITSM)

As part of the integration, you can create and monitor tickets in ServiceNow directly from Defender for Cloud:

- **Incident**: An incident is an unplanned interruption of reduction in the quality of an IT service as reported by a user or monitoring system. ServiceNow’s incident management module helps IT teams track and manage incidents, from initial reporting to resolution.
- **Problem**: A problem is the underlying cause of one or more incidents. It’s often a recurring or persistent issue that needs to be addressed to prevent future incidents.
- **Change**: A change is a planned alternation or addition to an IT service or its supporting infrastructure. A change management module helps IT teams plan, approve, and execute changes in a controlled and systematic manner. It minimizes the risk of service disruptions and maintains service quality.

### Bidirectional synchronization

As part of the governance capabilities within Defender for Cloud, you can enable a bi-directional integration between ServiceNow and Defender for Cloud, for the creation of ITSM incidents, changes or problem tickets.

Tickets can be initiated manually or automatically by leveraging governance automation rules. When using governance automation rules with the ServiceNow integration, the selected owner must resolve to a ServiceNow user or assignment group.

Note

Synchronization occurs every 24 hrs.

## Configuration Compliance module

As part of the integration, you can utilize the Defender for Cloud's CSPM plan's findings into the ServiceNow Configuration Compliance module to unify compliance efforts across on-premises and cloud environments.

When you ingest Defender for Cloud's findings into ServiceNow's Configuration Compliance module, your teams can utilize the Configuration Compliance module to identify, prioritize and remediate configuration issues in your cloud assets. You can also reduce security risks and improve your overall compliance posture through automated workflows and real-time insights.

To integrate Defender for Cloud's findings into ServiceNow's Configuration Compliance module:

- **In the Azure portal**:

    - An Azure account with Defender for Cloud onboarded. If you don't already have an Azure account, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - [Enable Defender for Cloud Foundational CSPM or Defender CSPM](tutorial-enable-cspm-plan) on the relevant Azure subscriptions, AWS accounts or GCP projects.
- **In ServiceNow**:

    - Have an [application registry in ServiceNow](https://www.opslogix.com/knowledgebase/servicenow/kb-create-a-servicenow-api-key-and-secret-for-the-scom-servicenow-incident-connector).
    - [Enable the ServiceNow Configuration Compliance module](https://store.servicenow.com/sn_appstore_store.do#!/store/application/29691e1f0212471dad08668c1e39932b/14.12.4?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%25253Bgenerative_ai%25253Bsnow_solution%26q%3DConfiguration%2520Compliance&amp;sl=sh).
    - [Enable the ServiceNow Microsoft Defender for Cloud integration.](https://docs.servicenow.com/bundle/washingtondc-security-management/page/product/secops-integration-vr/azure-security-center/concept/cc_asc_overview.html).
    - [Configure the Microsoft Defender for Cloud Integration in ServiceNow](https://docs.servicenow.com/bundle/washingtondc-security-management/page/product/secops-integration-vr/azure-security-center/task/cc_asc_install_configure.html).