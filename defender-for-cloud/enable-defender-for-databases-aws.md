---
layout: Conceptual
title: Enable Defender for Open-source Relational Databases on Amazon Web Services (AWS) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-defender-for-databases-aws
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
description: Enable Defender for open-source relational databases on AWS RDS to detect suspicious activity and protect supported database engines.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 2e006d5d-188d-ba36-5533-a9b6c3c4de26
document_version_independent_id: 3dd2f621-5d0f-8f0d-6683-a6468fcb925b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-defender-for-databases-aws.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-defender-for-databases-aws
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-defender-for-databases-aws.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/982661b3-cc41-45b1-b21d-18b4b6937344
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/bbee35d0-ba85-4062-b9c2-388c328eb4fa
platformId: dfaa402d-cfbd-3472-7840-98e2f011c44f
---

# Enable Defender for Open-source Relational Databases on Amazon Web Services (AWS) - Microsoft Defender for Cloud | Microsoft Learn

Important

On June 1, 2026, Microsoft Defender for Open-Source Relational Databases for AWS RDS transitioned to General Availability, and billing started. If you had the plan enabled before June 1, 2026 you continue to receive database threat protection and sensitive data discovery capabilities for supported AWS RDS databases. No action is required if you want to keep the protection enabled. To opt out, follow the instructions in Disable the plan.

The Defender for open-source relational databases plan in Microsoft Defender for Cloud helps you detect and investigate unusual activity in your AWS Relational Database Service (RDS) databases. This plan supports the following database instance types:

- Aurora PostgreSQL
- Aurora MySQL
- PostgreSQL
- MySQL
- MariaDB

This article explains how to enable Defender for open-source relational databases on AWS so that you can start receiving alerts for suspicious activity.

When you enable this plan, Defender for Cloud also discovers sensitive data in your AWS account and enriches security insights with these findings. Sensitive data discovery is also included in Defender Cloud Security Posture Management (CSPM).

Learn more about this Microsoft Defender plan in [Overview of Microsoft Defender for open-source relational databases](defender-for-databases-introduction).

## Prerequisites

Before you enable Defender for open-source relational databases on AWS, ensure you meet the following requirements:

- An Azure subscription. If you don't have one, [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Defender for Cloud enabled on your Azure subscription. [Enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- At least one connected [AWS account](quickstart-onboard-aws) with the required access and permissions.
- Region availability: All public AWS regions (excluding Tel Aviv, Milan, Jakarta, Spain, and Bahrain).

## Enable Defender for open-source relational databases

To enable Defender for open-source relational databases on AWS:

1. Sign in to [the Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **Environment settings**.
4. Select the relevant AWS account.
5. Locate the **Databases** plan and select **Settings**.

    [![Screenshot of the AWS environment settings page that shows where to select Settings.](media/enable-defender-for-databases-aws/databases-settings.png)](media/enable-defender-for-databases-aws/databases-settings.png#lightbox)
6. Toggle open-source relational databases to **On**.

    [![Screenshot that shows how to turn on open-source relational databases protection.](media/enable-defender-for-databases-aws/toggle-open-source-on.png)](media/enable-defender-for-databases-aws/toggle-open-source-on.png#lightbox)

    Note

    Turning on open-source relational databases also enables sensitive data discovery, a shared feature with Defender CSPM for RDS resources.

    [![Screenshot that shows the settings page for Defender CSPM and the sensitive data turned on with the protected resources.](media/enable-defender-for-databases-aws/cspm-shared.png)](media/enable-defender-for-databases-aws/cspm-shared.png#lightbox)

    For more information, see [Discover and scan AWS RDS instances](concept-data-security-posture-prepare#discover-and-scan-aws-rds-instances).
7. Select **Configure access**.
8. In the deployment method section, select **Download**.
9. Follow the instructions to update the stack in AWS. Updating the AWS stack creates or updates the CloudFormation template with the required permissions.
10. Select the checkbox to confirm that you updated the CloudFormation template in your AWS environment (stack).
11. Select **Review and generate**.
12. Review the information and select **Update**.

Defender for Cloud then automatically updates the relevant parameter and option group settings.

### Required permissions for DefenderForCloud-DataThreatProtectionDB role

The following permissions are required for the role that you create or update when you download the CloudFormation template and update the AWS stack. These permissions allow Defender for Cloud to configure auditing and collect database activity logs from your AWS RDS instances.

| Permission | Description |
| --- | --- |
| rds:AddTagsToResource | Adds tags on option and parameter groups created by the plan. |
| rds:DescribeDBClusterParameters | Describes parameters inside the cluster group. |
| rds:CreateDBParameterGroup | Creates a database parameter group. |
| rds:ModifyOptionGroup | Modifies options inside an option group. |
| rds:DescribeDBLogFiles | Describes database log files. |
| rds:DescribeDBParameterGroups | Describes database parameter groups. |
| rds:CreateOptionGroup | Creates an option group. |
| rds:ModifyDBParameterGroup | Modifies parameters inside database parameter groups. |
| rds:DownloadDBLogFilePortion | Downloads log file portions. |
| rds:DescribeDBInstances | Describes database instances. |
| rds:ModifyDBClusterParameterGroup | Modifies cluster parameters inside the cluster parameter group. |
| rds:ModifyDBInstance | Modifies databases to assign parameter or option groups as needed. |
| rds:ModifyDBCluster | Modifies clusters to assign cluster parameter groups as needed. |
| rds:DescribeDBParameters | Describes parameters inside the database group. |
| rds:CreateDBClusterParameterGroup | Creates a cluster parameter group. |
| rds:DescribeDBClusters | Describes clusters. |
| rds:DescribeDBClusterParameterGroups | Describes cluster parameter groups. |
| rds:DescribeOptionGroups | Describes option groups. |

## Affected parameter and option group settings

When you enable Defender for open-source relational databases, Defender for Cloud automatically configures auditing parameters in your RDS instances to consume and analyze access patterns. You don't need to modify these settings manually. The auditing settings are listed here for reference.

| Type | Parameter | Value |
| --- | --- | --- |
| PostgreSQL and Aurora PostgreSQL | log\_connections | 1 |
| PostgreSQL and Aurora PostgreSQL | log\_disconnections | 1 |
| Aurora MySQL cluster parameter group | server\_audit\_logging | 1 |
| Aurora MySQL cluster parameter group | server\_audit\_events | - If it exists, expand the value to include CONNECT, QUERY,  - If it doesn't exist, add it with the value CONNECT, QUERY. |
| Aurora MySQL cluster parameter group | server\_audit\_excl\_users | If it exists, expand it to include rdsadmin. |
| Aurora MySQL cluster parameter group | server\_audit\_incl\_users | If this setting exists and includes rdsadmin, remove rdsadmin from SERVER\_AUDIT\_EXCL\_USER and leave this setting empty. |

An option group is required for MySQL and MariaDB with the following options for the `MARIADB_AUDIT_PLUGIN`.

If the option doesn’t exist, add it. If it exists, expand the values as needed.

| Option name | Value |
| --- | --- |
| SERVER\_AUDIT\_EVENTS | If it exists, expand the value to include CONNECT  If it doesn't exist, add it with value CONNECT. |
| SERVER\_AUDIT\_EXCL\_USER | If it exists, expand it to include rdsadmin. |
| SERVER\_AUDIT\_INCL\_USERS | If this setting exists and includes rdsadmin, remove rdsadmin from SERVER\_AUDIT\_EXCL\_USER and leave this setting empty. |

Important

You might need to restart your instances to apply these changes.

If you're using the default parameter group, Defender for Cloud creates a new parameter group with the required changes and the prefix `defenderfordatabases*`.

If you create a new parameter group or update static parameters, the changes don't take effect until you restart the instance.

Note

- If a parameter group already exists, Defender for Cloud updates it.
- `MARIADB_AUDIT_PLUGIN` is supported in MariaDB 10.2 and later, MySQL 8.0.25 and later, and all MySQL 5.7 versions.
- Changes that Defender for Cloud makes to the `MARIADB_AUDIT_PLUGIN` for MySQL instances are applied during the next maintenance window. For more information, see [MARIADB_AUDIT_PLUGIN for MySQL instances](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.MySQL.Options.AuditPlugin.html#Appendix.MySQL.Options.AuditPlugin.Add).

## Disable the plan

To disable Defender for open-source relational databases on AWS RDS:

1. Sign in to [the Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant AWS account.
4. Locate the Databases plan and select **Settings**.
5. Toggle open-source relational databases to **Off**.
6. Select **Save**.