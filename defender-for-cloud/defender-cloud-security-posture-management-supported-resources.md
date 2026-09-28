---
layout: Conceptual
title: AWS and GCP resources supported by Defender CSPM - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-cloud-security-posture-management-supported-resources
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
description: Review the AWS and GCP services and resource types supported by Microsoft Defender CSPM.
ms.topic: reference
ms.date: 2026-09-11T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: f6c82542-d02c-f7d8-4f49-2d458fce65d9
document_version_independent_id: 3475dca1-372d-1841-ee41-45cac9458832
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-cloud-security-posture-management-supported-resources.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-cloud-security-posture-management-supported-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-cloud-security-posture-management-supported-resources.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: 2592f23f-c8d7-ed3d-cab2-5c46c4255c6c
---

# AWS and GCP resources supported by Defender CSPM - Microsoft Defender for Cloud | Microsoft Learn

The following tables list the Amazon Web Services (AWS) and Google Cloud Platform (GCP) services and resource types supported by Microsoft Defender Cloud Security Posture Management (Defender CSPM) after you connect an AWS account or GCP project.

Not every Defender CSPM capability or security recommendation applies to every listed resource type. This list doesn't indicate vulnerability scanning, threat protection, or coverage by a Defender workload protection plan. It also doesn't identify the resources used to calculate Defender CSPM charges. For those resources, see [Defender CSPM billable resources](concept-cloud-security-posture-management#plan-pricing).

## AWS resources

| Service | Resource type |
| --- | --- |
| AWS | AccountAccess keyAWS Marketplace Web Service access keyUser cookie |
| AWS AppSync | GraphQL API |
| AWS Backup | Backup planBackup vault |
| AWS Batch | Job definitionJob queue |
| AWS Certificate Manager (ACM) | Certificate |
| AWS CloudFormation | StackSetStack |
| AWS CloudTrail | Trail |
| AWS CodeArtifact | DomainRepository |
| AWS CodeBuild | Build project |
| AWS CodePipeline | PipelineWebhook |
| AWS Config | AWS Config rule |
| AWS DataSync | Task |
| AWS Database Migration Service | Replication instance |
| AWS Glue | Job |
| AWS IAM Identity Center | Permission set |
| AWS Identity and Access Management (IAM) | IAM user groupCustomer managed policyIAM roleIAM user |
| AWS Key Management Service (AWS KMS) | KMS key |
| AWS Lambda | Function |
| AWS Network Firewall | Firewall |
| AWS Step Functions | State machine |
| AWS WAF | Web ACL |
| Amazon API Gateway | Stage |
| Amazon AppFlow | Flow |
| Amazon AppStream 2.0 | Stack |
| Amazon Athena | Workgroup |
| Amazon Bedrock | AgentCustom modelKnowledge base |
| Amazon CloudFront | Distribution |
| Amazon Cognito | Identity poolUser pool |
| Amazon Comprehend | Entity recognizer |
| Amazon DocumentDB | DB cluster |
| Amazon DynamoDB | Table |
| Amazon DynamoDB Accelerator (DAX) | ClusterDAX cluster |
| Amazon EC2 | Flow logTransit gatewayVirtual private gatewayAmazon Machine Image (AMI)EC2 instanceNetwork ACLElastic network interfaceRoute tableSecurity groupAmazon EBS snapshotSubnetAmazon EBS volumeVPC |
| Amazon EC2 Auto Scaling | Auto Scaling group |
| Amazon ECR | Repository |
| Amazon ECS | Task definitionClusterServiceContainerTask |
| Amazon EFS | File system |
| Amazon EKS | Cluster |
| Amazon EMR | Cluster |
| Amazon ElastiCache | Serverless cacheCache cluster |
| Amazon EventBridge | Event busPipeRule |
| Amazon FSx | Amazon FSx for Lustre file systemAmazon FSx for OpenZFS file systemAmazon FSx for Windows File Server file systemFile system |
| Amazon Kendra | Index |
| Amazon Keyspaces | Table |
| Amazon Kinesis Data Streams | Data stream |
| Amazon Lightsail | BucketBlock storage diskDatabaseInstance |
| Amazon MQ | Broker |
| Amazon MSK | MSK cluster |
| Amazon MemoryDB | Cluster |
| Amazon Neptune | DB instanceDB cluster |
| Amazon OpenSearch Service | OpenSearch Service domainOpenSearch Serverless collection |
| Amazon QuickSight | Amazon QuickSight |
| Amazon RDS | Database connection stringDB instanceDB clusterDB cluster snapshotUnclear/nonstandard RDS identifierDB snapshot |
| Amazon Redshift | Amazon Redshift credentialsCluster |
| Amazon Route 53 | Health checkHosted zone |
| Amazon S3 | Amazon S3 presigned URLAccess PointBucket |
| Amazon SNS | Topic |
| Amazon SQS | Queue |
| Amazon SageMaker AI | AppDomainEndpointModel |
| Amazon VPC | Security group |
| CodeCommit | Repository |
| Codepipeline | Pipeline |
| Elastic Load Balancing | Classic Load BalancerApplication/Network/Gateway Load Balancer |

## GCP resources

| Service | Resource type |
| --- | --- |
| AI custom model | Custom model |
| AlloyDB for PostgreSQL | ClusterInstance |
| App Engine | ApplicationSSL certificateService |
| Artifact Registry | Repository |
| BigQuery | TableDataset |
| Certificate Manager | Certificate |
| Cloud DNS | Managed zone |
| Cloud Deploy | Delivery pipeline |
| Cloud Key Management Service | CryptoKeyKeyRing |
| Cloud Load Balancing | Forwarding ruleExternal or internal Application Load BalancerBackend serviceTarget poolTarget TCP proxy |
| Cloud Run | Service |
| Cloud SQL | Cloud SQL instance |
| Cloud Storage | Bucket |
| Compute Engine | DiskVPC firewall ruleImageManaged instance groupInstance groupVM instanceVPC networkProject metadataSubnet |
| Container Registry | Container Registry repository |
| Dataflow | Job |
| Dataproc | Cluster |
| Datastream | Stream |
| Filestore | Instance |
| Firestore | Database |
| Google Cloud | API keyGoogle Cloud sourceService account keyConvenience valueDomainGroupService accountSpecial groupUserCloud Storage signed URL |
| Google Kubernetes Engine (GKE) | Cluster |
| Identity and Access Management (IAM) | IAM policy binding |
| Memorystore | Memcached instanceRedis instanceRedis Cluster |
| Network | Network interface |
| Pub/Sub | SubscriptionTopic |
| Resource Manager | OrganizationProjectFolder |
| Secret Manager | Secret |
| Spanner | DatabaseInstance |
| Vertex AI | Workbench instanceBatch prediction endpointDatasetEndpointVector Search index |
| Vertex AI Search | Data storeEngine |
| Vertex AI Workbench | Workbench instance |