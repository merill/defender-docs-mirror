---
layout: Conceptual
title: Estimate costs with the Microsoft Defender for Cloud cost calculator - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/cost-calculator
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
description: Discover how to use the Microsoft Defender for Cloud Cost Calculator to estimate your cloud security expenses.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 87169a31-665f-c763-e8f6-26fc37ecf82e
document_version_independent_id: ef0b9f42-ada1-a4df-be39-e2d3672caf77
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/cost-calculator.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/cost-calculator
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/cost-calculator.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 879921ba-e374-469a-bed9-5ee10b5fcc6e
---

# Estimate costs with the Microsoft Defender for Cloud cost calculator - Microsoft Defender for Cloud | Microsoft Learn

The Microsoft Defender for Cloud cost calculator helps you estimate potential costs for your cloud security needs. You can configure plans and environments and get a detailed cost breakdown, including applicable discounts.

## Access the cost calculator

To use the Defender for Cloud cost calculator, open the [Microsoft Defender for Cloud Environment settings](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/EnvironmentSettings). Then select **Cost Calculator**.

[![Environment settings page with Cost Calculator selected in Microsoft Defender for Cloud.](media/cost-calculator/select-cost-calculator.png)](media/cost-calculator/select-cost-calculator.png#lightbox)

## Configure Defender for Cloud plans and environments

On the first page of the calculator, select **Add Assets** to start adding assets to your cost calculation. You can add assets in three ways:

- Add assets from onboarded environments: **Recommended** - Add assets from environments already onboarded to Defender for Cloud. This method covers all plans for Azure and works faster than the script option.
- Add assets with a script: Download and execute a script to automatically add existing assets. Recommended for environments such as Amazon Web Services (AWS) or Google Cloud Platform (GCP) projects that aren't yet onboarded to Azure.
- Add custom assets: Add assets manually without using automation.

[![Cost Calculator Add Assets page showing options to add onboarded, script-based, or custom assets.](media/cost-calculator/add-assets-cost-calculator.png)](media/cost-calculator/add-assets-cost-calculator.png#lightbox)

Note

The cost calculator doesn't consider reservation plans for Defender for Cloud.

### Add assets from onboarded environments

Tip

Adding assets from onboarded environments is recommended for Azure environments because it covers all plans and provides faster results than using scripts.

1. In **Azure environments**, select the onboarded environment that you want to include in the cost calculation.

    Note

    The calculator discovers resources for which you have permissions.
2. Choose the plans. The calculator estimates the cost based on your selections and any existing discounts.

    [![Onboarded environments list with selectable subscriptions and plans for cost calculation.](media/cost-calculator/assign-onboarded-assets.png)](media/cost-calculator/assign-onboarded-assets.png#lightbox)

### Add assets with a script

Note

Adding assets with a script is recommended for environments that aren't yet onboarded to Azure, such as AWS or GCP projects.

1. In **Environment type**, choose Azure, AWS, or GCP, and then copy the script to a new \*.ps1 file.

    Note

    The script only collects information that the user running it has access to.
2. Run the script in your PowerShell 7.X environment by using a privileged user account. The script collects information about your billable assets and creates a CSV file. It gathers information in two steps. First, it collects the current number of billable assets that usually stay constant. Second, it collects information about billable assets that can change a lot during the month. For these assets, it checks usage over the last 30 days to evaluate the cost. You can stop the script after the first step, which takes a few seconds. Or you can continue to collect the last 30 days of usage for dynamic assets, which might take longer for large accounts.
3. Upload the CSV file generated by the script into the wizard where you downloaded the script.
4. Select **Defender for Cloud plans**. The calculator estimates costs based on your selection and any existing discounts.

Note

- Reservation plans for Defender for Cloud aren't considered.
- For Defender for APIs: When calculating the cost based on the number of application programming interface (API) calls in the last 30 days, we automatically select the best Defender for APIs plan for you. If there are no API calls in the last 30 days, we automatically disable the plan for calculation purposes.

[![Script upload step in Cost Calculator with CSV upload control and plan selection.](media/cost-calculator/add-assets-with-script.png)](media/cost-calculator/add-assets-with-script.png#lightbox)

#### Required permissions for scripts

The following permissions overview describes the permissions required to run the scripts for each cloud provider.

##### Azure

To run this script successfully for each subscription, the account you use needs permissions that allow it to:

- **Discover and list resources** (including virtual machines, storage accounts, Azure API Management (APIM) services, Azure Cosmos DB accounts, and other resources).
- **Query Resource Graph** (via Search-AzGraph).
- **Read Metrics** (via Get-AzMetric and the Azure Monitor/Insights APIs).

**Recommended built-in role**:

In most cases, the **Reader** role *at the subscription scope* is sufficient. The Reader role provides the following key capabilities needed by this script:

- **Read all resource types** (so you can list and parse things like Storage Accounts, VMs, Cosmos DB, and APIM, etc.).
- **Read metrics (Microsoft.Insights/metrics/read)** so that calls to Get-AzMetric or direct Azure Monitor REST queries succeed.
- **Resource Graph queries** works as long as you have at least read access to those resources in the subscription.

Note

If you want to be certain you have the necessary metric permissions, you can also use **Monitoring Reader** role; however, the standard **Reader** role already includes read access to metrics and is usually all you need.

**If you already have Contributor or Owner roles**:

- **Contributor** or **Owner** on the subscription is more than enough (these roles are higher-privileged than Reader).
- The script doesn't perform resource creation or deletion. Therefore, granting high-level roles (like Contributor/Owner) for the sole purpose of data collection might be overkill from a least-privilege perspective.

**Summary**:

Granting your user or service principal the **Reader** role (or any higher-privileged role) on each subscription you want to query ensures the script can:

- Retrieve the list of subscriptions.
- Enumerate and read all relevant resource information (via REST or Az PowerShell).
- Fetch the necessary metrics (Requests for APIM, RU consumption for Cosmos DB, Storage Accounts ingress, etc.).
- Run Resource Graph queries without issue.

##### AWS

The AWS script supports two discovery flows:

- **Single account discovery** - Discovers resources within a single AWS account
- **Organization discovery** - Discovers resources across all member accounts in an AWS Organization

###### Single account discovery

For single account discovery, the following overview describes the permissions your AWS identity (user or role) needs to run this script successfully. The script enumerates resources (Amazon Elastic Compute Cloud (EC2), Amazon Relational Database Service (RDS), Amazon Elastic Kubernetes Service (EKS), Amazon Simple Storage Service (S3), and others) and fetches metadata for those resources. It doesn't create, modify, or delete resources, so **read-only** access is sufficient in most cases.

**AWS managed policy: ReadOnlyAccess or ViewOnlyAccess**:

The simplest approach is to attach one of AWS's built-in read-only policies to the IAM principal (user or role) that runs this script. Examples include:

- `arn:aws:iam::aws:policy/ReadOnlyAccess`
- `arn:aws:iam::aws:policy/job-function/ViewOnlyAccess`

Either of these policies covers the *describe* and *list* permissions for most AWS services. If your environment's security policy allows it, **ReadOnlyAccess** is the easiest way to ensure the script works across all AWS resources it enumerates.

**Key services and required permissions**:

If you need a more granular approach with a **custom** IAM policy, the following services and permissions are required:

- **EC2**
    - ec2:DescribeInstances
    - ec2:DescribeRegions
    - ec2:DescribeInstanceTypes (for retrieving vCPU/core info)
- **RDS**
    - rds:DescribeDBInstances
- **EKS**
    - eks:ListClusters
    - eks:DescribeCluster
    - eks:ListNodegroups
    - eks:DescribeNodegroup
- **Auto Scaling**(for EKS node groups underlying instances)
    - autoscaling:DescribeAutoScalingGroups
- **S3**
    - s3:ListAllMyBuckets
- **AWS Security Token Service (STS)**
    - sts:GetCallerIdentity (to retrieve the AWS account ID)

Additionally, if you need to list other resources not shown in the script or if you plan to expand the script's capabilities, ensure you grant the appropriate Describe\*, List\*, and Get\* actions as needed.

###### Organization discovery

For organization-wide discovery, you need:

- **In the management account**: Permission to list all accounts in the organization

    - `organizations:ListAccounts`
- **In all member accounts**: A role with the same permissions as described for single account discovery (ReadOnlyAccess or the custom permissions listed above)

**Setting up organization discovery**:

1. Create an IAM role in each member account with the required read permissions (as described in single account discovery)
2. Configure the role to trust the principal that runs the discovery script
3. Ensure the principal running the script has:
    - Permission to assume the role in each member account
    - The `organizations:ListAccounts` permission in the management account

Note

The organization discovery flow automatically iterates through all member accounts where the configured role is accessible.

**Summary**:

- The simplest approach is to attach AWS's built-in **ReadOnlyAccess** policy, which already includes all the actions required to list and describe EC2, RDS, EKS, S3, Auto Scaling resources, and call STS to get your account info.
- To grant just enough privileges, create a custom read-only policy with the above Describe\*, List\*, and Get\* actions for EC2, RDS, EKS, Auto Scaling, S3, and STS.

Either approach gives your script sufficient permissions to:

- List regions.
- Retrieve EC2 instance metadata.
- Retrieve RDS instances.
- List and describe EKS clusters and node groups (and the underlying Auto Scaling groups).
- List S3 buckets.
- Obtain your AWS account ID via STS.

This permission set ensures the script can discover resources and fetch the relevant metadata without creating, modifying, or deleting anything.

##### GCP

The following overview describes the permissions your GCP user or service account needs to run this script successfully. You can use the script to discover resources in a single project or across multiple projects, depending on your selection. To estimate costs for multiple projects, make sure your account has the required permissions in each project you want to include. The script lists and describes resources such as VM instances, Cloud SQL databases, Google Kubernetes Engine (GKE) clusters, and Google Cloud Storage (GCS) buckets in all selected projects.

###### Recommended built-in role: Project Viewer

The simplest approach to ensure read-only access across all these resources is granting your user or service account the **roles/viewer** role at the project level (the same project you select via `gcloud config set project`).

The **roles/viewer** role includes read-only access to most GCP services within that project, including the necessary permissions for:

- **Compute Engine** (list VM instances, instance templates, machine types, and more).
- **Cloud SQL** (list SQL instances).
- **Kubernetes Engine** (list clusters, node pools, and more).
- **Cloud Storage** (list buckets).

**Granular permissions by service (if creating a custom role)**:

If you prefer a more granular approach, create a **custom IAM role** or set of roles that collectively grant just the needed read-list-describe actions for each service:

- **Compute Engine**(for VM Instances, Regions, Instance Templates, Instance Group Managers):
    - `compute.instances.list`
    - `compute.regions.list`
    - `compute.machineTypes.list`
    - `compute.instanceTemplates.get`
    - `compute.instanceGroupManagers.get`
    - `compute.instanceGroups.get`
- **Cloud SQL**:
    - `cloudsql.instances.list`
- **Google Kubernetes Engine**:
    - `container.clusters.list`
    - `container.clusters.get` (needed when describing clusters)
    - `container.nodePools.list`
    - `container.nodePools.get`
- **Cloud Storage**:
    - `storage.buckets.list`

The script doesn't create or modify any resources, so it doesn't require update or delete permissions—only list, get, or describe type permissions.

**Summary**:

- Using **roles/viewer** at the project level is the fastest and most straightforward way to grant enough permissions for this script to succeed.
- For the strictest least-privilege approach, create or combine custom roles that only include the relevant list, describe, and get actions for Compute Engine, Cloud SQL, GKE, and Cloud Storage.

With these permissions, the script can:

- **Authenticate** (`gcloud auth login`).
- **List** VM instances, machine types, instance group managers, and similar resources.
- **List** Cloud SQL instances.
- **List** and **describe** GKE clusters and node pools.
- **List** GCS buckets.

This read-level access lets you enumerate resource counts and gather metadata without modifying or creating any resources.

### Assign onboarded assets

1. In **Azure environments**, select the onboarded environment that you want to include in the cost calculation.

    Note

    The calculator discovers resources for which you have permissions.
2. Choose the plans. The calculator estimates the cost based on your selections and any existing discounts.

[![Onboarded environments list with selectable subscriptions and plans for cost calculation.](media/cost-calculator/assign-onboarded-assets.png)](media/cost-calculator/assign-onboarded-assets.png#lightbox)

### Assign custom assets

To add a custom environment manually, complete the following steps:

1. Choose a name for the custom environment.
2. Specify the plans and the number of billable assets for each plan.
3. Select **Asset types** that you want to include in the cost calculation.
4. The calculator estimates costs based on your inputs and any existing discounts.

Note

The calculator doesn't consider reservation plans for Defender for Cloud.

[![Custom environment form with environment name, plan configuration, and asset type selection.](media/cost-calculator/add-custom-environment.png)](media/cost-calculator/add-custom-environment.png#lightbox)

## Adjust your report

After generating the report, you can adjust the plans and the number of billable assets:

1. Select the environment you want to modify by selecting the **edit** (pencil) icon.
2. A configuration page appears, where you can adjust plans, the number of billable assets, and the average monthly hours.
3. Select **Recalculate** to update the cost estimate.

## Export the report

When you're satisfied with the report, you can export it as a CSV file:

1. Select **Export to CSV** at the bottom of the **Summary** panel on the right.
2. The cost information is downloaded as a CSV file.

## Frequently asked questions

### What is the cost calculator?

The cost calculator is a tool that simplifies estimating costs for your security protection needs. When you define the scope of your desired plans and environments, the calculator provides a detailed breakdown of potential expenses, including any applicable discounts.

### How does the cost calculator work?

You select the environments and plans you want to enable. The calculator then performs a discovery process to automatically populate the number of billable units for each plan per environment. You can also manually adjust the unit quantities and discount levels.

### What is the discovery process?

The discovery process generates a report of the selected environment, including the inventory of billable assets by the various Defender for Cloud plans. This process relies on user permissions and the environment state at the time of discovery. For large environments, this process might take approximately 30 to 60 minutes as it also samples dynamic assets.

### Do I need to grant any special permission for the cost calculator to perform the discovery process?

The cost calculator uses your existing permissions to run the script and perform discovery automatically. It gathers the necessary data without requiring further access rights. To see what permissions you need to run the script, refer to the Required permissions for scripts section.

### Do the estimations accurately predict my cost?

The calculator provides an estimate based on the information available when the script runs. Various factors might influence the final cost, so you should consider it an approximate calculation.

### What are the billable units?

The cost of plans is based on the units they protect. Each plan charges for a different unit type. You can find unit details on the [Microsoft Defender for Cloud Environment settings page](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/EnvironmentSettings).

### Can I adjust the estimates manually?

Yes, the cost calculator supports both automatic data collection and manual adjustments. You can modify the unit quantity and discount levels to better reflect your specific needs and see how these changes affect your overall cost.

### Does the calculator support multiple cloud providers?

Yes, it offers multicloud support, ensuring that you can obtain accurate cost estimations regardless of your cloud provider.

### How can I share my cost estimate?

After you generate your cost estimate, you can easily export and share it for budget planning and approvals. This feature ensures that all stakeholders have access to the necessary information.

### Where can I get help if I have questions?

Our support team is ready to assist you with any questions or concerns you might have. Feel free to reach out to us for assistance.

### How can I try the cost calculator?

Try the cost calculator to define the scope of your protection needs. To use it, open [Microsoft Defender for Cloud Environment settings](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/EnvironmentSettings) and select **Cost Calculator**.