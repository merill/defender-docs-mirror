---
layout: Conceptual
title: Overview of Microsoft Defender for SQL servers on machines - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-servers-introduction
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
description: Learn how Microsoft Defender for SQL servers on machines secures your SQL databases. It works on Azure, AWS, GCP, and on-premises. It finds vulnerabilities and detects threats.
ms.date: 2025-01-26T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 01e9d031-fa09-2769-397d-9ade1c9b978b
document_version_independent_id: 63e8b2f9-2a26-9b4d-7b4f-2024742d9864
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-sql-servers-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-sql-servers-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-sql-servers-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: a3098455-bb28-fea5-9a54-a5c2624af2bd
---

# Overview of Microsoft Defender for SQL servers on machines - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's Defender for Databases plan provides protection for SQL servers on machines. Defender for SQL servers on machines protects SQL servers hosted on Azure, Amazon Web Service (AWS), Google Cloud Platform (GCP), and on premises machines. Defender for SQL servers on machines helps you identify and mitigate potential database vulnerabilities and detect anomalous activities that could indicate threats to your databases.

## What are the benefits of Defender for SQL servers on machines?

Defender for SQL servers on machines provides the following features:

- [Vulnerability assessment](sql-azure-vulnerability-assessment-overview): Scan databases to discover, track, and remediate vulnerabilities.
- [Advanced threat protection](/en-us/azure/azure-sql/database/threat-detection-overview): Mitigate threats by receiving detailed security alerts and recommended actions based on SQL Advanced Threat Protection.

When you [enable Defender for SQL servers on machines](defender-for-sql-usage), all supported resources that exist within the subscription are protected. Future resources created on the same subscription ware also be protected.

Defender for SQL servers on machines allows you to [explore vulnerability assessment reports](defender-for-sql-on-machines-vulnerability-assessment#view-vulnerabilities-in-graphical-interactive-reports) via scans that occur every 12 hours. The vulnerability assessment reports provide an overview of your SQL machines' security state and details of any security findings. Defender for SQL servers on machines helps you identify and mitigate potential database vulnerabilities, and detect anomalous activities that could indicate threats to your databases.

You can also [set a baseline](defender-for-sql-on-machines-vulnerability-assessment#set-a-baseline) to mark the current state of your SQL servers on machines and compare it to the state of your SQL servers on machines at a later time. This process allows you to track changes in your SQL servers on machines' security state over time.

Results can also be [exported to a CSV file](defender-for-sql-on-machines-vulnerability-assessment#export-results) for further analysis, or you can [view vulnerabilities in graphical, interactive reports](defender-for-sql-on-machines-vulnerability-assessment#view-vulnerabilities-in-graphical-interactive-reports).

Advanced Threat Protection can identify **Potential SQL injection**, **Access from unusual location or data center**, **Access from unfamiliar principal or potentially harmful application**, and **Brute force SQL credentials**.

With all of these features, Defender for SQL servers on machines helps you to protect your SQL servers on machines from potential threats and vulnerabilities.

## Related resources