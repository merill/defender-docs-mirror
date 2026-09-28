---
layout: Conceptual
title: Explore risks to sensitive data - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/data-security-review-risks
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
description: Learn how to use attack paths and security explorer to find and remediate sensitive data risks.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: template-how-to-pattern, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: b082e4f8-f307-976c-4b86-24d6f83d6d74
document_version_independent_id: b5460784-b462-ae1e-c3a5-779e441f4db9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/data-security-review-risks.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/data-security-review-risks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/data-security-review-risks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: c740d043-dc9b-0ffb-6d4b-b70898fdbab0
---

# Explore risks to sensitive data - Microsoft Defender for Cloud | Microsoft Learn

This article explains how to investigate sensitive data risks in attack paths, Cloud Security Explorer, and related alerts in Microsoft Defender for Cloud. You learn how to identify exposed resources that contain sensitive data, prioritize security alerts, and export findings to share with data owners for remediation.

## Explore and review sensitive data risks

Microsoft Defender for Cloud provides several ways to explore sensitive data risks after you [discover resources with sensitive data](data-security-posture-enable):

- **Attack paths**: When sensitive data discovery is enabled in the Defender Cloud Security Posture Management (CSPM) plan, you can use attack paths to discover risk of data breaches. For more information, see [Data security posture management in Defender CSPM](concept-data-security-posture#data-security-posture-management-in-defender-cspm).
- **Security Explorer**: When sensitive data discovery is enabled in the Defender CSPM plan, you can use Cloud Security Explorer to find sensitive data insights. For more information, see [Data security posture management in Defender CSPM](concept-data-security-posture#data-security-posture-management-in-defender-cspm).
- **Security alerts**: When sensitive data discovery is enabled in the Defender for Storage plan, you can prioritize and explore ongoing threats to sensitive data stores by applying sensitivity filters in Security Alerts settings.

## Explore risks through attack paths

View predefined attack paths to discover data breach risks, and get remediation recommendations, as follows:

1. In Defender for Cloud, open **Attack path analysis**.
2. Filter by **Risk Factors**, and select **Sensitive data** to filter the data-related attack paths.

    [![Screenshot that shows attack paths for data risk.](media/data-security-review-risks/attack-paths.png)](media/data-security-review-risks/attack-paths.png#lightbox)
3. Review the data attack paths.
4. To view sensitive information detected in data resources, select the resource name &gt; **Insights**. Then, expand the **Contain sensitive data** insight.
5. For risk mitigation steps, open **Active Recommendations**.

Other examples of attack paths for sensitive data include:

- "Internet exposed Azure Storage container with sensitive data is publicly accessible"
- "Managed database with excessive internet exposure and sensitive data allows basic (local user/password) authentication"
- "VM has high severity vulnerabilities and read permission to a data store with sensitive data"
- "Internet exposed AWS S3 Bucket with sensitive data is publicly accessible"
- "Private AWS S3 bucket that replicates data to the internet is exposed and publicly accessible"
- "RDS snapshot is publicly available to all AWS accounts"

## Explore risks with Cloud Security Explorer

Explore data risks and exposure in cloud security graph insights using a query template, or by defining a manual query.

1. In Defender for Cloud, open **Cloud Security Explorer**.
2. You can build your own query, or select one of the sensitive data query templates &gt; **Open query**, and modify it as needed. Here's an example:

    [![Screenshot that shows an Insights data query.](media/data-security-review-risks/query.png)](media/data-security-review-risks/query.png#lightbox)

### Use query templates

As an alternative to creating your own query, you can use predefined query templates. Several sensitive data query templates are available. For example:

- Internet exposed storage containers with sensitive data that allow public access.
- Internet exposed S3 buckets with sensitive data that allow public access

When you open a predefined query, it's populated automatically and can be tweaked as needed. For example, here are the prepopulated fields for "Internet exposed storage containers with sensitive data that allow public access".

[![Screenshot that shows an Insights data query template.](media/data-security-review-risks/query-template.png)](media/data-security-review-risks/query-template.png#lightbox)

## Explore sensitive data security alerts

When sensitive data discovery is enabled in the Defender for Storage plan, you can prioritize and focus on alerts that affect resources with sensitive data. For details, see [Monitor data security alerts in Defender for Storage](defender-for-storage-data-sensitivity).

For platform as a service (PaaS) databases and Amazon S3 buckets, findings are reported to Azure Resource Graph (ARG). You can filter and sort by sensitivity labels and sensitive info types in the Defender for Cloud Inventory, Alert, and Recommendation blades.

## Export findings

It's common for the security administrator, who reviews sensitive data findings in attack paths or the security explorer, to lack direct access to the data stores. Therefore, they need to share the findings with the data owners, who can then conduct further investigation.

To share findings with data owners, use the **Export** within the **Contains sensitive data** insight.

[![Screenshot of how to export insights.](media/data-security-review-risks/export-findings.png)](media/data-security-review-risks/export-findings.png#lightbox)

The CSV file produced includes:

- **Sample name** – depending on the resource type, this can be a database column, file name, or container name.
- **Sensitivity label** – the highest ranking label found on this resource (same value for all rows).
- **Contained in** – sample full path (file path or column full name).
- **Sensitive info types** – discovered info types per sample. If more than one info type was detected, a new row is added for each info type. This is to allow an easier filtering experience.

Note

**Download CSV report** in the Cloud Security Explorer page exports all insights retrieved by the query in raw format (json).