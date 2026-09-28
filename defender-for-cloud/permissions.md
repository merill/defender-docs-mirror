---
layout: Conceptual
title: User roles and permissions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/permissions
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
description: Learn how Microsoft Defender for Cloud uses role-based access control to assign permissions and identify permitted actions for each role.
ms.topic: limits-and-quotas
ms.date: 2025-03-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5af3d173-bdc2-d461-8283-b446915277ed
document_version_independent_id: e0430106-a3ed-5f41-7455-00a1b69b0519
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/permissions.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 5ee2d4e6-de3a-5a5c-ea84-bd645390c691
---

# User roles and permissions - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud uses [Azure role-based access control (Azure Role-Based Access Control)](/en-us/azure/role-based-access-control/role-assignments-portal) to provide [built-in roles](/en-us/azure/role-based-access-control/built-in-roles). Assign these roles to users, groups, and services in Azure to give them access to resources according to the role's defined access.

Defender for Cloud assesses resource configurations and identifies security issues and vulnerabilities. In Defender for Cloud, view resource information when assigned one of these roles for the subscription or resource group: Owner, Contributor, or Reader.

In addition to the built-in roles, there are two roles specific to Defender for Cloud:

- **Security Reader**: A user in this role has read-only access to Defender for Cloud. The user can view recommendations, alerts, security policies, and security states but can't make changes.
- **Security Admin**: A user in this role has the same access as the Security Reader and can also update security policies and dismiss alerts and recommendations.

Assign the least permissive role needed for users to complete their tasks.

For example, assign the Reader role to users who only need to view security health information of a resource without taking any action. Users with a Reader role can't apply recommendations or edit policies.

## Roles and allowed actions

The following table displays roles and allowed actions in Defender for Cloud.

| **Action** | [Security Reader](/en-us/azure/role-based-access-control/built-in-roles#security-reader)/[Reader](/en-us/azure/role-based-access-control/built-in-roles#reader) | [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)/[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor) | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| --- | --- | --- | --- | --- | --- |
|  |  |  | **(Resource group level)** | **(Subscription level)** | **(Subscription level)** |
| Add/assign initiatives (including regulatory compliance standards) | - | ✔ | - | - | ✔ |
| Edit security policy | - | ✔ | - | - | ✔ |
| Enable / disable Microsoft Defender plans | - | ✔ | - | ✔ | ✔ |
| Dismiss alerts | - | ✔ | - | ✔ | ✔ |
| Apply security recommendations for a resource (Use [Fix](implement-security-recommendations)) | - | - | ✔ | ✔ | ✔ |
| View alerts and recommendations | ✔ | ✔ | ✔ | ✔ | ✔ |
| Exempt security recommendations | - | ✔ | - | - | ✔ |
| Configure email notifications | - | ✔ | ✔ | ✔ | ✔ |
| View GitHub issue and its associated information | ✔ | ✔ | ✔ | ✔ | ✔ |
| Generate GitHub issue + assign to "owner" | - | ✔ | ✔ | ✔ | ✔ |

Note

While the three roles mentioned are sufficient for enabling and disabling Defender for Cloud plans, the Owner role is required to enable all capabilities of a plan.

The specific role required to deploy monitoring components depends on the extension you deploy. Learn more about [monitoring components](monitoring-components).

## Roles used to automatically configure agents and extensions

To allow the Security Admin role to automatically configure agents and extensions used in Defender for Cloud plans, Defender for Cloud uses policy remediation similar to [Azure Policy](/en-us/azure/governance/policy/how-to/remediate-resources). To use remediation, Defender for Cloud needs to create service principals, also called managed identities, that assign roles at the subscription level. For example, the service principals for the Defender for Containers plan are:

| Service Principal | Roles |
| --- | --- |
| Defender for Containers provisioning Azure Kubernetes Service (AKS) Security Profile | Kubernetes Extension ContributorContributorAzure Kubernetes Service ContributorLog Analytics Contributor |
| Defender for Containers provisioning Arc-enabled Kubernetes | Azure Kubernetes Service ContributorKubernetes Extension ContributorContributorLog Analytics Contributor |
| Defender for Containers provisioning Azure Policy for Kubernetes | Kubernetes Extension ContributorContributorAzure Kubernetes Service Contributor |
| Defender for Containers provisioning Policy extension for Arc-enabled Kubernetes | Azure Kubernetes Service ContributorKubernetes Extension ContributorContributor |

## Permissions on AWS

When you onboard an Amazon Web Services (AWS) connector, Defender for Cloud creates roles and assigns permissions on your AWS account. The following table shows the roles and permissions assigned by each plan on your AWS account.

| Defender for Cloud plan | Role created | Permissions assigned on AWS account |
| --- | --- | --- |
| Defender Cloud Security Posture Management (CSPM) | CspmMonitorAws | To discover AWS resources permissions, read all resources except: consolidatedbilling: freetier:  invoicing: payments:  billing: tax:  cur: |
| Defender CSPM  Defender for Servers | DefenderForCloud-AgentlessScanner | To create and clean up disk snapshots (scoped by tag) "CreatedBy": "Microsoft Defender for Cloud" Permissions: ec2:DeleteSnapshot ec2:ModifySnapshotAttribute ec2:DeleteTags ec2:CreateTags ec2:CreateSnapshots ec2:CopySnapshot ec2:CreateSnapshot ec2:DescribeSnapshots ec2:DescribeInstanceStatus Permission to EncryptionKeyCreation kms:CreateKey kms:ListKeys Permissions to EncryptionKeyManagement kms:TagResource kms:GetKeyRotationStatus kms:PutKeyPolicy kms:GetKeyPolicy kms:CreateAlias kms:TagResource kms:ListResourceTags kms:GenerateDataKeyWithoutPlaintext kms:DescribeKey kms:RetireGrant kms:CreateGrant kms:ReEncryptFrom |
| Defender CSPM  Defender for Storage | SensitiveDataDiscovery | Permissions to discover S3 buckets in the AWS account, permission for the Defender for Cloud scanner to access data in the S3 buckets  S3 read only  KMS decrypt  kms:Decrypt |
| CIEM | DefenderForCloud-Ciem  DefenderForCloud-OidcCiem | Permissions for Ciem Discovery sts:AssumeRole sts:AssumeRoleWithSAML sts:GetAccessKeyInfo sts:GetCallerIdentity sts:GetFederationToken sts:GetServiceBearerToken sts:GetSessionToken sts:TagSession |
| Defender for Servers | DefenderForCloud-DefenderForServers | Permissions to configure JIT Network Access: ec2:RevokeSecurityGroupIngress ec2:AuthorizeSecurityGroupIngress ec2:DescribeInstances ec2:DescribeSecurityGroupRules ec2:DescribeVpcs ec2:CreateSecurityGroup ec2:DeleteSecurityGroup ec2:ModifyNetworkInterfaceAttribute ec2:ModifySecurityGroupRules ec2:ModifyInstanceAttribute ec2:DescribeSubnets ec2:DescribeSecurityGroups |
| Defender for Containers |  | See [Defender for Containers AWS permissions](containers-permissions) |
| Defender for Servers | DefenderForCloud-ArcAutoProvisioning | Permissions to install Azure Arc on all EC2 instances using SSM ssm:CancelCommand ssm:DescribeInstanceInformation ssm:GetCommandInvocation ssm:UpdateServiceSetting ssm:GetServiceSetting ssm:GetAutomationExecution ec2:DescribeIamInstanceProfileAssociations ec2:DisassociateIamInstanceProfile ec2:DescribeInstances ssm:StartAutomationExecution iam:GetInstanceProfile iam:ListInstanceProfilesForRole ssm:GetAutomationExecution ec2:DescribeIamInstanceProfileAssociations ec2:DisassociateIamInstanceProfile ec2:DescribeInstances ssm:StartAutomationExecution iam:GetInstanceProfile iam:ListInstanceProfilesForRole |
| Defender CSPM | DefenderForCloud-DataSecurityPostureDB | Permission to Discover RDS instances in AWS account, create RDS instance snapshot,  - List all RDS DBs/clusters  - List all DB/Cluster snapshots  - Copy all DB/cluster snapshots  - Delete/update DB/cluster snapshot with prefix *defenderfordatabases* - List all KMS keys  - Use all KMS keys only for RDS on source account  - List KMS keys with tag prefix *DefenderForDatabases* - Create alias for KMS keys  Permissions required to discover, RDS instances rds:DescribeDBInstances rds:DescribeDBClusters rds:DescribeDBClusterSnapshots rds:DescribeDBSnapshots rds:CopyDBSnapshot rds:CopyDBClusterSnapshot rds:DeleteDBSnapshot rds:DeleteDBClusterSnapshot rds:ModifyDBSnapshotAttribute rds:ModifyDBClusterSnapshotAttribute rds:DescribeDBClusterParameters rds:DescribeDBParameters rds:DescribeOptionGroups kms:CreateGrant kms:ListAliases kms:CreateKey kms:TagResource kms:ListGrants kms:DescribeKey kms:PutKeyPolicy kms:Encrypt kms:CreateGrant kms:EnableKey kms:CancelKeyDeletion kms:DisableKey kms:ScheduleKeyDeletion kms:UpdateAlias kms:UpdateKeyDescription |

## Permissions on GCP

When you onboard a Google Cloud Platforms (GCP) connector, Defender for Cloud creates roles and assigns permissions on your GCP project. The following table shows the roles and permissions assigned by each plan on your GCP project.

| Defender for Cloud plan | Role created | Permission assigned on AWS account |
| --- | --- | --- |
| Defender CSPM | MDCCspmCustomRole | These permissions allow the CSPM role to discover and scan resources within the organization:Allows the role to view and organizations, projects, and folders: resourcemanager.folders.get resourcemanager.folders.list resourcemanager.folders.getIamPolicy resourcemanager.organizations.get resourcemanager.organizations.getIamPolicy storage.buckets.getIamPolicyAllows the autoprovisioning process of new projects and removal of deleted projects: resourcemanager.projects.get resourcemanager.projects.listAllows the role to enable Google Cloud services used for the discovery of resources: serviceusage.services.enableUsed to create and list IAM roles: iam.roles.create iam.roles.listAllows the role to act as a service account and gain permission to resources:iam.serviceAccounts.actAsAllows the role to view project details and set common instance metadata:compute.projects.getcompute.projects.setCommonInstanceMetadata Used to discover and scan AI platform resources within the organization:aiplatform.batchPredictionJobs.listaiplatform.customJobs.listaiplatform.datasets.listaiplatform.datasets.getaiplatform.endpoints.getIamPolicyaiplatform.endpoints.listaiplatform.indexEndpoints.listaiplatform.indexes.listaiplatform.models.listaiplatform.models.getaiplatform.pipelineJobs.listaiplatform.schedules.listaiplatform.tuningJobs.listdiscoveryengine.dataStores.listdiscoveryengine.documents.listdiscoveryengine.engines.listnotebooks.instances.list |
| Defender for Servers | microsoft-defender-for-servers  azure-arc-for-servers-onboard | Read-only access to get and list Compute Engine resources:  compute.viewer iam.serviceAccountTokenCreator osconfig.osPolicyAssignmentAdmin osconfig.osPolicyAssignmentReportViewer |
| Defender for Database | defender-for-databases-arc-ap | Permissions to Defender for databases ARC auto provisioning  compute.viewer  iam.workloadIdentityUser  iam.serviceAccountTokenCreator osconfig.osPolicyAssignmentAdmin osconfig.osPolicyAssignmentReportViewer |
| Defender CSPM  Defender for Storage | data-security-posture-storage | Permission for the Defender for Cloud scanner to discover GCP storage buckets, to access data in the GCP storage buckets  storage.objects.list storage.objects.get storage.buckets.get |
| Defender CSPM  Defender for Storage | data-security-posture-storage | Permission for the Defender for Cloud scanner to discover GCP storage buckets, to access data in the GCP storage buckets storage.objects.list storage.objects.get storage.buckets.get |
| Defender CSPM | microsoft-defender-ciem | Permissions to get details about the organization resource. resourcemanager.folders.getIamPolicy resourcemanager.folders.list resourcemanager.organizations.get resourcemanager.organizations.getIamPolicy storage.buckets.getIamPolicy |
| Defender CSPM  Defender for Servers | MDCAgentlessScanningRole | Permissions for agentless disk scanning: compute.disks.createSnapshot compute.instances.get |
| Defender CSPM  Defender for servers | cloudkms.cryptoKeyEncrypterDecrypter | Permissions to an existing GCP KMS role are granted to support scanning disks that are encrypted with CMEK |
| Defender for Containers |  | See [Defender for Containers GCP permissions](containers-permissions) |