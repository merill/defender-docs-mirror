---
layout: Conceptual
title: Connect Microsoft Sentinel to Amazon Web Services to Ingest AWS EKS Logs | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-aws-eks
breadcrumb_path: breadcrumb/toc.json
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
description: Use the Amazon Web Services (AWS) S3-based Elastic Kubernetes Service (EKS) connector to ingest AWS EKS audit logs, collected in AWS S3 buckets, to Microsoft Sentinel.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 6ac95647-2ebd-8b2e-515d-6d9f76aa9292
document_version_independent_id: 8b2b4b75-4861-83ab-ef7f-6efc3d0bf546
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-aws-eks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-aws-eks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-aws-eks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: a67f4a8f-0354-6f88-a867-827f69b9d613
---

# Connect Microsoft Sentinel to Amazon Web Services to Ingest AWS EKS Logs | Microsoft Learn

Use the Amazon Web Services (AWS) S3-based Elastic Kubernetes Service (EKS) connector to ingest AWS EKS audit logs, collected in AWS S3 buckets, to Microsoft Sentinel. AWS EKS audit logs are detailed records of API server requests, authentication decisions, and cluster activities within your Kubernetes clusters. These records contain information such as the time the request was received, the specifics of the request, the user making the request, and the action taken. This log analysis is essential for maintaining the security and compliance of containerized applications running on EKS clusters.

This connector features an *AWS CloudFormation*-based onboarding script to streamline the creation of the AWS resources used by the connector.

Important

- The **Amazon Web Services S3 EKS** data connector is currently in preview. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.
- After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

    If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Overview

The **Amazon Web Services S3 EKS** data connector serves the following use cases:

- **Kubernetes security monitoring and threat detection**: Analyze AWS EKS audit logs to help identify and respond to security threats such as unauthorized access, privilege escalation, and suspicious API calls within your Kubernetes clusters. By ingesting these logs into Microsoft Sentinel, you can use its advanced analytics and threat intelligence to detect and investigate malicious activities targeting your containerized workloads.
- **Compliance and auditing for containerized environments**: AWS EKS audit logs provide detailed records of all API server interactions, which are crucial for compliance reporting and auditing purposes in containerized environments. The connector ensures that these audit logs are available within Microsoft Sentinel for easy access and analysis, helping meet regulatory requirements for container security.
- **DevSecOps and cluster governance**: Monitor developer activities, resource access patterns, and configuration changes within your EKS clusters to ensure proper governance and security practices in your DevSecOps workflows.

This article explains how to configure the Amazon Web Services S3 EKS connector. The process of setting it up has two parts: the AWS side and the Microsoft Sentinel side. Each side's process produces information used by the other side. The exchange of configuration details between the AWS setup and the Microsoft Sentinel setup creates secure communication.

## Prerequisites

- You must have write permission on the Microsoft Sentinel workspace.
- Install the Amazon Web Services solution from the **Content Hub** in Microsoft Sentinel. If you already installed an earlier version of the solution, update the solution in the content hub to ensure you have the latest version that includes this connector. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).
- You must have an existing AWS EKS cluster with audit logging enabled, or the ability to enable audit logging on your EKS cluster during the setup process.
- You must have appropriate AWS IAM permissions to:

    - Create IAM roles and policies
    - Create S3 buckets and configure bucket policies
    - Create SQS queues and configure queue policies
    - Create CloudFormation stacks
    - Configure EKS cluster logging settings
    - Create Kinesis Data Firehose delivery streams
    - Create Lambda functions

## Enable and configure the Amazon Web Services S3 EKS connector

To enable and configure the connector, complete the following tasks:

- **In your AWS environment:**

    The **Amazon Web Services S3 EKS** connector page in Microsoft Sentinel provides downloadable AWS CloudFormation stack templates that automate the following AWS tasks:

    - Configure your AWS EKS cluster to send audit logs to **CloudWatch Logs**.
    - Create a **Kinesis Data Firehose delivery stream** to transform and deliver logs from CloudWatch to S3.
    - Create an **S3 bucket** to store the processed audit logs.
    - Create a **Simple Queue Service (SQS) queue** to provide notification when new log files are created in S3.
    - Create a **web identity provider** to authenticate users to AWS through OpenID Connect (OIDC).
    - Create an **assumed role** to grant permissions to users authenticated by the OIDC web identity provider to access your AWS resources.
    - Attach the appropriate **IAM permissions policies** to grant the assumed role access to the appropriate resources (S3 bucket, SQS).
    - Create a **Lambda function** to transform EKS audit logs into the format expected by Microsoft Sentinel.
- **In Microsoft Sentinel:**

    - Configure the **Amazon Web Services S3 EKS Connector** in the Microsoft Sentinel portal by adding **log collectors** that poll the SQS queue and retrieve log data from the S3 bucket. For more information, see Add log collectors.

## Set up the AWS environment

To simplify the onboarding process, the **Amazon Web Services S3 EKS** connector page in Microsoft Sentinel provides downloadable templates for use with the AWS CloudFormation service. The CloudFormation service uses these templates to automatically create resource stacks in AWS. These stacks include the resources described in this article, along with credentials, permissions, and policies.

Note

Use the automatic setup process. For special cases, see the [manual setup instructions](connect-aws-configure-environment#manual-setup).

### Prepare the template files

To run the script that sets up the AWS environment, use the following steps:

1. In the Azure portal, from the Microsoft Sentinel navigation menu, expand **Configuration**, and select **Data connectors**.

    In the Defender portal, from the quick launch menu, expand **Microsoft Sentinel &gt; Configuration** and select **Data connectors**.
2. Select **Amazon Web Services S3 EKS** from the list of data connectors.

    If you don't see the connector, install the Amazon Web Services solution from the **Content hub** under **Content management** in Microsoft Sentinel, or update the solution to the latest version.
3. In the details pane for the connector, select **Open connector page**.

    ![Screenshot of data connectors gallery showing AWS S3 EKS connector.](media/connect-aws-s3-waf/find-aws-waf-connector.png)
4. In the **Configuration** section, under **1. AWS CloudFormation Deployment**, select the [AWS CloudFormation Stacks](https://aka.ms/awsCloudFormationLink#/stacks/create) link. This action opens the AWS console in a new browser tab.
5. Return to the tab of the portal where you have Microsoft Sentinel open. Select **Download** under *Template 1: OpenID Connect authentication deployment* to download the template that creates the OIDC web identity provider. The template is downloaded as a JSON file to your designated downloads folder.

    Note

    If you already have an OIDC web identity provider from a previous AWS connector setup, skip this step.
6. Select **Download** under *Template 2: AWS EKS resources deployment* to download the template that creates the other AWS resources. The template is downloaded as a JSON file to your designated downloads folder.

    ![Screenshot of AWS S3 EKS connector configuration page.](media/connect-aws-s3-waf/configure-connector.png)

### Create AWS CloudFormation stacks

Return to the AWS Console browser tab, which is open to the AWS CloudFormation page for creating a stack.

If you're not already signed in to AWS, sign in now. You're redirected to the AWS CloudFormation page.

#### Create the OIDC web identity provider

Important

If you already have the OIDC web identity provider from a previous AWS connector setup, skip this step and proceed to Create the remaining AWS resources.If you already have an OIDC Connect provider set up for Microsoft Defender for Cloud, add Microsoft Sentinel as an audience to your existing provider (Commercial: `api://1462b192-27f7-4cb9-8523-0f4ecb54b47e`, Government:`api://d4230588-5f84-4281-a9c7-2c15194b28f7`). Don't try to create a new OIDC provider for Microsoft Sentinel.

Follow the instructions on the AWS Console page for creating a new stack.

1. Specify a template and upload a template file.
2. Select **Choose file** and locate the *Template 1: OpenID connect authentication deployment.json* file you downloaded.
3. Choose a name for the stack.
4. Advance through the rest of the process and create the stack.

#### Create the remaining AWS resources

1. Return to the AWS CloudFormation stacks page and create a new stack.
2. Select **Choose file** and locate the *Template 2: AWS EKS resources deployment.json* file you downloaded.
3. Choose a name for the stack.
4. When prompted, enter the following parameters:

    - **EKSClusterName**: Enter the name of your existing EKS cluster.
    - **Microsoft Sentinel Workspace ID**: To find your Workspace ID:
        - In the Azure portal, in the Microsoft Sentinel navigation menu, expand **Configuration** and select **Settings**. Select the **Workspace settings** tab and find the Workspace ID on the Log Analytics workspace page.
        - In the Defender portal, in the quick launch menu, expand **System** and select **Settings**. Select **Microsoft Sentinel**, then select **Log Analytics settings** under **Settings for `[WORKSPACE_NAME]`**. Find the Workspace ID on the Log Analytics workspace page, which opens in a new browser tab.
    - **BucketName**: Enter a unique name for the S3 bucket where EKS audit logs are stored.
    - **SentinelSQSQueueName**: Enter a name for the SQS queue (default: MicrosoftSentinelEKSSqs).
    - **AwsRoleName**: Enter a name for the IAM role (must start with "OIDC\_", default: OIDC\_MicrosoftSentinelRoleEKS).
5. Advance through the rest of the process and create the stack.
6. After the stack creation is complete, go to the **Outputs** section of the CloudFormation stack and note the following values:

    - **SentinelRoleArn**: The ARN of the IAM role created for Microsoft Sentinel access.
    - **SentinelSQSQueueURL**: The URL of the SQS queue.
    - **Step1EnableEKSAuditLogging**: AWS CLI command to enable EKS audit logging.
    - **Step2CreateSubscriptionFilter**: AWS CLI command to create the CloudWatch Logs subscription filter.

### Enable EKS audit logging and configure log streaming

After creating the CloudFormation stacks, enable audit logging on your EKS cluster and configure log streaming:

1. If audit logging isn't already enabled on your EKS cluster, run the command provided in the **Step1EnableEKSAuditLogging** output from the CloudFormation stack.
2. Wait about five minutes for audit logs to start appearing in CloudWatch Logs.
3. Run the command provided in the **Step2CreateSubscriptionFilter** output to create a subscription filter that streams audit logs from CloudWatch to the Kinesis Data Firehose delivery stream.
4. The Lambda function automatically transforms the EKS audit logs into the format expected by Microsoft Sentinel and delivers them to S3, where they trigger SQS notifications for ingestion.

## Add log collectors

When you create the resource stacks and configure EKS audit logging, return to the browser tab open to the data connector page in Microsoft Sentinel, and begin the second part of the configuration process.

1. In the **Configuration** section, under **2. Connect new collectors**, select **Add new collector**.

    [![Screenshot of second part of AWS EKS connector configuration.](media/connect-aws-s3-waf/add-new-collector.png)](media/connect-aws-s3-waf/add-new-collector.png#lightbox)
2. Enter the role ARN of the IAM role that you created. Use the value from the **SentinelRoleArn** output of your CloudFormation stack (for example, `arn:aws:iam::{AWS_ACCOUNT_ID}:role/OIDC_MicrosoftSentinelRoleEKS`).
3. Enter the SQS queue URL that you created. Use the value from the **SentinelSQSQueueURL** output of your CloudFormation stack (for example, `https://sqs.{AWS_REGION}.amazonaws.com/{AWS_ACCOUNT_ID}/MicrosoftSentinelEKSSqs`).
4. Select **Connect** to add the collector. This action creates a data collection rule for the Azure Monitor Agent to retrieve the logs and ingest them into the dedicated *AWSEKSLogs\_CL* table in your Log Analytics workspace.

    ![Screenshot of adding new collector for EKS logs.](media/connect-aws-s3-waf/enter-collector-details.png)

## Verify data ingestion

Use the following steps to verify that EKS audit log data is being ingested into your Microsoft Sentinel workspace.

1. After setting up the connector, go to the **Logs** page (or the **Advanced hunting** page in the Defender portal) and run the following query. If you get any results, the connector is working properly.

    ```kusto
    AWSEKSLogs_CL
    | take 10
    ```
2. You can also run more specific queries to explore your EKS audit data.

    ```kusto
    // View recent EKS audit events by verb (API action)
    AWSEKSLogs_CL
    | where TimeGenerated > ago(1h)
    | summarize count() by Verb
    | order by count_ desc
    ```

    ```kusto
    // Monitor authentication decisions
    AWSEKSLogs_CL
    | where TimeGenerated > ago(24h)
    | where AuthDecision != ""
    | summarize count() by AuthDecision, User
    | order by count_ desc
    ```

    ```kusto
    // Track failed requests (non-200 response codes)
    AWSEKSLogs_CL
    | where TimeGenerated > ago(24h)
    | where ResponseCode != 200
    | project TimeGenerated, User, Verb, ObjectRef, ResponseCode, SourceIPs
    | order by TimeGenerated desc
    ```

## Schema reference

The EKS audit logs ingest into the **AWSEKSLogs\_CL** table with the following schema:

| Column | Type | Description |
| --- | --- | --- |
| TimeGenerated | datetime | The time when the audit event was generated |
| AwsAccountId | string | AWS account ID where the EKS cluster is located |
| Region | string | AWS region where the EKS cluster is located |
| ClusterName | string | Name of the EKS cluster |
| Verb | string | The HTTP verb associated with the API request (GET, POST, PUT, DELETE, etc.) |
| User | string | Information about the user making the request |
| SourceIPs | dynamic | Array of source IP addresses from which the request originated |
| UserAgent | string | User agent string of the client making the request |
| ObjectRef | string | Reference to the Kubernetes object being accessed |
| ResponseCode | int | HTTP response code for the API request |
| Stage | string | Stage of the request processing (RequestReceived, ResponseStarted, ResponseComplete, Panic) |
| AuthDecision | string | Authorization decision made by the API server |
| RawEvent | dynamic | Complete raw audit event data for advanced analysis |

## Troubleshooting

### Common issues and solutions

The following common issues and solutions can help you troubleshoot connector setup problems.

- **No data appears in AWSEKSLogs\_CL table:**

    - Verify that EKS audit logging is enabled on your cluster.
    - Check that the CloudWatch Logs subscription filter is correctly configured.
    - Ensure the Lambda function processes logs without errors. Check CloudWatch Logs for Lambda function logs.
    - Verify that S3 bucket notifications are configured correctly to trigger SQS messages.
- **CloudFormation stack creation fails:**

    - Ensure you have sufficient IAM permissions to create all required resources.
    - Check that the EKS cluster name you provided exists in your account.
    - Verify that the S3 bucket name is globally unique.
- **Authentication errors:**

    - Verify that the OIDC web identity provider is correctly configured.
    - Ensure the IAM role permissions are sufficient for accessing S3 and SQS resources.
    - Check that the workspace ID used in the CloudFormation template matches your Microsoft Sentinel workspace.

### Advanced monitoring

If you haven't already done so, implement data connector health monitoring so that you can know when connectors aren't receiving data or have other issues. For more information, see [Monitor the health of your data connectors](monitor-data-connector-health).