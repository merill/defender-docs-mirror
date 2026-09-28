---
layout: Conceptual
title: Enable Agentless Machine Scanning - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-agentless-scanning-vms
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
description: Learn what agentless scanning covers, review supported Azure, AWS, and GCP machines, and enable scanning in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-08-24T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 5fea564e-2239-57ef-2ce0-ef3d69832c1d
document_version_independent_id: 36575e3d-7705-ef4c-1ecb-ce495492a619
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-agentless-scanning-vms.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-agentless-scanning-vms
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-agentless-scanning-vms.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
platformId: 47f722bb-754b-8eb9-0ed1-46f6d81a3011
---

# Enable Agentless Machine Scanning - Microsoft Defender for Cloud | Microsoft Learn

Agentless machine scanning helps you discover vulnerabilities, secrets, malware signals, and software inventory for cloud machines without deploying endpoint agents. In Microsoft Defender for Cloud, this capability runs through your cloud connectors so security teams can scale coverage with low operational overhead and minimal performance impact.

This article explains the supported environments, important coverage limitations, and how to enable and manage scanning for Azure, AWS, and GCP.

Important

Before you enable this feature, review the supported machines and scan coverage, followed by the limitations and unsupported configurations.

Agentless scanning runs once every 24 hours on a nonconfigurable schedule.

## What agentless scanning covers

The following table shows what each capability provides and which plans include it.

| Capability | What it provides | Defender Cloud Security Posture Management | Defender for Servers Plan 2 |
| --- | --- | --- | --- |
| Software inventory | Lists software found on supported machine disks. | Yes | Yes |
| Vulnerability assessment | Identifies known vulnerabilities associated with the discovered software. | Yes | Yes |
| Secrets scanning | Finds plaintext secrets stored on supported machine disks. | Yes | Yes |
| Malware scanning | Detects malicious files and generates security alerts for detected threats. Review Malware scanning coverage and limitations. | No | Yes |

Agentless scanning has one setting for each connected environment, such as an Azure subscription, AWS account, or GCP project. The plans enabled for that environment determine which agentless capabilities are available. You can't turn individual agentless capabilities on or off separately.

Note

Malware scanning of Kubernetes node virtual machines (VMs) requires Defender for Servers Plan 2 or Defender for Containers. This capability is available in commercial clouds only.

## Supported machines and scan coverage

### Scan timing and machine state

| Condition | Coverage |
| --- | --- |
| The machine is running during its scheduled scan | The machine is eligible to be scanned. |
| The machine is stopped or deallocated during its scheduled scan | The machine isn't scanned during that cycle. Results can remain missing or outdated until the machine is running during a later scheduled cycle. |
| Agentless scanning was just enabled or connector permissions were updated | Allow up to 24 hours for the next scheduled scan before troubleshooting missing results. |

### Azure VM requirements

Agentless scanning supports Azure standard VMs and virtual machine scale sets that use flexible orchestration, subject to these limits:

| Requirement | Supported coverage |
| --- | --- |
| Combined size of the operating system disk and all data disks is 4 TB or less | The operating system disk and supported data disks can be scanned. |
| Combined size of the operating system disk and all data disks exceeds 4 TB | Only the operating system disk is scanned, and only when that disk is less than 4 TB. Data disks aren't scanned. |
| The VM has 14 disks or fewer | The VM is within the supported disk-count limit. VMs with more than 14 disks aren't supported. |
| Disks use platform-managed keys | Supported. |
| Managed disks use customer-managed keys | Supported after you grant the additional Key Vault permissions described in Azure VMs with customer-managed keys. |

Caution

For an Azure VM whose combined disk size exceeds 4 TB, agentless findings cover only the operating system disk when that disk is less than 4 TB.

### AWS requirements

Agentless scanning supports:

- Amazon EC2 instances and instances in Auto Scaling groups.
- Unencrypted disks.
- Disks encrypted with platform-managed or customer-managed keys.

Agentless scanning doesn't support Amazon Machine Images (AMIs) that require third-party licensing, including applicable AWS Marketplace images.

### GCP requirements

Agentless scanning supports Compute Engine instances and instance groups, both managed and unmanaged, with Google-managed encryption keys or customer-managed encryption keys (CMEK).

GCP organization policies can prevent Defender for Cloud from creating or accessing the snapshots required for scanning. If no results appear within 24 hours, review [Resolve an agentless scan error for GCP](resolve-disk-scanning-error).

## Malware scanning coverage and limitations

Agentless malware scanning provides periodic, point-in-time visibility rather than continuous or real-time protection. The amount and type of content on a VM can affect scan coverage.

### Compressed package limits

A malware scan can complete with partial VM coverage when a compressed package meets any of these conditions:

| Condition | Partial-coverage threshold |
| --- | --- |
| Compressed package size | Larger than 1 GB |
| Files in a compressed package | More than 10,000 files |
| Nested archive depth | More than five archive levels |

### File-count planning targets

To lower the risk of partial coverage, use these planning targets for the total number of files eligible for malware scanning on the VM:

| Operating system | Planning target |
| --- | --- |
| Windows | Up to approximately 300,000 files |
| Linux | Up to approximately 500,000 files |

Workloads that create or modify approximately 200,000 files or more between scans can also increase the risk of partial coverage.

Important

These file-count targets are planning guidance. They're not service-enforced limits and don't guarantee complete coverage.

### Files that might not be scanned

The following files might not be scanned:

- Empty files.
- Files that are inaccessible or no longer available at scan time.
- Files with unsupported operating-system attributes, including system, offline, operating-system-level compressed, or reparse-point files.

### What partial coverage means

Partial coverage doesn't discard the scan results. The scan reports detections from content that it successfully scanned.

To improve coverage:

- Reduce large file collections where operationally appropriate.
- Extract or split compressed packages that exceed the package thresholds.
- Ensure the scanner can access important files at scan time.

## Limitations and unsupported configurations

Agentless scanning doesn't support the following configurations.

| Category | Unsupported configuration | Coverage consequence |
| --- | --- | --- |
| Azure disk type | `UltraSSD_LRS`, `PremiumV2_LRS`, or Azure Kubernetes Service (AKS) ephemeral OS disks | If any disk attached to the VM uses one of these disk types, the VM isn't scanned. |
| Resource type | Databricks VMs | The VM isn't supported for agentless scanning. |
| File system | UFS (Unix File System), ReFS (Resilient File System), or ZFS (ZFS Member) | If any disk uses one of these file systems, the VM isn't scanned. |
| RAID or block-storage format | OracleASM (Oracle Automatic Storage Management), DRBD (Distributed Replicated Block Device), or `Linux_Raid_Member` | If any disk uses one of these formats, the VM isn't scanned. |
| Integrity mechanism or partition | `DM_Verity_Hash` or swap | If any disk contains one of these configurations, the VM isn't scanned. |

Note

After enabling agentless scanning, verify that results appear for the machines you expect. The setting status alone doesn't confirm that every machine meets the support requirements.

## Before you begin

Verify the following requirements:

- **Plan**: Agentless scanning requires Defender CSPM or Defender for Servers Plan 2. Agentless malware scanning is available only with Defender for Servers Plan 2.
- **Connected environment**: Connect the Azure subscription, AWS account, or GCP project or organization to Defender for Cloud.
- **Machine support**: Confirm that the machine and its disks meet the requirements in Supported machines and scan coverage and aren't listed under Limitations and unsupported configurations.
- **Permissions**: Review the [permissions used by agentless scanning](concept-agentless-data-collection#permissions-used-by-agentless-scanning).
- **Customer-managed encryption**: For Azure disks encrypted with customer-managed keys, grant the extra Key Vault permissions described in Azure VMs with customer-managed keys. AWS and GCP connector setup includes the required permissions for their key-management services.

## Enable agentless scanning

Use the rollout guidance in this section, and then follow the procedure for each cloud environment.

### Plan your rollout

A phased rollout helps you confirm permissions, identify unsupported machines, and establish a repeatable process before enabling agentless scanning in a large environment.

#### Benefits of a phased rollout

- **Find coverage gaps early**: Identify machines that exceed disk limits or use unsupported configurations before broad deployment.
- **Validate permissions**: Confirm that disk snapshots and customer-managed encryption keys can be accessed as expected.
- **Set clear expectations**: Verify which inventory, vulnerability, secrets, and malware results should appear for each enabled plan.
- **Reduce repeated work**: Use the validated connector and permission configuration as the pattern for additional environments.

#### Guidelines for a successful rollout

| Guideline | Recommended approach |
| --- | --- |
| Choose a representative test environment | Include common machine types and any customer-managed encryption, large disks, multiple data disks, or scale sets used in your organization. |
| Review support before enabling | Check disk size, disk count, disk type, file system, encryption, and machine power-state requirements. Record machines that aren't supported. |
| Assess malware content scale | For malware scanning, compare file counts, file-change volume, and compressed packages with the coverage guidance. |
| Define the expected results | Decide which software inventory, vulnerability, secrets, or malware results you expect based on the plan enabled for the environment. |
| Allow for the scan schedule | Wait up to 24 hours after enablement or permission changes before assessing the results. |
| Verify results, not only the setting | Confirm that results appear for the expected test machines. An enabled setting alone doesn't confirm successful coverage. |
| Resolve exceptions before expanding | Correct missing permissions or connector configuration. Document machines that remain outside the supported configuration. |
| Roll out in manageable groups | Enable additional Azure subscriptions, AWS accounts, or GCP projects in batches and verify each batch before continuing. |

#### Recommended rollout sequence

1. Select a representative Azure subscription, AWS account, or GCP project.
2. Review its machines against the supported coverage and limitation tables on this page.
3. If malware scanning is required, review the file-count and compressed-package guidance.
4. Confirm that the required plan, connector, and encryption permissions are in place.
5. Define which results you expect to see for the test machines.
6. Enable agentless scanning and allow up to 24 hours for the scheduled scan.
7. Verify that software inventory or vulnerability results appear. To validate malware scanning, follow [Test agentless malware scanning](test-agentless-malware-scanning).
8. Resolve permission, connector, or support issues.
9. Repeat the process for the next group of subscriptions, accounts, or projects.

### Azure

To enable agentless scanning for an Azure subscription:

Important

If any Azure VM disks use customer-managed keys, also complete Azure VMs with customer-managed keys.

1. In Defender for Cloud, open **Environment settings**.
2. Select the relevant subscription.
3. For **Defender CSPM** or **Defender for Servers Plan 2**, select **Settings**.

    [![Screenshot of the settings link for Defender plans in an Azure subscription.](media/enable-vulnerability-assessment-agentless/defender-plan-settings-azure.png)](media/enable-vulnerability-assessment-agentless/defender-plan-settings-azure.png#lightbox)
4. In **Settings and monitoring**, turn on **Agentless scanning for machines**.

    [![Screenshot of the setting used to turn on agentless scanning for Azure machines.](media/enable-vulnerability-assessment-agentless/turn-on-agentless-scanning-azure.png)](media/enable-vulnerability-assessment-agentless/turn-on-agentless-scanning-azure.png#lightbox)
5. Select **Save**.

Wait up to 24 hours for the next scheduled scan. If results don't appear, use the troubleshooting checklist.

### Azure VMs with customer-managed keys

Azure VMs with disks encrypted by customer-managed keys require extra Key Vault permissions. These permissions let Defender for Cloud create and check a secure copy of the encrypted disk.

Assign permissions to **Microsoft Defender for Cloud Servers Scanner Resource Provider** with application ID `0c7668b5-3260-4ad0-9f53-34ed54fa19b2`.

- **For a key vault that uses access policies:** Grant **Get**, **Wrap Key**, and **Unwrap Key** permissions.
- **For a key vault that uses Azure role-based access control (RBAC):** Assign the [**Key Vault Crypto Service Encryption User**](/en-us/azure/key-vault/general/rbac-guide?preserve-view=true&amp;tabs=azure-cli#azure-built-in-roles-for-key-vault-data-plane-operations) built-in role.

To assign these permissions for multiple Key Vaults, use the [agentless scanning CMK support script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Agentless%20Scanning%20CMK%20support).

### AWS

To enable agentless scanning for an AWS account:

1. In Defender for Cloud, open **Environment settings**.
2. Select the relevant AWS account.
3. For **Defender CSPM** or **Defender for Servers Plan 2**, select **Settings**.

    [![Screenshot of the settings link for Defender plans in an AWS account.](media/enable-vulnerability-assessment-agentless/defender-plan-settings-aws.png)](media/enable-vulnerability-assessment-agentless/defender-plan-settings-aws.png#lightbox)
4. Turn on **Agentless scanning for machines**.

    [![Screenshot of the agentless scanning setting for an AWS account.](media/enable-vulnerability-assessment-agentless/agentless-scan-on-aws.png)](media/enable-vulnerability-assessment-agentless/agentless-scan-on-aws.png#lightbox)
5. Select **Save and Next: Configure Access**.
6. Download the CloudFormation template.
7. Create the CloudFormation stack in AWS by following the on-screen instructions.
8. If you're onboarding an AWS management account, deploy the template as both a stack and a StackSet.
9. Select **Next: Review and generate**, and then select **Update**.

Creating member-account connectors can take up to 24 hours. Software inventory and vulnerability information update automatically after scanning begins.

### GCP

To enable agentless scanning for a GCP project or organization:

1. In Defender for Cloud, open **Environment settings**.
2. Select the relevant GCP project or organization.
3. For **Defender CSPM** or **Defender for Servers Plan 2**, select **Settings**.

    [![Screenshot of selecting a Defender plan for a GCP project.](media/enable-agentless-scanning-vms/gcp-select-plan.png)](media/enable-agentless-scanning-vms/gcp-select-plan.png#lightbox)
4. Set **Agentless scanning** to **On**.

    [![Screenshot of the agentless scanning setting for a GCP project.](media/enable-agentless-scanning-vms/gcp-select-agentless.png)](media/enable-agentless-scanning-vms/gcp-select-agentless.png#lightbox)
5. Select **Save and Next: Configure Access**.
6. Copy and run the onboarding script at the intended GCP organization or project scope.
7. Select **Next: Review and generate**, and then select **Update**.

Allow up to 24 hours for the next scheduled scan. If results don't appear, check whether a GCP organization policy is restricting disk, image, or snapshot access.

## Troubleshoot missing or incomplete results

Agentless scanning runs once every 24 hours. After enabling scanning or changing permissions, allow up to 24 hours before troubleshooting missing results.

### No machines are scanned

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Check the plan | Confirm that Defender CSPM or Defender for Servers Plan 2 is enabled. |
| ☐ | Check the setting | In **Environment settings**, turn on **Agentless scanning for machines**. |
| ☐ | Check the connection | Confirm that the Azure subscription, AWS account, or GCP project or organization is connected to Defender for Cloud. |
| ☐ | Check connector permissions | Confirm that the cloud connector setup completed successfully and includes the required permissions. |
| ☐ | Wait for a scan cycle | Keep the machines running and allow up to 24 hours for results. |

### Some Azure VMs aren't scanned

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Check the power state | Confirm that each affected VM was running during a scheduled scan cycle. |
| ☐ | Count attached disks | VMs with more than 14 disks aren't supported. |
| ☐ | Calculate total disk size | Add the provisioned size of the operating system disk and all data disks. If the total exceeds 4 TB, only an operating system disk smaller than 4 TB can be scanned. |
| ☐ | Check disk types | A VM isn't scanned if any disk uses `UltraSSD_LRS`, `PremiumV2_LRS`, or an AKS ephemeral OS disk. |
| ☐ | Check the resource and storage format | Databricks VMs and the listed unsupported file systems, RAID formats, and integrity mechanisms aren't scanned. |
| ☐ | Check encryption permissions | For disks encrypted with customer-managed keys, verify the required Key Vault permissions. |

### Only the Azure VM operating system disk is scanned

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Calculate total disk size | Add the provisioned size of the operating system disk and all data disks. |
| ☐ | Confirm the expected coverage | If the total exceeds 4 TB, only the operating system disk is scanned, and only when that disk is less than 4 TB. |
| ☐ | Address the remaining coverage | Document the data disks as outside agentless coverage and apply your organization's approved protection method. Don't reconfigure production disks solely to meet the scanning limit. |

### Azure VMs with customer-managed-key encrypted disks aren't scanned

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Find the encryption key | Identify the Key Vault that contains the key used to encrypt the disks. |
| ☐ | Find the scanner identity | Locate **Microsoft Defender for Cloud Servers Scanner Resource Provider** with application ID `0c7668b5-3260-4ad0-9f53-34ed54fa19b2`. |
| ☐ | Grant access-policy permissions | For a key vault that uses access policies, grant **Get**, **Wrap Key**, and **Unwrap Key**. |
| ☐ | Grant Azure RBAC permissions | For a key vault that uses Azure RBAC, assign the **Key Vault Crypto Service Encryption User** role. |
| ☐ | Wait for a scan cycle | Allow up to 24 hours for the next scheduled scan. |

### AWS machines aren't scanned

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Check the connection | Confirm that the AWS account appears as connected in **Environment settings**. |
| ☐ | Check the setting | Confirm that agentless scanning is turned on under Defender CSPM or Defender for Servers Plan 2. |
| ☐ | Update connector permissions | Deploy the latest CloudFormation template and confirm that the deployment succeeds. |
| ☐ | Check management-account deployment | For an AWS management account, deploy the template as both a stack and a StackSet. |
| ☐ | Wait for member connectors | Allow up to 24 hours for member-account connectors to be created. |
| ☐ | Check the AMI | AMIs that require third-party licensing, including applicable AWS Marketplace images, aren't supported. |

### GCP machines aren't scanned

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Check the connection | Confirm that the GCP project or organization appears as connected in **Environment settings**. |
| ☐ | Check the setting | Confirm that agentless scanning is turned on under Defender CSPM or Defender for Servers Plan 2. |
| ☐ | Update connector permissions | Run the current onboarding script at the intended GCP project or organization scope. |
| ☐ | Check the organization policy | Confirm that the policy for Compute Engine disks, images, and snapshots doesn't block Defender for Cloud. |
| ☐ | Resolve a policy block | Follow [Resolve an agentless scan error for GCP](resolve-disk-scanning-error) to update the organization policy. |
| ☐ | Wait for a scan cycle | Allow up to 24 hours for the next scheduled scan. |

### Results are missing or outdated for stopped machines

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Start the machine | Agentless scanning scans only machines that are running during the scheduled scan. |
| ☐ | Wait for updated results | Keep the machine running and allow up to 24 hours for results to update. |

### Malware scan has partial coverage

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Check compressed package size | A package larger than 1 GB can result in partial VM coverage. |
| ☐ | Check the number of files in packages | A compressed package containing more than 10,000 files can result in partial coverage. |
| ☐ | Check nested archives | More than five nested archive levels can result in partial coverage. |
| ☐ | Estimate the total eligible file count | Use approximately 300,000 files for Windows and 500,000 files for Linux as planning targets, not enforced limits. |
| ☐ | Review file-change volume | Creating or modifying approximately 200,000 files or more between scans can increase the risk of partial coverage. |
| ☐ | Check file accessibility | Empty, inaccessible, unavailable, system, offline, operating-system-level compressed, or reparse-point files might not be scanned. |
| ☐ | Improve package coverage | Where operationally appropriate, reduce large file collections and extract or split packages that exceed the compressed-package thresholds. |
| ☐ | Review available detections | Partial coverage doesn't discard detections from content that was scanned successfully. |

### Malware alerts don't appear

| Done | Action | Guidance |
| --- | --- | --- |
| ☐ | Check the plan | Defender for Servers Plan 2 is required. Defender CSPM alone doesn't include malware scanning. |
| ☐ | Check scanning eligibility | Confirm that agentless scanning is on and that the machine meets the support requirements. |
| ☐ | Check other results | Verify whether software inventory or vulnerability results appear for the machine. |
| ☐ | Run a validation test | Malware alerts appear only when a threat is detected. Follow [Test agentless malware scanning](test-agentless-malware-scanning) to validate the feature. |