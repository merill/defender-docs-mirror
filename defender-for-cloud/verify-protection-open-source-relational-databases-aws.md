---
layout: Conceptual
title: Verify Protection for Open-Source relational Databases on AWS - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/verify-protection-open-source-relational-databases-aws
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
description: Learn how to verify that Microsoft Defender for Cloud is configured to protect open-source relational databases on Amazon RDS and Aurora.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 6877a2e7-bc2d-6083-a7a9-aa8b40bf0ee2
document_version_independent_id: 686a13c1-d4e2-5464-8eea-cfc2b57bf872
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/verify-protection-open-source-relational-databases-aws.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/verify-protection-open-source-relational-databases-aws
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/verify-protection-open-source-relational-databases-aws.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 80ada8d4-516b-7f10-e11f-f0d68e1317da
---

# Verify Protection for Open-Source relational Databases on AWS - Microsoft Defender for Cloud | Microsoft Learn

This article shows you how to verify that Microsoft Defender for Cloud is configured to protect open-source relational databases on Amazon RDS and Amazon Aurora.

Use this article to check plan enablement, connector health, regional configuration, discovery status, and resource-level protection status for supported PostgreSQL, MySQL, MariaDB, Aurora PostgreSQL, and Aurora MySQL resources.

## Verify plan enablement

To verify that the Databases plan is enabled for the AWS connector:

1. In the Azure portal, go to **Microsoft Defender for Cloud**.
2. Go to **Environment settings**.
3. Select the AWS connector.
4. Verify that the **Databases** plan is set to **On**.
5. Under the Databases plan, verify that **Open-source relational databases** is enabled.

If the plan or component is turned off, turn it on and save the connector configuration.

## Verify connector health

To verify that the AWS connector is healthy:

1. In Defender for Cloud, go to **Environment settings**.
2. Select the AWS connector.
3. Review the connector status.

The expected status is **Connected**.

If the connector status is **Not connected** or **Partially connected**, redeploy the AWS CloudFormation template from the connector page to refresh the IAM roles that grant Defender for Cloud access to your AWS environment. After redeployment, wait up to 30 minutes and check the connector status again.

## Verify AWS region configuration

Defender for Cloud protects supported Amazon RDS and Aurora resources only in AWS regions that are configured for the AWS connector.

1. In Defender for Cloud, go to **Environment settings**.
2. Select the AWS connector.
3. Go to the access configuration for the connector.
4. Verify that every AWS region that contains supported RDS or Aurora resources is selected.
5. In AWS, verify that AWS Security Token Service (STS) is active in each selected region.

CloudFormation IAM roles are global, but AWS STS must be active in each region where Defender for Cloud needs to access protected resources.

Learn more about [activating and deactivating AWS STS in a region](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_enable-regions.html#sts-regions-activate-deactivate).

## Allow time for discovery

After the Databases plan is enabled and the AWS connector is healthy, Defender for Cloud discovers supported RDS and Aurora resources.

- New RDS and Aurora resources can take up to six hours to appear in Defender for Cloud.
- Discovery scans run every 12 hours after the initial discovery.

If a supported resource doesn't appear after one full discovery cycle, verify that the resource is in a configured AWS region and that the connector is healthy.

## Verify resource support

Defender for Cloud protects only certain database engines and configurations. Check the following tables to confirm that your resources are supported.

### Supported database engines

The following table lists the database engines that Defender for Cloud supports on AWS.

| Engine | Supported |
| --- | --- |
| PostgreSQL | Yes |
| MySQL | Yes |
| MariaDB | Yes |
| Aurora PostgreSQL | Yes, each cluster instance is protected independently |
| Aurora MySQL | Yes, each cluster instance is protected independently |
| Oracle | No |
| SQL Server | No |

### Supported configurations

The following table lists the supported deployment configurations and any important notes.

| Configuration | Supported | Notes |
| --- | --- | --- |
| Single-AZ | Yes | Standard deployment. |
| Multi-AZ readable standbys | No | Not supported. |
| Read replicas | Partial | Read replicas are monitored as independent instances. |
| Stopped instances | No | Stopped instances are skipped until they're started. |

If the database engine, region, or configuration isn't supported, Defender for Cloud protection doesn't apply to that resource.

## Review resource-level protection status

The recommendation **The status of open-source relational databases on AWS RDS should be protected** lists resources that aren't fully protected. Each unhealthy resource includes a reason that explains what needs to be fixed.

Use the Open-source relational database protection errors and Sensitive data discovery errors tables to review the reason and recommended action.

### Open-source relational database protection errors

The following table lists common protection errors, what they mean, and how to resolve them.

| Unhealthy reason | Description | Recommended action |
| --- | --- | --- |
| **Defender for open-source relational databases isn't authorized** | Defender for open-source relational databases isn't authorized because the onboarding configuration is incomplete. This result can happen if the role's web identity configuration is missing the required service identity, the OpenID Connect (OIDC) provider is missing, or an explicit deny or missing permission is blocking the required action. | Rerun the AWS CloudFormation template for the connector and follow the [AWS onboarding troubleshooting guide](quickstart-onboard-aws?tabs=Defender-for-SQL) to complete onboarding. |
| **Defender for open-source relational databases isn't authorized because a service control policy has an explicit deny** | Defender for open-source relational databases isn't authorized because an AWS service control policy (SCP) has an explicit deny. | Review the SCP applied to the account:1. Sign in to the AWS Management Console.2. Go to **AWS Organizations**.3. In the navigation pane, select **Accounts** or **Organizational Units (OUs)**.4. Select the relevant account.5. Open the **Policies** tab.6. Identify the SCPs attached to the account or parent OU.7. Review explicit deny statements that might block required actions, such as STS, IAM, or RDS.8. Update the SCP to remove or adjust deny rules so Defender for Cloud can perform the required actions.Learn more about [AWS service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html). |
| **STS isn't turned on in this region** | Defender for open-source relational databases is failing because AWS Security Token Service (STS) isn't turned on in this region. | Turn on AWS STS in the required region by using the IAM console:1. Sign in to the AWS Management Console.2. Go to **IAM**.3. In the navigation pane, select **Account settings**.4. Locate **Security Token Service (STS) regions**.5. Find the relevant region and verify its status.6. If STS is turned off, select the region and turn it on.7. Retry Defender onboarding or scan.Learn more about [activating and deactivating AWS STS in a region](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_enable-regions.html#sts-regions-activate-deactivate). |
| **This region isn't supported for Defender for open-source relational databases** | Defender for open-source relational databases isn't currently deployed in the region where this resource is located. | Review the [list of supported regions](quickstart-onboard-aws?tabs=Defender-for-open-source-databases-Preview). If the region is listed as supported and the issue persists, contact Microsoft support. |
| **Amazon RDS instance or cluster is stopped and can't be protected** | Defender for open-source relational databases can't provide protection when your Amazon RDS instance or cluster is stopped. Start the database to restore threat protection. | 1. Go to **AWS Management Console** &gt; **RDS** &gt; **Databases**.2. Select the affected RDS instance or cluster.3. Select **Instance State** &gt; **Start database**.4. For Aurora clusters, select **Start cluster**.5. Wait for the RDS instance or Aurora cluster to reach **Available** status.6. Verify that threat protection resumed. |
| **RDS instance or cluster is pending restart after parameter group configuration** | The RDS instance or RDS cluster has a pending restart after a parameter group change. Defender can't complete protection setup until the restart is applied. | Restart the affected RDS instance or cluster from the AWS console to apply the pending parameter group configuration, then check the recommendation. |
| **Defender failed to create a parameter group** | The parameter group quota limit was reached in this region. | 1. In the AWS console, review the parameter groups defined in this region.2. Remove any parameter groups that aren't assigned to an RDS instance.3. If unassigned parameter groups with the `defenderfordatabases` prefix remain after cleanup, contact Microsoft support. |
| **Defender failed to create an option group** | The option group quota limit was reached in this region. | 1. In the AWS console, review the option groups defined in this region.2. Remove any option groups that aren't assigned to an RDS instance.3. If unassigned option groups with the `defenderfordatabases` prefix remain after cleanup, contact Microsoft support. |
| **Defender encountered an internal error** | Defender for open-source relational databases encountered an internal service error while processing this operation. This error wasn't caused by your current configuration. | Contact Microsoft support if this issue persists. |

### Sensitive data discovery errors

Sensitive data discovery for Amazon RDS is also available through Defender CSPM.

| Unhealthy reason | Description | Recommended action |
| --- | --- | --- |
| **RDS Data Sensitivity Scan isn't authorized** | The onboarding configuration is incomplete or misconfigured. This can happen if the role's web identity configuration is missing the required service identity, an identity-based policy has an explicit deny, the OpenID Connect (OIDC) provider is missing or misconfigured, required permissions are missing, or a permissions boundary prevents the service from performing the required actions. | Rerun the AWS CloudFormation template for the connector and follow the [AWS onboarding troubleshooting guide](quickstart-onboard-aws?tabs=Defender-for-SQL) to complete onboarding. |
| **RDS Data Sensitivity Scan isn't authorized because a service control policy has an explicit deny** | RDS Data Sensitivity Scan isn't authorized because an AWS service control policy (SCP) has an explicit deny. | Review the SCP applied to the account:1. Sign in to the AWS Management Console.2. Go to **AWS Organizations**.3. In the navigation pane, select **Accounts** or **Organizational Units (OUs)**.4. Select the relevant account.5. Open the **Policies** tab.6. Identify the SCPs attached to the account or parent OU.7. Review explicit deny statements that might block required actions, such as STS, IAM, or RDS.8. Update the SCP to remove or adjust deny rules so Defender for Cloud can perform the required actions.Learn more about [AWS service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html). |
| **STS isn't turned on in this region** | RDS Data Sensitivity Scan fails because AWS Security Token Service (STS) isn't turned on in the selected region. | Turn on AWS STS in the required region by using the IAM console:1. Sign in to the AWS Management Console.2. Go to **IAM**.3. In the navigation pane, select **Account settings**.4. Locate **Security Token Service (STS) regions**.5. Find the relevant region and verify its status.6. If STS is turned off, select the region and turn it on.7. Retry Defender onboarding or scan.Learn more about [activating and deactivating AWS STS in a region](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_enable-regions.html#sts-regions-activate-deactivate). |
| **This region isn't supported for RDS Data Sensitivity Scan** | RDS Data Sensitivity Scan isn't currently deployed in the region where this resource is located. | Review the [list of supported regions](quickstart-onboard-aws?tabs=Defender-for-open-source-databases-Preview). If the region is listed as supported and the issue persists, contact Microsoft support. |

## Common verification results

The following scenarios describe common results you might see during verification and how to resolve them.

### The plan is enabled, but the resource shows as not applicable or has no data

Verify that the resource uses a supported engine, configuration, and region. Then verify that the AWS connector is healthy and that one full discovery cycle completed.

### Some AWS regions are protected, but others aren't

Verify that all required AWS regions are selected in the connector configuration. Then verify that AWS STS is active in each affected region.

If you recently added regions to the connector, redeploy the AWS CloudFormation template and allow time for discovery.