---
layout: Conceptual
title: Agentless machine scanning in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-agentless-data-collection
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
description: Learn how Defender for Cloud can gather information about multicloud machine without installing an agent.
ms.topic: concept-article
ms.date: 2026-04-19T00:00:00.0000000Z
ms.custom: template-concept
ai-usage: ai-assisted
locale: en-us
document_id: 9ae06eee-a04e-3d24-eb59-aeadaf5a364f
document_version_independent_id: 3f8e91cd-4374-e349-2f29-2971c4ce8d89
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-agentless-data-collection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-agentless-data-collection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-agentless-data-collection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: df05588e-3a66-7d9c-1bf0-12097794a270
---

# Agentless machine scanning in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Agentless machine scanning in Microsoft Defender for Cloud improves the security posture of machines connected to Defender for Cloud.

Agentless scanning doesn't need any installed agents or network connectivity, and doesn't affect machine performance. Agentless machine scanning:

- **Scans endpoint detection and response (EDR) settings**: Scan machines to assess whether they're running an EDR solution, and whether settings are correct if machines integrate with Microsoft Defender for Endpoint. [Learn more](endpoint-detection-response)
- **Scans software inventory**: Scan your [software inventory](/en-us/defender-vulnerability-management/tvm-software-inventory) with integrated Microsoft Defender Vulnerability Management.
- **Scans for vulnerabilities**: [Assess machines for vulnerabilities](auto-deploy-vulnerability-assessment) using integrated Defender Vulnerability Management.
- **Scans for secrets on machines**: Locate plain text secrets in your compute environment with agentless [secrets scanning](secrets-scanning).
- **Scans for malware**: [Scan machines for malware and viruses](agentless-malware-scanning) using [Microsoft Defender Antivirus](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-antivirus-windows).
- **Scans VMs running as Kubernetes nodes**: [Vulnerability assessment and malware scanning is available for VMs running as Kubernetes nodes](kubernetes-nodes-overview) when Defender for Servers Plan 2 or the Defender for Containers plan is enabled. Available in commercial clouds only.

Agentless scanning is available in the following Defender for Cloud plans:

- [Defender Cloud Security Posture Management (CSPM)](concept-cloud-security-posture-management).
- [Defender for Servers Plan 2](defender-for-servers-overview#defender-for-servers-plans).
- Malware scanning is only available in Defender for Servers Plan 2.
- Agentless scanning is available for Azure VMs, AWS EC2 and GCP compute instances connected to Defender for Cloud.

## Agentless scanning architecture

Here's how agentless scanning works:

1. Defender for Cloud takes snapshots of VM disks (root + data disk) and performs an out-of-band, deep analysis of the operating system configuration and file system stored in the snapshot.

    - The copied snapshot remains in the same region as the VM.
    - The scan doesn't affect the VM.
2. After Defender for Cloud gets the necessary metadata from the copied disk, it immediately deletes the copied snapshot of the disk and sends the metadata to relevant Microsoft engines to detect configuration gaps and potential threats. For example, in vulnerability assessment, the analysis is done by Defender Vulnerability Management.
3. Defender for Cloud displays scanning results, which consolidates both the agent-based and agentless results on the Security alerts page.
4. Defender for Cloud analyses disks in a scanning environment that's regional, volatile, isolated, and highly secure. Disk snapshots and data unrelated to the scan aren't stored longer than is necessary to collect the metadata, typically a few minutes.

![Diagram of the process for collecting operating system data through agentless scanning.](media/concept-agentless-data-collection/agentless-scanning-process.png)

## Permissions used by agentless scanning

Defender for Cloud used specific roles and permissions to perform agentless scanning.

- In Azure, these permissions are automatically added to your subscriptions when you enable agentless scanning.
- In AWS, these permissions are [added to the CloudFormation stack in your AWS connector](enable-agentless-scanning-vms#aws).
- In GCP, these permissions are [added to the onboarding script in your GCP connector](enable-agentless-scanning-vms#gcp).

### Azure permissions

The built-in role **VM scanner operator** has read-only permissions for VM disks that are required for the snapshot process. The detailed list of permissions is:

- `Microsoft.Compute/disks/read`
- `Microsoft.Compute/disks/beginGetAccess/action`
- `Microsoft.Compute/disks/diskEncryptionSets/read`
- `Microsoft.Compute/virtualMachines/instanceView/read`
- `Microsoft.Compute/virtualMachines/read`
- `Microsoft.Compute/virtualMachineScaleSets/instanceView/read`
- `Microsoft.Compute/virtualMachineScaleSets/read`
- `Microsoft.Compute/virtualMachineScaleSets/virtualMachines/read`
- `Microsoft.Compute/virtualMachineScaleSets/virtualMachines/instanceView/read`

When coverage for CMK encrypted disks is enabled, more permissions are required:

- `Microsoft.KeyVault/vaults/keys/read`
- `Microsoft.KeyVault/vaults/keys/wrap/action`
- `Microsoft.KeyVault/vaults/keys/unwrap/action`

### AWS permissions

The role **VmScanner** is assigned to the scanner when you enable agentless scanning. This role has the minimal permission set to create and clean up snapshots (scoped by tag) and to verify the current state of the VM. The detailed permissions are:

| Attribute | Value |
| --- | --- |
| SID | **VmScannerDeleteSnapshotAccess** |
| Actions | ec2:DeleteSnapshot |
| Conditions | `"StringEquals":{"ec2:ResourceTag/CreatedBy”:<br>"Microsoft Defender for Cloud"}` |
| Resources | arn:aws:ec2:::snapshot/ |
| Effect | Allow |

| Attribute | Value |
| --- | --- |
| SID | **VmScannerAccess** |
| Actions | ec2:ModifySnapshotAttribute  ec2:DeleteTags  ec2:CreateTags  ec2:CreateSnapshots  ec2:CopySnapshots  ec2:CreateSnapshot |
| Conditions | None |
| Resources | arn:aws:ec2:::instance/  arn:aws:ec2:::snapshot/  arn:aws:ec2:::volume/ |
| Effect | Allow |

| Attribute | Value |
| --- | --- |
| SID | **VmScannerVerificationAccess** |
| Actions | ec2:DescribeSnapshots  ec2:DescribeInstanceStatus |
| Conditions | None |
| Resources | \* |
| Effect | Allow |

| Attribute | Value |
| --- | --- |
| SID | **VmScannerEncryptionKeyCreation** |
| Actions | kms:CreateKey |
| Conditions | None |
| Resources | \* |
| Effect | Allow |

| Attribute | Value |
| --- | --- |
| SID | **VmScannerEncryptionKeyManagement** |
| Actions | kms:TagResource  kms:GetKeyRotationStatus  kms:PutKeyPolicy  kms:GetKeyPolicy  kms:CreateAlias  kms:ListResourceTags |
| Conditions | None |
| Resources | `arn:aws:kms::${AWS::AccountId}: key/ <br> arn:aws:kms:*:${AWS::AccountId}:alias/DefenderForCloudKey` |
| Effect | Allow |

| Attribute | Value |
| --- | --- |
| SID | **VmScannerEncryptionKeyUsage** |
| Actions | kms:GenerateDataKeyWithoutPlaintext  kms:DescribeKey  kms:RetireGrant  kms:CreateGrant  kms:ReEncryptFrom |
| Conditions | None |
| Resources | arn:aws:kms::${AWS::AccountId}: key/ |
| Effect | Allow |

### GCP permissions

During onboarding, a new custom role is created with minimal permissions required to get instances status and create snapshots.

In addition, permissions to an existing GCP KMS role are granted to support scanning disks that are encrypted with CMEK. The roles are:

- roles/MDCAgentlessScanningRole granted to Defender for Cloud’s service account with permissions: compute.disks.createSnapshot, compute.instances.get
- roles/cloudkms.cryptoKeyEncrypterDecrypter granted to Defender for Cloud’s compute engine service agent