---
layout: Conceptual
title: Troubleshoot connectors guide - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/troubleshoot-connectors
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
description: This guide is for IT professionals, security analysts, and cloud admins who need to troubleshoot problems related to Microsoft Defender for Cloud's AWS and GCP connectors.
ms.topic: concept-article
ms.date: 2026-01-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 498b2cae-43e6-a176-9369-ea60071e272f
document_version_independent_id: b33d4d1d-393a-f72d-b2bd-21c234b9ff8b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/troubleshoot-connectors.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/troubleshoot-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/troubleshoot-connectors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
platformId: f366c424-7dab-45c4-787d-765c84abfc32
---

# Troubleshoot connectors guide - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud provides a unified security management system that helps you protect your cloud resources. It supports various cloud providers, including Amazon Web Services (AWS) and Google Cloud Platform (GCP). This guide is for IT professionals, security analysts, and cloud admins who need to troubleshoot problems related to Microsoft Defender for Cloud connectors.

## Troubleshoot connectors

Defender for Cloud uses connectors to collect monitoring data from Amazon Web Services (AWS) accounts and Google Cloud Platform (GCP) projects. If you're experiencing problems with the connectors or you don't see data from AWS or GCP, review the following troubleshooting tips.

### Tips for common connector problems

- Make sure that the subscription associated with the connector is selected in the subscription filter located in the **Directories + subscriptions** section of the Azure portal.
- Standards should be assigned on the security connector. To check, go to **Environment settings** on the Defender for Cloud left menu, select the connector, and then select **Settings**. If no standards are assigned, select the three dots to check if you have permissions to assign standards.
- A connector resource should be present in Azure Resource Graph. Use the following Resource Graph query to check: `resources | where ['type'] =~ "microsoft.security/securityconnectors"`.
- Make sure that sending Kubernetes audit logs is enabled on the AWS or GCP connector so that you can get [threat detection alerts for the control plane](alerts-containers).
- Make sure that the Microsoft Defender sensor and the Azure Policy for Azure Arc-enabled Kubernetes extensions were installed successfully to your Amazon Elastic Kubernetes Service (EKS) and Google Kubernetes Engine (GKE) clusters. You can verify and install the agent with the following Defender for Cloud recommendations:
    - **EKS clusters should have Microsoft Defender's extension for Azure Arc installed**
    - **GKE clusters should have Microsoft Defender's extension for Azure Arc installed**
    - **Azure Arc-enabled Kubernetes clusters should have the Azure Policy extension installed**
    - **GKE clusters should have the Azure Policy extension installed**
- If you're experiencing problems with deleting the AWS or GCP connector, check the Azure Activity log for failed delete operations caused by resource locks. If a lock is present, learn how to [Manage locks to prevent resources from being deleted or changed](/en-us/azure/azure-resource-manager/management/lock-resources) to remove it and try again.
- Check that workloads exist in the AWS account or GCP project.

### Tips for AWS connector problems

- Make sure that the CloudFormation template deployment finished successfully.
- Wait at least 12 hours after creation of the AWS root account.
- Make sure that EKS clusters are successfully connected to Azure Arc-enabled Kubernetes.
- If you don't see AWS data in Defender for Cloud, make sure that the required AWS resources for sending data to Defender for Cloud exist in the AWS account.

### CloudFormation error resolution table

If you see an error when deploying the CloudFormation template, use the following table to help identify and resolve the issue.

| Error | Suggested fix |
| --- | --- |
| Access denied | Ensure AWS user or role has proper IAM role.• Check StackSet trust (Org access).• Run script with proper IAM role. |
| Already exists/Duplicate resource | Deploy template in one region first.• Skip or conditionally create globals in others.• Remove any leftover duplicate instances, then retry. |
| Unsupported Lambda runtime | Template is outdated.• Download latest template (updated runtime).• Update stack or StackSet with new template.• Verify Lambda uses new runtime. |
| No Updates to be performed | No changes detected.• Confirm you're using the new template.• If not, get the current template.• If yes and no changes needed, no action. |
| StackSet won't start in portal and hangs | Deployment orchestration issue. • Enable Org trusted access for CFN.• Try manual StackSet update via AWS console or CLI.• Use browser dev tools to catch hidden errors. |
| Azure connector error | Azure or AWS config mismatch.• Verify CloudFormation stack name and settings.• Ensure management and member stacks deployed.• Align names, then retry in portal. |
| Other / Not sure / Still failing | Seek further help. • Contact Microsoft Support with logs and details. |

### Connected to Sentinel first

If you connected your AWS account to Microsoft Sentinel first, the Defender for Cloud connector won't work. To fix this issue, you need to edit the CloudFormation template and apply remediation steps within your AWS account.

Learn how to [Connect a Microsoft Sentinel connected AWS account to Defender for Cloud](sentinel-connected-aws).

#### Cost impact of API calls to AWS

When you onboard your AWS single or management account, the discovery service in Defender for Cloud starts an immediate scan of your environment. The discovery service executes API calls to various service endpoints in order to retrieve all resources that Azure helps secure.

After this initial scan, the service continues to periodically scan your environment at the interval that you configured during onboarding. In AWS, each API call to the account generates a lookup event that's recorded in the CloudTrail resource. The CloudTrail resource incurs costs. For pricing details, see the [AWS CloudTrail Pricing](https://aws.amazon.com/cloudtrail/pricing/) page on the Amazon AWS site.

If you connected your CloudTrail to GuardDuty, you're also responsible for associated costs. You can find these costs in the [GuardDuty documentation](https://docs.aws.amazon.com/guardduty/latest/ug/monitoring_costs.html) on the Amazon AWS site.

#### Get the number of native API calls

There are two ways to get the number of calls that Defender for Cloud made:

- Use an existing Athena table or create a new one. For more information, see [Querying AWS CloudTrail logs](https://docs.aws.amazon.com/athena/latest/ug/cloudtrail-logs.html) on the Amazon AWS site.
- Use an existing event data store or create a new one. For more information, see [Working with AWS CloudTrail Lake](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-lake.html) on the Amazon AWS site.

Both methods rely on querying AWS CloudTrail logs.

To get the number of calls, go to the Athena table or the event data store and use one of the following predefined queries, according to your needs. Replace `<TABLE-NAME>` with the ID of the Athena table or event data store.

- List the number of overall API calls by Defender for Cloud:

    ```sql
    SELECT COUNT(*) AS overallApiCallsCount FROM <TABLE-NAME> 
    WHERE userIdentity.arn LIKE 'arn:aws:sts::<YOUR-ACCOUNT-ID>:assumed-role/CspmMonitorAws/MicrosoftDefenderForClouds_<YOUR-AZURE-TENANT-ID>' 
    AND eventTime > TIMESTAMP '<DATETIME>' 
    ```
- List the number of overall API calls by Defender for Cloud aggregated by day:

    ```sql
    SELECT DATE(eventTime) AS apiCallsDate, COUNT(*) AS apiCallsCountByRegion FROM <TABLE-NAME> 
    WHERE userIdentity.arn LIKE 'arn:aws:sts:: <YOUR-ACCOUNT-ID>:assumed-role/CspmMonitorAws/MicrosoftDefenderForClouds_<YOUR-AZURE-TENANT-ID>' 
    AND eventTime > TIMESTAMP '<DATETIME>' GROUP BY DATE(eventTime)
    ```
- List the number of overall API calls by Defender for Cloud aggregated by event name:

    ```sql
    SELECT eventName, COUNT(*) AS apiCallsCountByEventName FROM <TABLE-NAME> 
    WHERE userIdentity.arn LIKE 'arn:aws:sts::<YOUR-ACCOUNT-ID>:assumed-role/CspmMonitorAws/MicrosoftDefenderForClouds_<YOUR-AZURE-TENANT-ID>' 
    AND eventTime > TIMESTAMP '<DATETIME>' GROUP BY eventName     
    ```
- List the number of overall API calls by Defender for Cloud aggregated by region:

    ```sql
    SELECT awsRegion, COUNT(*) AS apiCallsCountByRegion FROM <TABLE-NAME> 
    WHERE userIdentity.arn LIKE 'arn:aws:sts::<YOUR-ACCOUNT-ID>:assumed-role/CspmMonitorAws/MicrosoftDefenderForClouds_<YOUR-AZURE-TENANT-ID>' 
    AND eventTime > TIMESTAMP '<DATETIME>' GROUP BY awsRegion
    ```

### Tips for GCP connector problems

- Make sure that the GCP Cloud Shell script finished successfully.
- Make sure that GKE clusters are successfully connected to Azure Arc-enabled Kubernetes.
- Make sure that Azure Arc endpoints are in the firewall allowlist. The GCP connector makes API calls to these endpoints to fetch the necessary onboarding files.
- If the onboarding of GCP projects fails, make sure you have `compute.regions.list` permission and Microsoft Entra permission to create the service principal for the onboarding process. Make sure that the GCP resources `WorkloadIdentityPoolId`, `WorkloadIdentityProviderId`, and `ServiceAccountEmail` are created in the GCP project.

#### Defender API calls to GCP

When you onboard your GCP single project or organization, the discovery service in Defender for Cloud starts an immediate scan of your environment. The discovery service executes API calls to various service endpoints in order to retrieve all resources that Azure helps secure.

After this initial scan, the service continues to periodically scan your environment at the interval that you configured during onboarding.

To get the number of native API calls that Defender for Cloud executed:

1. Go to **Logging** &gt; **Log Explorer**.
2. Filter the dates as you want (for example, **1d**).
3. To show API calls that Defender for Cloud executed, run this query:

    ```json
    protoPayload.authenticationInfo.principalEmail : "microsoft-defender"
    ```

Refer to the histogram to see the number of calls over time.