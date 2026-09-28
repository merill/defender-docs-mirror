---
layout: Conceptual
title: Troubleshoot AWS S3 connector issues - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/aws-s3-troubleshoot
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
description: Troubleshoot AWS S3 connector issues in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: troubleshooting
ms.date: 2022-09-08T00:00:00.0000000Z
locale: en-us
document_id: bdbfc274-253e-09d5-e0db-80a7ccd57a86
document_version_independent_id: ed1c1cfa-b670-0013-a31c-fa3bbb9e19fc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/aws-s3-troubleshoot.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/aws-s3-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/aws-s3-troubleshoot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 77911e70-3c1e-5a06-80dd-7b827fd2e38d
---

# Troubleshoot AWS S3 connector issues - Microsoft Sentinel | Microsoft Learn

The Amazon Web Services (AWS) S3 connector allows you to ingest AWS service logs, collected in AWS S3 buckets, to Microsoft Sentinel. The types of logs we currently support are AWS CloudTrail, VPC Flow Logs, and AWS GuardDuty.

This article describes how to quickly identify the cause of issues occurring with the AWS S3 connector so you can find the steps needed to resolve the issues.

Learn how to [connect Microsoft Sentinel to Amazon Web Services to ingest AWS service log data](connect-aws?tabs=s3).

## Microsoft Sentinel doesn’t receive data from the Amazon Web Services S3 connector or one of its data types

The logs for the AWS S3 connector (or one of its data types) aren’t visible in the Microsoft Sentinel workspace for more than 30 minutes after the connector was connected.

Before you search for a cause and solution, review these considerations:

- It can take around 20-30 minutes from the moment the connector is connected until data is ingested into the workspace.
- The connector's connection status indicates that a collection rule exists; it doesn't indicate that data was ingested. If the status of the Amazon Web Services S3 connector is green, there's a collection rule for one of the data types, but still no data.

### Determine the cause of your problem

In this section, we cover these causes:

1. The AWS S3 connector permissions policies aren't set properly.
2. The data isn't ingested to the S3 bucket in AWS.
3. The Amazon Simple Queue Service (SQS) in the AWS cloud doesn't receive notifications from the S3 bucket.
4. The data cannot be read from the SQS/S3 in the AWS cloud. With GuardDuty logs, the issue is caused by wrong KMS permissions.

### Cause 1: The AWS S3 connector permissions policies aren't set properly

This issue is caused by incorrect permissions in the AWS environment.

### Create permissions policies

You need permissions policies to deploy the AWS S3 data connector. Review the [required permissions](https://github.com/Azure/Azure-Sentinel/blob/master/DataConnectors/AWS-S3/AwsRequiredPolicies.md) and set the relevant permissions.

## Cause 2: The relevant data doesn't exist in the S3 bucket

The relevant logs don't exist in the S3 bucket.

### Solution: Search for logs and export logs if needed

1. In AWS, open the S3 bucket, search for the relevant folder according to the required logs, and check if there are any log files inside the folder.
2. If the data doesn't exist, there’s an issue with the AWS configuration. In this case, you need to [configure an AWS service to export logs to an S3 bucket](connect-aws-configure-environment#configure-aws-services-to-export-logs-to-an-s3-bucket).

### Cause 3: The S3 data didn't arrive at the SQS

The data wasn't successfully transferred from S3 to the SQS.

### Solution: Verify that the data arrived and configure event notifications

1. In AWS, open the relevant SQS.
2. In the **Monitoring** tab, you should see traffic in the **Number Of Messages Sent** widget. If there's no traffic in the SQS, there's an AWS configuration problem.
3. Make sure that the event notifications definition for the SQS includes the correct data filters (prefix and suffix).
    1. To see the event notifications, in the S3 bucket, select the **Properties** tab, and locate the **Event notifications** section.
    2. If you can’t see this section, create it.
    3. Make sure that the SQS has the relevant policies to get the data from the S3 bucket. The SQS must contain this policy in the **Access policy** tab.

### Cause 4: The SQS didn't read the data

The SQS didn't successfully read the S3 data.

### Solution: Verify that the SQS reads the data

1. In AWS, open the relevant SQS.
2. In the **Monitoring** tab, you should see traffic in the **Number Of Messages Deleted** and **Number Of Messages Received** widgets.
3. One spike of data isn't enough. Wait until there's enough data (several spikes), and then check for issues.
4. If at least one of the widgets is empty, check the health logs by running this query:

    ```kusto
    SentinelHealth 
    | where TimeGenerated > ago(1d)
    | where SentinelResourceKind in ('AmazonWebServicesCloudTrail', 'AmazonWebServicesS3')
    | where OperationName == 'Data fetch failure summary'
    | mv-expand TypeOfFailureDuringHour = ExtendedProperties["FailureSummary"]
    | extend StatusCode = TypeOfFailureDuringHour["StatusCode"]
    | extend StatusMessage = TypeOfFailureDuringHour["StatusMessage"]
    | project SentinelResourceKind, SentinelResourceName, StatusCode, StatusMessage, SentinelResourceId, TypeOfFailureDuringHour, ExtendedProperties
    ```
5. Make sure that the health feature is enabled:

    ```kusto
    SentinelHealth 
    | take 20
    ```
6. If the health feature isn’t enabled, [enable it](enable-monitoring).

## Data from the AWS S3 connector (or one of its data types) is seen in Microsoft Sentinel with a delay of more than 30 minutes

This issue usually happens when Microsoft can’t read files in the S3 folder. Microsoft can't read the files because they're either encrypted or in the wrong format. In these cases, many retries eventually cause ingestion delay.

### Determine the cause of your problem

In this section, we cover these causes:

- Log encryption isn't set up correctly
- Event notifications aren't defined correctly
- Health errors or health disabled

### Cause 1: Log encryption isn't set up correctly

If the logs are fully or partially encrypted by the Key Management Service (KMS), Microsoft Sentinel might not have permission for this KMS to decrypt the files.

### Solution: Check log encryption

Make sure that Microsoft Sentinel has permission for this KMS to decrypt the files. Review the [required KMS permissions](https://github.com/Azure/Azure-Sentinel/blob/master/DataConnectors/AWS-S3/AwsRequiredPolicies.md#sqs-policy) for the GuardDuty and CloudTrail logs.

### Cause 2: Event notifications aren't configured correctly

When you configure an Amazon S3 event notification, you must specify which supported event types Amazon S3 should send the notification to. If an event type that you didn't specify exists in your Amazon S3 bucket, Amazon S3 doesn't send the notification.

### Solution: Verify that event notifications are defined properly

To verify that the event notifications from S3 to the SQS are defined properly, check that:

- The notification is defined from the specific folder that includes the logs, and not from the main folder that contains the bucket.
- The notification is defined with the *.gz* suffix. For example:

### Cause 3: Health errors or health disabled

There might be errors in the health logs, or the health feature might not be enabled.

### Solution: Verify that there are no errors in the health logs and enable health

1. Verify that there are no errors in the health logs by running this query:

    ```kusto
    SentinelHealth
    | where TimeGenerated between (ago(startTime)..ago(endTime))
    | where SentinelResourceKind  == "AmazonWebServicesS3"
    | where Status != "Success"
    | distinct TimeGenerated, OperationName, SentinelResourceName, Status, Description
    ```
2. Make sure that the health feature is enabled:

    ```kusto
    SentinelHealth 
    | take 20
    ```
3. If the health feature isn’t enabled, [enable it](enable-monitoring).

    See more information on the following items used in the preceding example, in the Kusto documentation:

    - [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***mv-expand*** operator](/en-us/kusto/query/mv-expand-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)

    For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

    Other resources:

    - [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
    - [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)