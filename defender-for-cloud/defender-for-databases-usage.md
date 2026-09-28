---
layout: Conceptual
title: Respond to Defender open-source database alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-databases-usage
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
description: Investigate and respond to alerts from Microsoft Defender for open-source relational databases, including Azure Database services and AWS Relational Database Service instances.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: fa469464-1200-6452-27d0-346b085803c2
document_version_independent_id: 341054d0-7770-2b2e-8fc4-6ef107f36a7c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-databases-usage.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-databases-usage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-databases-usage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: f4a7474b-5c1c-9ab4-9934-ebe1db22a174
---

# Respond to Defender open-source database alerts - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases for the following services:

- [Azure Database for PostgreSQL](/en-us/azure/postgresql/)
- [Azure Database for MySQL](/en-us/azure/mysql/)

For Amazon Web Services (AWS) Relational Database Service (RDS) instances (Preview):

- Aurora PostgreSQL
- Aurora MySQL
- PostgreSQL
- MySQL
- MariaDB

To get alerts from the Microsoft Defender plan, first [enable Defender for open-source relational databases on Azure](enable-defender-for-databases-azure) or [enable Defender for open-source relational databases on AWS](enable-defender-for-databases-aws).

Learn more about Microsoft Defender for open-source relational databases in [Overview of Microsoft Defender for open-source relational databases](defender-for-databases-introduction).

## Prerequisites

Before you respond to database alerts, make sure these prerequisites are met:

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- **AWS users only**: [Connect your AWS account by using the AWS onboarding quickstart](quickstart-onboard-aws).

## Respond to alerts in Defender for Cloud

When Defender for Cloud is enabled on your database, it detects anomalous activities and generates alerts.

You can find alerts in multiple locations, including:

- In the Azure portal:

    - **Defender for Cloud's security alerts page** - Shows alerts for all resources protected by Defender for Cloud in the subscriptions you've got permissions to view.
    - The resource's **Microsoft Defender for Cloud** page - Shows alerts and recommendations for one specific resource.
- The designated person in your organization receives email alerts in their inbox after you [configure email notifications](configure-email-notifications).

Tip

A live tile on [Defender for Cloud's overview dashboard](overview-page) tracks the status of active threats to your resources including databases. Select the security alerts tile to navigate to the Defender for Cloud security alerts page and get an overview of active threats detected on your databases.

For detailed steps and the recommended method to respond to security alerts, see [Respond to a security alert](manage-respond-alerts#respond-to-a-security-alert).

### Respond to email notifications of security alerts

Defender for Cloud sends email notifications when it detects anomalous database activities.

Each email includes details about the security event, such as activity type, database name, server name, application name, and event time. The email also includes possible causes and recommended investigation and mitigation actions.

1. From the email, select the **View the full alert** link to launch the Azure portal and show the security alerts page, which provides an overview of active threats detected on the database.

    [![Defender for Cloud's email notification about a suspected brute force attack.](media/defender-for-databases-usage/suspected-brute-force-attack-notification-email.png)](media/defender-for-databases-usage/suspected-brute-force-attack-notification-email.png#lightbox)

    View active threats at the subscription level from within the Defender for Cloud portal pages:

    [![Active threats on one or more subscriptions are shown in Microsoft Defender for Cloud.](media/defender-for-databases-usage/db-alerts-page.png)](media/defender-for-databases-usage/db-alerts-page.png#lightbox)
2. For extra details and recommended actions for investigating the current threat and remediating future threats, select a specific alert.

    [![Screenshot that shows the details of a specific alert.](media/defender-for-databases-usage/specific-alert-details.png)](media/defender-for-databases-usage/specific-alert-details.png#lightbox)

Tip

For a detailed tutorial on how to handle your alerts, see [Manage and respond to alerts](tutorial-security-incident).