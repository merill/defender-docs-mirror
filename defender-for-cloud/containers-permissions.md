---
layout: Conceptual
title: Cloud IAM permissions for Defender for Containers on AWS and GCP - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/containers-permissions
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
description: Reference of cloud IAM roles and permissions required to onboard and operate Microsoft Defender for Containers in AWS (EKS) and Google Cloud (GKE) environments.
ms.topic: reference
ms.date: 2025-03-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 81ef5fb5-93f7-9113-ecaf-c6cc73734a3d
document_version_independent_id: 3817f1e3-c797-db28-01ad-76a6637be35e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/containers-permissions.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/containers-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/containers-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
platformId: 69a76ed3-2e5e-3204-8faf-647647b15844
---

# Cloud IAM permissions for Defender for Containers on AWS and GCP - Microsoft Defender for Cloud | Microsoft Learn

This article describes the cloud IAM roles and permissions required to onboard and operate Microsoft Defender for Containers in Amazon Elastic Kubernetes Service (EKS) and Google Kubernetes Engine (GKE) environments.

These permissions apply to cloud connectors, Azure Arc provisioning, agentless threat protection, and registry integration features.

## Permissions required by feature

| Defender for Containers feature | Component | Required roles |
| --- | --- | --- |
| [GKE runtime protection](support-matrix-defender-for-containers?tabs=gcprt#runtime-protection-features)[GKE workload hardening](support-matrix-defender-for-containers?tabs=gcpspm#security-posture-management-features)[Runtime vulnerability assessment (optional)](support-matrix-defender-for-containers?tabs=gcpva#vulnerability-assessment-va-features) | GKE Arc provisioning, for the Defender agent and Azure Policy agent | Azure Arc role: **Defender Kubernetes Agent Operator**GCP predefined role: [**Kubernetes Engine Admin**](https://cloud.google.com/iam/docs/understanding-roles#container.admin)OR[**Kubernetes Engine Viewer**](https://cloud.google.com/iam/docs/understanding-roles#container.viewer), if only agentless threat protection and/or the Kubernetes API access extension are enabled |
| [EKS runtime protection](support-matrix-defender-for-containers?tabs=awsrt#runtime-protection-features)[EKS workload hardening](support-matrix-defender-for-containers?tabs=awsspm#security-posture-management-features)[Runtime vulnerability assessment (optional)](support-matrix-defender-for-containers?tabs=awsva#vulnerability-assessment-va-features) | EKS Arc provisioning, for the Defender agent and Azure Policy agent | Azure Arc role: **Defender Kubernetes Agent Operator**AWS role: **AzureDefenderKubernetesRole** |
| [GKE control plane hardening - Agentless threat protection](support-matrix-defender-for-containers?tabs=gcpspm#security-posture-management-features) | GKE AuditLogs provisioning | See GCP Agentless threat protection permissions |
| [EKS control plane hardening - Agentless threat protection](support-matrix-defender-for-containers?tabs=awsspm#security-posture-management-features) | AWS AuditLogs provisioning | See AWS Agentless threat protection permissions |

### Azure Arc provisioning role for EKS and GKE

The Azure Arc built-in role **Defender Kubernetes Agent Operator** to provision the Defender agent and Azure policy agent has the following permissions:

- Microsoft.Authorization/\*/read
- Microsoft.Insights/alertRules/\*
- Microsoft.Resources/deployments/\*
- Microsoft.Resources/subscriptions/resourceGroups/read
- Microsoft.Resources/subscriptions/resourceGroups/write
- Microsoft.Resources/subscriptions/operationresults/read
- Microsoft.Resources/subscriptions/read
- Microsoft.KubernetesConfiguration/extensions/write
- Microsoft.KubernetesConfiguration/extensions/read
- Microsoft.KubernetesConfiguration/extensions/delete
- Microsoft.KubernetesConfiguration/extensions/operations/read
- Microsoft.Kubernetes/connectedClusters/Write
- Microsoft.Kubernetes/connectedClusters/read
- Microsoft.OperationalInsights/workspaces/write
- Microsoft.OperationalInsights/workspaces/read
- Microsoft.OperationalInsights/workspaces/listKeys/action
- Microsoft.OperationalInsights/workspaces/sharedkeys/action
- Microsoft.Kubernetes/register/action
- Microsoft.KubernetesConfiguration/register/action

## AWS Agentless threat protection permissions

- AzureDefenderKubernetesRole (default role name: **MDCContainersK8sRole**):
- sts:AssumeRole
- sts:AssumeRoleWithWebIdentity
- logs:PutSubscriptionFilter
- logs:DescribeSubscriptionFilters
- logs:DescribeLogGroups
- logs:PutRetentionPolicy
- firehose:\*
- iam:PassRole
- eks:UpdateClusterConfig
- eks:DescribeCluster
- eks:CreateAccessEntry
- eks:ListAccessEntries
- eks:AssociateAccessPolicy
- eks:ListAssociatedAccessPolicies
- sqs:\*
- s3:\*
- AzureDefenderKubernetesScubaReaderRole (default role name: **MDCContainersK8sDataCollectionRole**):

    - sts:AssumeRole
    - sts:AssumeRoleWithWebIdentity
    - sqs:ReceiveMessage
    - sqs:DeleteMessage
    - s3:GetObject
    - s3:GetBucketLocation
- AzureDefenderCloudWatchToKinesisRole (default role name: **MDCContainersK8sCloudWatchToKinesisRole**):

    - sts:AssumeRole
    - firehose:\*
- AzureDefenderKinesisToS3Role (default role name: **MDCContainersK8sKinesisToS3Role**):
- MDCContainersAgentlessDiscoveryK8sRole

    - sts:AssumeRoleWithWebIdentity
    - eks:UpdateClusterConfig
    - eks:DescribeCluster
    - eks:CreateAccessEntry
    - eks:ListAccessEntries
    - eks:AssociateAccessPolicy
    - eks:ListAssociatedAccessPolicies
- MDCContainersImageAssessmentRole

    - sts:AssumeRoleWithWebIdentity
    - The permissions of these assumed roles: [AmazonEC2ContainerRegistryPowerUser](https://docs.aws.amazon.com/AmazonECR/latest/userguide/security-iam-awsmanpol#security-iam-awsmanpol-AmazonEC2ContainerRegistryPowerUser) & [AmazonElasticContainerRegistryPublicPowerUser](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonElasticContainerRegistryPublicPowerUser)

## GCP Agentless threat protection permissions

- MicrosoftDefenderContainersDataCollectionRole

    - pubsub.subscriptions.consume
    - pubsub.subscriptions.get
- MicrosoftDefenderContainersRole

    - logging.sinks.list
    - logging.sinks.get
    - logging.sinks.create
    - logging.sinks.update
    - logging.sinks.delete
    - resourcemanager.projects.getIamPolicy
    - resourcemanager.organizations.getIamPolicy
    - iam.serviceAccounts.get
    - iam.workloadIdentityPoolProviders.get (all the logs that go to Pub/Sub)
- MDCCustomRole

    - resourcemanager.folders.get
    - resourcemanager.folders.list
    - resourcemanager.projects.get
    - resourcemanager.projects.list
    - serviceusage.services.enable
    - iam.roles.create
    - iam.roles.list
    - compute.projects.get
    - compute.projects.setCommonInstanceMetadata
- MDCCspmCustomRole

    - resourcemanager.folders.getIamPolicy
    - resourcemanager.folders.list
    - resourcemanager.organizations.get
    - resourcemanager.organizations.getIamPolicy
    - storage.buckets.getIamPolicy
- MDCGkeContainerInventoryCollectionRole

    - container.nodes.proxy
    - container.secrets.list

## Permissions granted in cloud environments

When you onboard AWS or GCP environments to Microsoft Defender for Cloud, a deployment script is generated to create the required IAM roles based on the selected access model:

- **Default Access** supports all current and future extensions of the selected Defender plans.
- **Least Privileged Access** grants only the permissions required to support the currently enabled extensions.

The following tables show the permissions granted to Defender for Containers roles, depending on the selected access model.

### AWS default access

| Role Name | Associated Policies / Permissions | Capabilities |
| --- | --- | --- |
| MDCContainersImageAssessmentRole | AmazonEC2ContainerRegistryPowerUser [AWS permissions list](https://docs.aws.amazon.com/AmazonECR/latest/userguide/security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonEC2ContainerRegistryPowerUser)AmazonElasticContainerRegistryPublicPowerUser [AWS permissions list](https://docs.aws.amazon.com/AmazonECR/latest/public/public-security-iam-awsmanpol.html#public-security-iam-awsmanpol-AmazonElasticContainerRegistryPublicPowerUser) | Agentless container vulnerability assessment. |
| MDCContainersAgentlessDiscoveryK8sRole | eks:DescribeClustereks:UpdateClusterConfigeks:CreateAccessEntryeks:ListAccessEntrieseks:AssociateAccessPolicyeks:ListAssociatedAccessPolicies | Agentless discovery of Kubernetes.Updating EKS clusters to support IP restriction |

### AWS least privileged access

| **Role Name** | **Associated Policies / Permissions** | **Capabilities** |
| --- | --- | --- |
| MDCContainersImageAssessmentRole | AmazonEC2ContainerRegistryReadOnly [AWS permissions list](https://docs.aws.amazon.com/AmazonECR/latest/userguide/security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonEC2ContainerRegistryReadOnly)AmazonElasticContainerRegistryPublicReadOnly [AWS permissions list](https://docs.aws.amazon.com/AmazonECR/latest/public/public-security-iam-awsmanpol.html#public-security-iam-awsmanpol-AmazonElasticContainerRegistryPublicReadOnly) | Agentless container vulnerability assessment. |
| MDCContainersAgentlessDiscoveryK8sRole | eks:DescribeClustereks:UpdateClusterConfig | Agentless discovery of Kubernetes. Updating EKS clusters to support IP restriction |

### GCP default access

| Service Account Name | Associated Roles / Permissions | Capabilities |
| --- | --- | --- |
| mdc-containers-artifact-assess | Roles/storage.objectUser [GCP permissions list](https://cloud.google.com/iam/docs/understanding-roles#storage.objectUser)Roles/artifactregistry.writer [GCP permissions list](https://cloud.google.com/iam/docs/understanding-roles#artifactregistry.writer) | Agentless container vulnerability assessment. |
| mdc-containers-k8s-operator | Roles/container.viewer [GCP permissions list](https://cloud.google.com/iam/docs/understanding-roles#container.viewer)Custom role MDCGkeClusterWriteRole [Custom Role] with permission container.clusters.update | Agentless discovery of KubernetesUpdating GKE clusters to support IP restriction |

### GCP least privileged access

| **Service Account Name** | **Associated Roles / Permissions** | **Current Capabilities** |
| --- | --- | --- |
| mdc-containers-artifact-assess | Roles/artifactregistry.reader [GCP permissions list](https://cloud.google.com/iam/docs/understanding-roles#artifactregistry.reader) Roles/storage.objectViewer [GCP permissions list](https://cloud.google.com/iam/docs/understanding-roles#storage.objectViewer) | Agentless container vulnerability assessment. |
| mdc-containers-k8s-operator | Roles/container.viewer [GCP permissions list](https://cloud.google.com/iam/docs/understanding-roles#container.viewer)Custom role MDCGkeClusterWriteRole with permission container.clusters.update | Agentless discovery of Kubernetes.Updating GKE clusters to support IP restriction |