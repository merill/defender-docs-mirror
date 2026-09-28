---
layout: Conceptual
title: Overview of Defender for Open-Source Relational Databases - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-databases-introduction
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
description: Learn about the benefits and features of Microsoft Defender for Open-Source Relational Databases such as PostgreSQL and MySQL.
ms.date: 2026-08-10T00:00:00.0000000Z
ms.topic: overview
ms.custom:
- sfi-image-nochange
- msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 3e5c0ce7-eafb-5125-ca15-5085387a1b04
document_version_independent_id: 01db2ae2-d7aa-f58f-7ecb-1e59a6412f12
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-databases-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-databases-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-databases-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 87047ecf-1e73-c976-c79a-d6934abc160e
---

# Overview of Defender for Open-Source Relational Databases - Microsoft Defender for Cloud | Microsoft Learn

In Microsoft Defender for Cloud, the *Defender for Open-Source Relational Databases* plan within Defender for Databases detects anomalous activities that indicate unusual and potentially harmful attempts to access or exploit databases. With this plan, you can address potential threats to databases without the need to be a security expert or manage advanced security-monitoring systems.

## Availability

For pricing information about Defender for Open-Source Relational Databases, see the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

Defender for Open-Source Relational Databases is supported on platform as a service (PaaS) environments for Azure and Amazon Web Services (AWS). It isn't supported on Azure Arc-enabled machines. For more information about availability, see [Defender for Cloud support matrices for Azure commercial/other clouds](support-matrix-defender-for-cloud#cloud-support).

For a summary of AWS and GCP workload coverage by plan, see the [multicloud workload protection support matrix](multicloud-support-matrix).

This plan brings threat protections for the following open-source relational databases on Azure.

### Azure Database for PostgreSQL

Protected versions of [Azure Database for PostgreSQL](/en-us/azure/postgresql/) include:

- Flexible Server: All pricing tiers.

### Azure Database for MySQL

Protected versions of [Azure Database for MySQL](/en-us/azure/mysql/) include:

- Flexible Server: All pricing tiers.

### Amazon RDS

Amazon Relational Database Service (RDS) instances on AWS support:

- Aurora PostgreSQL
- Aurora MySQL
- PostgreSQL
- MySQL
- MariaDB

## Benefits

Defender for Cloud provides multicloud alerts on anomalous activities so that you can detect potential threats and respond to them as they occur. For supported Amazon RDS databases, the plan also includes sensitive data discovery. For more information, see [Enable Defender for open-source relational databases on Amazon Web Services](enable-defender-for-databases-aws).

When you enable this plan, Defender for Cloud provides alerts when it detects anomalous database access and query patterns, along with suspicious database activities. The alerts include:

- Details of the suspicious activity that triggered them.
- The associated MITRE ATT&CK tactic.
- Recommended actions for how to investigate and mitigate the threat.
- Options for continuing your investigations by using Microsoft Sentinel.

[![Screenshot that shows example multicloud alerts for databases where Microsoft Defender for Open-Source Relational Databases is enabled.](media/defender-for-databases-introduction/defender-alerts.png)](media/defender-for-databases-introduction/defender-alerts.png#lightbox)

## Alert types

Activities that trigger multicloud alerts enriched with threat intelligence include:

- **Anomalous database access and query patterns**: For example, an abnormally high number of failed sign-in attempts with different credentials (a brute force attack). The alerts can separate successful brute force attacks from unsuccessful ones.
- **Suspicious database activity**: For example, a legitimate user accessing a SQL server from a breached computer that communicated with a crypto-mining command and control (C&C) server.

View the full list of multicloud alerts for database servers in [Alerts for open-source relational databases](alerts-open-source-relational-databases).