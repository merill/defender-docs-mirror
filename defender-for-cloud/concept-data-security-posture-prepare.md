---
layout: Conceptual
title: Prerequisites for data security posture management - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-data-security-posture-prepare
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
description: Learn about the requirements and prerequisites for data security posture management in Microsoft Defender for Cloud, including supported resources and regions.
ms.topic: concept-article
ms.date: 2026-04-20T00:00:00.0000000Z
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: a92c3074-387a-0bc3-8939-bc7ce421e4b1
document_version_independent_id: 4f6db80f-be36-d7cc-6f90-9fbb5e5914fb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-data-security-posture-prepare.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-data-security-posture-prepare
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-data-security-posture-prepare.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/a9a12e3a-5d9d-4197-ad96-b826bc774b60
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/6dfd60ec-b0d6-48ef-9c74-057162ea03fb
platformId: 88df285e-5eeb-9fa8-d77e-79dcc937414e
---

# Prerequisites for data security posture management - Microsoft Defender for Cloud | Microsoft Learn

Review the requirements on this page before you set up [data security posture management](concept-data-security-posture) in Microsoft Defender for Cloud.

## Enable sensitive data discovery

Sensitive data discovery is available in the Defender Cloud Security Posture Management (CSPM), Defender for Storage, and Defender for Databases plans.

- When you enable one of the plans, the sensitive data discovery extension turns on as part of the plan.
- If you have existing plans running, the extension is available, but turns off by default.
- Existing plan status shows as "Partial" rather than "Full" if one or more extensions aren't turned on.
- The feature turns on at the subscription level.
- If sensitive data discovery turns on, but Defender CSPM isn't enabled, only storage resources are scanned.
- When a subscription enables Defender CSPM and you scan the same resources with Purview, Purview's scan result is ignored. It defaults to displaying the Microsoft Defender for Cloud's scanning results for the supported resource type.

## What's supported

The table summarizes availability and supported scenarios for sensitive data discovery.

| **Support** | **Details** |
| --- | --- |
| What Azure data resources can I discover? | **Object storage:**[Block blob](/en-us/azure/storage/blobs/storage-blobs-introduction) storage accounts in Azure Storage v1/v2 Azure files in Azure Storage v1/v2.Supported using SMB protocol only Azure Data Lake Storage Gen2Storage accounts behind private networks are supported. Storage accounts encrypted with a customer-managed server-side key are supported. Accounts aren't supported if a storage account endpoint has a [custom domain mapped to it](/en-us/azure/storage/blobs/storage-custom-domain-name).Prerequisites and limitations: - In order to scan File Shares, Defender for Cloud assigns the role **Storage File Data Privileged Reader** to **StorageDataScanner**.**Databases**Azure SQL Databases  Azure SQL Database encrypted with [Transparent data encryption](/en-us/azure/azure-sql/database/secure-database-tutorial#transparent-data-encryption) |
| What AWS data resources can I discover? | **Object storage:**AWS S3 buckets Defender for Cloud can discover KMS-encrypted data, but not data encrypted with a customer-provided keys ([SSE-C](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ServerSideEncryptionCustomerKeys.html)).**Databases**- Amazon Aurora- Amazon RDS for PostgreSQL- Amazon RDS for MySQL- Amazon RDS for MariaDB- Amazon RDS for SQL Server (noncustom)- Amazon RDS for Oracle Database (noncustom, SE2 Edition only) Prerequisites and limitations: - Automated backups need to be enabled. - The IAM role created for the scanning purposes (DefenderForCloud-DataSecurityPostureDB by default) needs to have permissions to the KMS key used for the encryption of the RDS instance. - You can't share a DB snapshot that uses an option group with permanent or persistent options, except for Oracle DB instances that have the **Timezone** or **OLS** option (or both). [Learn more](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html) |
| What GCP data resources can I discover? | GCP storage buckets Standard Class Geo: region, dual region, multi region |
| What permissions do I need for discovery? | Storage account: Subscription Owner**or**`Microsoft.Authorization/roleAssignments/*` (read, write, delete) **and**`Microsoft.Security/pricings/*` (read, write, delete) **and**`Microsoft.Security/pricings/SecurityOperators` (read, write) Amazon S3 buckets and RDS instances: AWS account permission to run Cloud Formation (to create a role). GCP storage buckets: Google account permission to run script (to create a role). |
| What file types are supported for sensitive data discovery? | Supported file types (you can't select a subset) - .doc, .docm, .docx, .dot, .gz, .odp, .ods, .odt, .pdf, .pot, .pps, .ppsx, .ppt, .pptm, .pptx, .xlc, .xls, .xlsb, .xlsm, .xlsx, .xlt, .csv, .json, .psv, .ssv, .tsv, .txt., xml, .parquet, .avro, .orc. |
| What Azure regions are supported? | You can discover Azure storage accounts in:West Europe (westeurope), Canada Central (canadacentral), UK South (uksouth), Japan East (japaneast), East US 2 (eastus2), Australia East (australiaeast), Canada East (canadaeast), East US (eastus), South Central US (southcentralus), North Central US (northcentralus), West US 2 (westus2), Southeast Asia (southeastasia), Central US (centralus), Brazil South (brazilsouth), France Central (francecentral), North Europe (northeurope), Japan West (japanwest), Australia Southeast (australiasoutheast), West US (westus), East US 2 EUAP (eastus2euap), Australia Central (australiacentral), East Asia (eastasia), UK West (ukwest), Central India (centralindia), Norway East (norwayeast), South Africa North (southafricanorth), Sweden Central (swedencentral), West US 3 (westus3), West Central US (westcentralus), South India (southindia), UAE North (uaenorth), Switzerland North (switzerlandnorth), Germany West Central (germanywestcentral), Korea Central (koreacentral), Korea South (koreasouth), Jio India West (jioindiawest), Israel Central (israelcentral), Switzerland West (switzerlandwest), Poland Central (polandcentral), Germany North (germanynorth), Italy North (italynorth), Norway West (norwaywest), Australia Central 2 (australiacentral2), South Africa West (southafricawest), Mexico Central (mexicocentral), UAE Central (uaecentral), France South (francesouth), Brazil Southeast (brazilsoutheast), Jio India Central (jioindiacentral), Sweden South (swedensouth), Spain Central (spaincentral), New Zealand North (newzealandnorth) You can discover Azure SQL Databases in any region where Defender CSPM and Azure SQL Databases are supported. |
| What AWS regions are supported? | S3:EU (Stockholm), EU (London), EU (Paris), Asia Pacific (Mumbai), Canada (Central), South America (São Paulo), US West (N. California), US West (Oregon), Asia Pacific (Tokyo), Asia Pacific (Singapore), Asia Pacific (Sydney), EU (Ireland), US East (N. Virginia), EU (Frankfurt), US East (Ohio)RDS:Africa (Cape Town); Asia Pacific (Hong Kong SAR); Asia Pacific (Hyderabad); Asia Pacific (Melbourne); Asia Pacific (Mumbai); Asia Pacific (Osaka); Asia Pacific (Seoul); Asia Pacific (Singapore); Asia Pacific (Sydney); Asia Pacific (Tokyo); Canada (Central); Europe (Frankfurt); Europe (Ireland); Europe (London); Europe (Paris); Europe (Stockholm); Europe (Zurich); Middle East (UAE); South America (São Paulo); US East (Ohio); US East (N. Virginia); US West (N. California): US West (Oregon). Discovery is done locally within the region. |
| What GCP regions are supported? | Tel Aviv (me-west1), Mumbai (asia-south1), South Carolina (us-east1), Montréal (northamerica-northeast1), Iowa (us-central1), Oregon (us-west1), Belgium (europe-west1), Northern Virginia (us-east4) |
| Do I need to install an agent? | No, discovery requires no agent installation. |
| What's the cost? | The feature is included with the Defender CSPM and Defender for Storage plans, and doesn’t incur extra costs except for the respective plan costs. |
| Other costs | Sensitive data discovery for Azure Storage accounts relies on other Azure services. This reliance might result in extra costs, including Azure Storage read operations. |
| What permissions do I need to view/edit data sensitivity settings? | You need one of these Microsoft Entra roles:- Compliance Data Administrator, Compliance Administrator, or higher<br>- Security Operator, Security Administrator, or higher |
| What permissions do I need to perform onboarding? | You need one of these [Azure role-based access control (Azure RBAC) roles](/en-us/azure/role-based-access-control/role-assignments-portal): Security Admin, Contributor, Owner on the subscription level (where the GCP project/s reside). For consuming the security findings: Security Reader, Security Admin, Reader, Contributor, Owner on the subscription level (where the GCP project/s reside). |

## Configure data sensitivity settings

The main steps for configuring data sensitivity settings include:

- [Import custom sensitivity info types/labels from Microsoft Purview compliance portal](data-sensitivity-settings#import-custom-sensitivity-info-typeslabels)
- [Customize sensitive data categories/types](data-sensitivity-settings#customize-sensitive-data-categoriestypes)
- [Set the threshold for sensitivity labels](data-sensitivity-settings#set-the-threshold-for-sensitive-data-labels)

[Learn more](/en-us/microsoft-365/compliance/create-sensitivity-labels) about sensitivity labels in Microsoft Purview.

## Discovery

Defender for Cloud starts discovering data immediately after you enable a plan, or after you turn on plan features.

For object storage:

- Results are available for first-time discovery within 24 hours.
- After you update files in the discovered resources, data refreshes within eight days.
- A new Azure storage account added to an already discovered subscription is discovered within 24 hours or less.
- A new AWS S3 bucket or GCP storage bucket added to an already discovered AWS account or Google account is discovered within 48 hours or less.
- Sensitive data discovery for storage conducts locally within your region. This ensures that your data doesn't leave your region. Only resource metadata, such as files, blobs, buckets names, detected sensitivity labels, and the names of identified Sensitive Information Types (SITs), transfer to Defender for Cloud.

For databases:

- Are scanned on a weekly basis.
- For newly enabled subscriptions, results appear within 24 hours.

### Cloud Security Explorer

We display all storage types, including Azure Storage Accounts, AWS Buckets, and GCP Buckets, regardless of their associated insights. For Azure Storage Accounts, which include Blob Containers and File Shares, the following rules apply:

- Blob Containers display if they meet any of the following criteria:

    - They have the Contains Sensitive Data insight.
    - They have the Public Access insight.
    - They have a replication rule to or from another blob.
- File Shares display only if they have the "Contains Sensitive Data" insight.

### Discover and scan Azure storage accounts

To scan Azure storage accounts, Microsoft Defender for Cloud creates a new `storageDataScanner` resource and assigns it the [Storage Blob Data Reader](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-reader) role. This role grants the following permissions:

- List
- Read

For storage accounts behind private networks, we include the `StorageDataScanner` in the list of allowed resource instances in the storage account's network rules configuration.

### Discover and scan AWS S3 buckets

To protect AWS resources in Defender for Cloud, set up an AWS connector using a CloudFormation template to onboard the AWS account.

- To discover AWS data resources, Defender for Cloud updates the CloudFormation template.
- The CloudFormation template creates a new role in AWS IAM to allow permission for the Defender for Cloud scanner to access data in the S3 buckets.
- To connect AWS accounts, you need Administrator permissions on the account.
- The role allows these permissions: S3 read only; KMS decrypt.

### Discover and scan AWS RDS instances

To protect AWS resources in Defender for Cloud, set up an AWS connector using a CloudFormation template to onboard the AWS account.

- To discover AWS RDS instances, Defender for Cloud updates the CloudFormation template.
- The CloudFormation template creates a new role in AWS IAM to allow permission for the Defender for Cloud scanner to take the last available automated snapshot of your instance and bring it online in an isolated scanning environment within the same AWS region.
- To connect AWS accounts, you need Administrator permissions on the account.
- Automated snapshots need to be enabled on the relevant RDS Instances/Clusters.
- The role allows these permissions (review the CloudFormation template for exact definitions):
    - List all RDS DBs/clusters
    - Copy all DB/cluster snapshots
    - Delete/update DB/cluster snapshot with prefix *defenderfordatabases*
    - List all KMS keys
    - Use all KMS keys only for RDS on source account
    - Create & full control on all KMS keys with tag prefix *DefenderForDatabases*
    - Create alias for KMS keys
- KMS keys are created once for each region that contains RDS instances. The creation of a KMS key might incur a minimal extra cost, according to AWS KMS pricing.

### Discover and scan GCP storage buckets

To protect GCP resources in Defender for Cloud, set up a Google connector using a script template to onboard the GCP account.

- To discover GCP storage buckets, Defender for Cloud updates the script template.
- The script template creates a new role in the Google account to allow permission for the Defender for Cloud scanner to access data in the GCP storage buckets.
- To connect Google accounts, you need Administrator permissions on the account.

## Exposed to the internet/allows public access

Defender CSPM attack paths and cloud security graph insights include information about storage resources that are exposed to the internet and allow public access. The following table provides more details.

| **State** | **Azure storage accounts** | **AWS S3 Buckets** | **GCP Storage Buckets** |
| --- | --- | --- | --- |
| **Exposed to the internet** | An Azure storage account is considered exposed to the internet if either of these settings enabled: Storage\_account\_name &gt; **Networking** &gt; **Public network access** &gt; **Enabled from all networks** or Storage\_account\_name &gt; **Networking** &gt; **Public network access** &gt; **Enable from selected virtual networks and IP addresses**. | An AWS S3 bucket is considered exposed to the internet if the AWS account/AWS S3 bucket policies don't have a condition set for IP addresses. | All GCP storage buckets are exposed to the internet by default. |
| **Allows public access** | An Azure storage account container is considered as allowing public access if these settings are enabled on the storage account: Storage\_account\_name &gt; **Configuration** &gt;**Allow Blob Anonymous access** &gt; **Enabled**.and **either** of these settings: Storage\_account\_name &gt; **Containers** &gt; container\_name &gt; **Public access level** set to **Blob (anonymous read access for blobs only)** Or, storage\_account\_name &gt; **Containers** &gt; container\_name &gt; **Public access level** set to **Container (anonymous read access for containers and blobs)**. | An AWS S3 bucket is considered to allow public access if both the AWS account and the AWS S3 bucket have **Block all public access** set to **Off**, and **either** of these settings is set: In the policy, **RestrictPublicBuckets** isn't enabled, and the **Principal** setting is set to \* and **Effect** is set to **Allow**. Or, in the access control list, **IgnorePublicAcl** isn't enabled, and permission is allowed for **Everyone**, or for **Authenticated users**. | A GCP storage bucket is considered to allow public access if: it has an IAM (Identity and Access Management) role that meets these criteria:  The role is granted to the principal **allUsers** or **allAuthenticatedUsers**. The role has at least one storage permission that *isn't***storage.buckets.create** or **storage.buckets.list**. Public access in GCP is called **Public to internet**. |

Database resources don't allow public access but can still be exposed to the internet.

Internet exposure insights are available for the following resources:

Azure:

- Azure SQL server
- Azure Cosmos DB
- Azure SQL Managed Instance
- Azure MySQL Single Server
- Azure MySQL Flexible Server
- Azure PostgreSQL Single Server
- Azure PostgreSQL Flexible Server
- Synapse Workspace

AWS:

- RDS instance

Note

- Exposure rules that include 0.0.0.0/0 are considered "excessively exposed", meaning that they can be accessed from any public IP.

- Azure resources with the exposure rule "0.0.0.0" are accessible from any resource in Azure (regardless of tenant or subscription).