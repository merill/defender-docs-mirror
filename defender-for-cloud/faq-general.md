---
layout: FAQ
title: Common questions - General questions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-general
summary: >
  <p>This article answers common general questions about Microsoft Defender for Cloud.

  Use this FAQ to quickly find guidance about access, pricing, recommendations, alerts, and multicloud scenarios.</p>
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
description: Frequently asked general questions about Microsoft Defender for Cloud, a product that helps you prevent, detect, and respond to threats
services: defender-for-cloud
ms.topic: faq
ms.date: 2026-06-18T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f6602bae-a1ab-c103-7a1a-5c87dd4487ce
document_version_independent_id: 81da0f08-3d63-b4a5-785d-2133258a9b75
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-general.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-general
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-general.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 044f405f-7793-675d-3d19-34e380bd1ca4
---

# Common questions - General questions - Microsoft Defender for Cloud | Microsoft Learn

This article answers common general questions about Microsoft Defender for Cloud. Use this FAQ to quickly find guidance about access, pricing, recommendations, alerts, and multicloud scenarios.

## General questions

### What is Microsoft Defender for Cloud?

Microsoft Defender for Cloud helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your resources. It provides integrated security monitoring and policy management across your subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.

Defender for Cloud uses monitoring components to collect and store data. For in-depth details, see [Data collection in Microsoft Defender for Cloud](monitoring-components).

### How do I get Microsoft Defender for Cloud?

Microsoft Defender for Cloud is enabled with your Microsoft Azure subscription and accessed from the [Azure portal](https://azure.microsoft.com/features/azure-portal/). To access it, [sign in to the portal](https://portal.azure.com), select **Browse**, and scroll to **Defender for Cloud**.

### Is there a trial version of Defender for Cloud?

Defender for Cloud is free for the first 30 days. Any usage beyond 30 days is automatically charged based on the pricing model. See [Microsoft Defender for Cloud pricing details](https://azure.microsoft.com/pricing/details/defender-for-cloud/). Note that malware scanning in Defender for Storage isn't included in the free 30-day trial and is charged from the first day.

### Which Azure resources are monitored by Microsoft Defender for Cloud?

Microsoft Defender for Cloud monitors the following Azure resources:

- Virtual machines (VMs) (including [Cloud Services](/en-us/azure/cloud-services/cloud-services-choose-me))
- Virtual Machine Scale Sets
- [The many Azure PaaS services listed in the product overview](support-matrix-defender-for-cloud#security-benefits-for-azure-services)

Defender for Cloud also protects [on-premises resources](quickstart-onboard-machines) and multicloud resources, including Amazon AWS and Google Cloud.

### How can I see the current security state of my Azure, multicloud, and on-premises resources?

The **Defender for Cloud Overview** page shows the overall security posture of your environment broken down by Compute, Networking, Storage & data, and Applications. Each resource type has an indicator showing identified security vulnerabilities. Selecting each tile displays a list of security issues identified by Defender for Cloud, along with an inventory of the resources in your subscription.

### What is a security initiative?

A security initiative defines the set of controls (policies) that are recommended for resources within the specified subscription. In Microsoft Defender for Cloud, you assign initiatives for your Azure subscriptions, AWS accounts, and GCP projects according to your company's security requirements and the type of applications or sensitivity of the data in each subscription.

The security policies enabled in Microsoft Defender for Cloud drive security recommendations and monitoring. Learn more in [What are security policies, initiatives, and recommendations?](security-policy-concept).

### Who can modify a security policy?

To modify a security policy, you must be a **Security Administrator** or an **Owner** of that subscription.

To learn how to configure a security policy, see [Setting security policies in Microsoft Defender for Cloud](tutorial-security-policy).

### What is a security recommendation?

Microsoft Defender for Cloud analyzes the security state of your Azure, multicloud, and on-premises resources. When potential security vulnerabilities are identified, recommendations are created. The recommendations guide you through the process of configuring the needed control. Examples are:

- Provisioning of anti-malware to help identify and remove malicious software
- [Network security groups](/en-us/azure/virtual-network/network-security-groups-overview) and rules to control traffic to virtual machines
- Provisioning of a web application firewall to help defend against attacks targeting your web applications
- Deploying missing system updates
- Addressing OS configurations that don't match the recommended baselines

Only recommendations that are enabled in security policies are shown in Defender for Cloud.

### What triggers a security alert?

Microsoft Defender for Cloud automatically collects, analyzes, and fuses log data from your Azure, multicloud, and on-premises resources, the network, and partner solutions like anti-malware and firewalls. When threats are detected, a security alert is created. Examples include detection of:

- Compromised virtual machines communicating with known malicious IP addresses
- Advanced malware detected using Windows error reporting
- Brute force attacks against virtual machines
- Security alerts from integrated partner security solutions such as Anti-Malware or Web Application Firewalls

### What's the difference between threats detected and alerted on by Microsoft Security Response Center versus Microsoft Defender for Cloud?

The Microsoft Security Response Center (MSRC) performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties. When MSRC becomes aware that customer data was accessed by an unlawful or unauthorized party or that the customer's use of Azure doesn't comply with the terms for Acceptable Use, a security incident manager notifies the customer. Notification typically occurs by sending an email to the security contacts specified in Microsoft Defender for Cloud or the Azure subscription owner if a security contact isn't specified.

Defender for Cloud is an Azure service that continuously monitors the customer's Azure, multicloud, and on-premises environment and applies analytics to automatically detect a wide range of potentially malicious activity. These detections are surfaced as security alerts in the workload protection dashboard.

### How can I track who in my organization enabled a Microsoft Defender plan in Defender for Cloud?

Azure Subscriptions might have multiple administrators with permissions to change the pricing settings. To find out which user made a change, use the Azure Activity Log.

![Screenshot of Azure Activity log showing a pricing change event.](media/faq-general/logged-change-to-pricing.png)

If the user's info isn't listed in the **Event initiated by** column, explore the event's JSON for the relevant details.

![Screenshot of Azure Activity log JSON explorer.](media/faq-general/tracking-pricing-changes-in-activity-log.png)

### What happens when one recommendation is in multiple policy initiatives?

Sometimes, a security recommendation appears in more than one policy initiative. If you have multiple instances of the same recommendation assigned to the same subscription, and you create an exemption for the recommendation, it affects all of the initiatives that you have permission to edit.

If you try to create an exemption for that recommendation instance, you'll see one of these two messages:

- If you **have** the necessary permissions to edit both initiatives, you'll see:

    *This recommendation is included in several policy initiatives: [initiative names separated by comma]. Exemptions will be created on all of them.*
- If you **don't have** sufficient permissions on both initiatives, you'll see this message instead:

    *You have limited permissions to apply the exemption on all the policy initiatives, the exemptions will be created only on the initiatives with sufficient permissions.*

### Are there any recommendations that don't support exemption?

The following generally available recommendations don't support exemption:

- All advanced threat protection types should be enabled in SQL managed instance advanced data security settings
- All advanced threat protection types should be enabled in SQL server advanced data security settings
- Audit usage of custom RBAC roles
- Container CPU and memory limits should be enforced
- Container images should be deployed from trusted registries only
- Container with privilege escalation should be avoided
- Containers sharing sensitive host namespaces should be avoided
- Containers should listen on allowed ports only
- Default IP Filter Policy should be Deny
- File integrity monitoring should be enabled on machines
- Immutable (read-only) root filesystem should be enforced for containers
- IoT Devices - Open Ports On Device
- IoT Devices - Permissive firewall policy in one of the chains was found
- IoT Devices - Permissive firewall rule in the input chain was found
- IoT Devices - Permissive firewall rule in the output chain was found
- IP Filter rule large IP range
- Kubernetes clusters should be accessible only over HTTPS
- Kubernetes clusters should disable automounting API credentials
- Kubernetes clusters should not use the default namespace
- Kubernetes clusters should not grant CAPSYSADMIN security capabilities
- Least privileged Linux capabilities should be enforced for containers
- Overriding or disabling of containers AppArmor profile should be restricted
- Privileged containers should be avoided
- Running containers as root user should be avoided
- Services should listen on allowed ports only
- SQL servers should have a Microsoft Entra administrator provisioned
- Usage of host networking and ports should be restricted
- Usage of pod HostPath volume mounts should be restricted to a known list to restrict node access from compromised containers
- Azure API Management APIs should be onboarded to Defender for APIs
- Unused API endpoints should be disabled and removed from Function Apps
- Unused API endpoints should be disabled and removed from Logic Apps
- Authentication should be enabled on API endpoints hosted in Function Apps
- Authentication should be enabled on API endpoints hosted in Logic Apps

### Are there any limitations to Defender for Cloud's identity and access protections?

There are some limitations to Defender for Cloud's identity and access protections:

- Identity recommendations aren't available for subscriptions with more than 6,000 accounts. In these cases, these types of subscriptions are listed under Not applicable tab.
- Identity recommendations aren't available for Cloud Solution Provider (CSP) partner's admin agents.
- Identity recommendations evaluate role assignments, including PIM‑eligible assignments, but do not currently differentiate risk based on PIM activation workflows or approval requirements. This may result in findings that include PIM‑managed identities.
- Identity recommendations don't support Microsoft Entra conditional access policies with included Directory Roles instead of users and groups.

### What operating systems for my EC2 instances are supported?

For a list of Amazon Machine Images (AMIs) with the AWS Systems Manager (SSM) Agent preinstalled, see [AWS docs: AMIs with SSM Agent preinstalled](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent-technical-details.html#ami-preinstalled-agent).

For other operating systems, the SSM Agent should be installed manually using the following instructions:

- [Install SSM Agent for a hybrid environment (Windows)](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-install-managed-win.html)
- [Install SSM Agent for a hybrid environment (Linux)](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-install-managed-linux.html)

### For the CSPM plan, what IAM permissions are needed to discover AWS resources?

The following IAM permissions are needed to discover AWS resources:

| DataCollector | AWS Permissions |
| --- | --- |
| API Gateway | `apigateway:GET` |
| Application Auto Scaling | `application-autoscaling:Describe*` |
| Auto scaling | `autoscaling-plans:Describe*``autoscaling:Describe*` |
| Certificate manager | `acm-pca:Describe*``acm-pca:List*``acm:Describe*``acm:List*` |
| CloudFormation | `cloudformation:Describe*``cloudformation:List*` |
| CloudFront | `cloudfront:DescribeFunction``cloudfront:GetDistribution``cloudfront:GetDistributionConfig``cloudfront:List*` |
| CloudTrail | `cloudtrail:Describe*``cloudtrail:GetEventSelectors``cloudtrail:List*``cloudtrail:LookupEvents` |
| CloudWatch | `cloudwatch:Describe*``cloudwatch:List*` |
| CloudWatch logs | `logs:DescribeLogGroups``logs:DescribeMetricFilters` |
| CodeBuild | `codebuild:DescribeCodeCoverages``codebuild:DescribeTestCases``codebuild:List*` |
| Config Service | `config:Describe*``config:List*` |
| DMS - database migration service | `dms:Describe*``dms:List*` |
| DAX | `dax:Describe*` |
| DynamoDB | `dynamodb:Describe*``dynamodb:List*` |
| Ec2 | `ec2:Describe*``ec2:GetEbsEncryptionByDefault` |
| ECR | `ecr:Describe*``ecr:List*` |
| ECS | `ecs:Describe*``ecs:List*` |
| EFS | `elasticfilesystem:Describe*` |
| EKS | `eks:Describe*``eks:List*` |
| Elastic Beanstalk | `elasticbeanstalk:Describe*``elasticbeanstalk:List*` |
| ELB - elastic load balancing (v1/2) | `elasticloadbalancing:Describe*` |
| Elastic search | `es:Describe*``es:List*` |
| EMR - elastic map reduce | `elasticmapreduce:Describe*``elasticmapreduce:GetBlockPublicAccessConfiguration``elasticmapreduce:List*``elasticmapreduce:View*` |
| GuardDuty | `guardduty:DescribeOrganizationConfiguration``guardduty:DescribePublishingDestination``guardduty:List*` |
| IAM | `iam:Generate*``iam:Get*``iam:List*``iam:Simulate*` |
| KMS | `kms:Describe*``kms:List*` |
| Lambda | `lambda:GetPolicy``lambda:List*` |
| Network firewall | `network-firewall:DescribeFirewall``network-firewall:DescribeFirewallPolicy``network-firewall:DescribeLoggingConfiguration``network-firewall:DescribeResourcePolicy``network-firewall:DescribeRuleGroup``network-firewall:DescribeRuleGroupMetadata``network-firewall:ListFirewallPolicies``network-firewall:ListFirewalls``network-firewall:ListRuleGroups``network-firewall:ListTagsForResource` |
| RDS | `rds:Describe*``rds:List*` |
| RedShift | `redshift:Describe*` |
| S3 and S3Control | `s3:DescribeJob``s3:GetEncryptionConfiguration``s3:GetBucketPublicAccessBlock``s3:GetBucketTagging``s3:GetBucketLogging``s3:GetBucketAcl``s3:GetBucketLocation``s3:GetBucketPolicy``s3:GetReplicationConfiguration``s3:GetAccountPublicAccessBlock``s3:GetObjectAcl``s3:GetObjectTagging``s3:List*` |
| SageMaker | `sagemaker:Describe*``sagemaker:GetSearchSuggestions``sagemaker:List*``sagemaker:Search` |
| Secret manager | `secretsmanager:Describe*``secretsmanager:List*` |
| Simple notification service SNS | `sns:Check*``sns:List*` |
| SSM | `ssm:Describe*``ssm:List*` |
| SQS | `sqs:List*``sqs:Receive*` |
| STS | `sts:GetCallerIdentity` |
| WAF | `waf-regional:Get*``waf-regional:List*``waf:List*``wafv2:CheckCapacity``wafv2:Describe*``wafv2:List*` |

### Is there an API for connecting my GCP resources to Defender for Cloud?

Yes. To create, edit, or delete Defender for Cloud cloud connectors with a REST API, see the details of the [Connectors API](/en-us/rest/api/defenderforcloud-composite/security-connectors?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).

### What GCP regions are supported by Defender for Cloud?

Defender for Cloud supports and scans all available regions on GCP public cloud.

### Does workflow automation support any business continuity or disaster recovery (BCDR) scenarios?

When preparing your environment for BCDR scenarios, where the target resource is experiencing an outage or other disaster, it's the organization's responsibility to prevent data loss by establishing backups according to the guidelines from Azure Event Hubs, Log Analytics workspace, and Logic Apps.

For every active automation, we recommend you create an identical (disabled) automation and store it in a different location. When there's an outage, you can enable these backup automations and maintain normal operations.

Learn more about [Business continuity and disaster recovery for Azure Logic Apps](/en-us/azure/logic-apps/business-continuity-disaster-recovery-guidance).

### What are the costs involved in exporting data?

There's no cost for enabling a continuous export. Costs might be incurred for ingestion and retention of data in your Log Analytics workspace, depending on your configuration there.

Many alerts are only provided when you enable Defender plans for your resources. A good way to preview the alerts in your exported data is to review alerts on the **Alerts** page in Defender for Cloud in the Azure portal.

Learn more about [Log Analytics workspace pricing](https://azure.microsoft.com/pricing/details/monitor/).

Learn more about [Azure Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

For general information about Defender for Cloud pricing, see the [Microsoft Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/).

### Does the continuous export include data about the current state of all resources?

No. Continuous export is built for streaming of **events**:

- **Alerts** received before you enabled export aren't exported.
- **Recommendations** are sent whenever a resource's compliance state changes. For example, when a resource turns from healthy to unhealthy. Therefore, as with alerts, recommendations for resources that haven't changed state since you enabled export won't be exported.
- **Secure score** per security control or subscription is sent when a security control's score changes by 0.01 or more.
- **Regulatory compliance status** is sent when the status of the resource's compliance changes.

### Why are recommendations sent at different intervals?

Different recommendations have different compliance evaluation intervals, which can range from every few minutes to every few days. So, the amount of time that it takes for recommendations to appear in your exports varies.

### How can I get an example query for a recommendation?

To get an example query for a recommendation, open the recommendation in Defender for Cloud, select **Open query**, and then select **Query returning security findings**.

![Screenshot of how to create example query for recommendation.](media/faq-general/recommendation-example-query.png)

### Does continuous export support any business continuity or disaster recovery (BCDR) scenarios?

Continuous export can help you prepare for business continuity and disaster recovery (BCDR) scenarios where the target resource is experiencing an outage or another disaster. However, it's your organization's responsibility to prevent data loss by establishing backups according to guidance for Azure Event Hubs, Log Analytics workspaces, and Azure Logic Apps.

Learn more in [Azure Event Hubs - Geo-disaster recovery](/en-us/azure/event-hubs/event-hubs-geo-dr).

### Can I programmatically update multiple plans on a single subscription simultaneously?

We don't recommend programmatically updating multiple plans on a single subscription simultaneously (via REST API, ARM templates, scripts, etc.). When using the [Microsoft.Security/pricings API](/en-us/rest/api/defenderforcloud-composite/pricings?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true), or any other programmatic solution, you should insert a delay of 10-15 seconds between each request.

### When I enable default access, in which situations do I need to re-run the Cloud Formation template, Cloud Shell script, or Terraform template?

Modifications to Defender for Cloud plans or plan options, including plan features, require rerunning the relevant deployment artifact, such as the CloudFormation template, Cloud Shell script, or Terraform template. This applies regardless of the permission type selected during creation of the security connector. If only regions were changed, as shown in this screenshot, you don't need to rerun the CloudFormation template or Cloud Shell script.

![Screenshot that shows a change in region.](media/faq-general/change-region.png)

When you configure permission types, least privilege access supports features available at the time the template or script was run. New resource types can be supported only by re-running the template or script.

![Screenshot that shows selecting permission types.](media/faq-general/permission-types.png)

### If I change the region or the scan interval for my AWS connector, do I need to re-run the CloudFormation template or Cloud Shell script?

No, if the region or scan interval is changed, there is no need to re-run the CloudFormation template or Cloud Shell script. The changes will be applied automatically.

### How does onboarding an AWS organization or management account to Microsoft Defender for Cloud work?

Onboarding an organization or a management account to Microsoft Defender for Cloud initiates the process of [deploying a StackSet](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-getting-started-create.html). The StackSet includes the necessary roles and permissions. The StackSet also propagates the required permissions across all accounts within the organization.

The included permissions allow Microsoft Defender for Cloud to deliver the selected security features through the created connector in Defender for Cloud. The permissions also allow Defender for Cloud to continuously monitor all accounts that might be added using the auto-provisioning service.

Defender for Cloud is capable of identifying the creation of new management accounts and can leverage the granted permissions to automatically provision an equivalent member security connector for each member account.

Automatic connector creation for newly added accounts is available for organizational onboarding only. Management-account-based connector management also allows Defender for Cloud to edit all member connectors when the management account is edited, delete all member connectors when the management account is deleted, and remove a specific member connector when the corresponding account is removed.

A separate stack must be deployed specifically for the management account.

## Agentless

### Does Agentless scanning scan deallocated VMs?

No. Agentless scanning doesn't scan deallocated VMs.

### Does Agentless scanning scan OS Disk and Data Disks?

Yes. Agentless scanning scans both OS Disk and Data Disks.

### What time of the day my VM is scanned, including start and end time?

Scan timing is dynamic and can change across different accounts and subscriptions.

### Is there any telemetry regarding the copied snapshot?

In AWS, the operations on the customer account are traceable through CloudTrail.

### Which data is collected from snapshots?

Agentless scanning collects data similar to the data an agent collects to perform the same analysis. Raw data, personally identifiable information (PII), and sensitive business data aren't collected. Only metadata results are sent to Defender for Cloud.

### Where are disk snapshots copied?

Analysis of copied disk snapshots takes place in secure environments managed by Defender for Cloud.

The environments are regional across multicloud, so snapshots remain in the same cloud region as the VM they originated from. For example, a snapshot of an EC2 instance in US West is analyzed in that same region, without being copied to another region or cloud.

The scanning environment where disks are analyzed is volatile, isolated, and highly secure.

### How are disk snapshots handled in Microsoft accounts, and what are the agentless scanning platform security and privacy principles?

The agentless scanning platform is audited and compliant with Microsoft's strict security and privacy standards. Some of the measures include (this list isn't comprehensive):

- Physical isolation per region, additional isolation per customer and subscription
- End-to-end (E2E) encryption at rest and in transit
- Disk snapshots are immediately purged after the scan
- Only metadata (that is, security findings) leaves the isolated scanning environment
- The scanning environment is autonomous
- All operations are internally audited

### What are the costs related to agentless scanning?

Agentless scanning is included in the Defender cloud security posture management (Defender CSPM) plan and Defender for Servers Plan 2. There are no additional Defender for Cloud charges when you enable agentless scanning.

Note

AWS charges for retention of disk snapshots. The Defender for Cloud scanning process tries to minimize how long a snapshot is stored in your account, typically up to a few minutes. AWS might charge an overhead cost for snapshot storage. Check with AWS to understand which costs apply to you.

### How can I track AWS costs incurred for the disk snapshots created by Defender for Cloud agentless scanning?

Disk snapshots are created with the `CreatedBy` tag key, and the `Microsoft Defender for Cloud` tag value. The `CreatedBy` tag tracks who created the resource. You need to [activate the tags in the Billing and Cost Management console](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/activate-built-in-tags.html). It can take up to 24 hours for tags to activate.