---
layout: Conceptual
title: Connect your GCP Project - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/quickstart-onboard-gcp
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
description: Connect your GCP project or organization to Microsoft Defender for Cloud to protect workloads and assess your security posture.
ms.topic: install-set-up-deploy
ms.date: 2026-08-04T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1018
ai-usage: ai-assisted
locale: en-us
document_id: 484d916c-10fa-dfc3-93c9-e1722e49fd61
document_version_independent_id: e8f1f0da-a911-2a9f-d6c8-eee7d76cf486
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/quickstart-onboard-gcp.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/quickstart-onboard-gcp
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/quickstart-onboard-gcp.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: b1f4d4e4-db27-6cbd-cfb3-ca5b8b76397f
---

# Connect your GCP Project - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud provides security posture management and threat protection for workloads running in Google Cloud Platform (GCP).

This article shows you how to connect a GCP project or organization to Microsoft Defender for Cloud so Microsoft Defender for Cloud can discover resources, assess security posture, and surface security recommendations and alerts.

## Authentication architecture

Microsoft Defender for Cloud uses federated authentication to securely access GCP APIs without storing long-lived credentials.

During onboarding, Defender for Cloud establishes trust with Google Cloud using workload identity federation and service account impersonation. Access is scoped to the connected project or organization and limited to the permissions required by the enabled Defender plans.

Learn more about [authentication architecture for GCP connectors](authentication-architecture-google-cloud).

## Prerequisites

Before you connect your GCP project, make sure you have:

- A Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free one](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) enabled on your Azure subscription.
- Access to a GCP project or organization.
- Contributor-level permission for the relevant Azure subscription.
- If you enable CIEM as part of Defender for CSPM, the user onboarding the connector also needs the [Security Admin role and Application.ReadWrite.All permission](enable-permissions-management?source=recommendations#before-you-start) for the tenant.

## Cost considerations

Connecting GCP projects to Microsoft Defender for Cloud and enabling Defender plans can incur additional charges.

You can learn more about Defender for Cloud pricing on the [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/).

You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

## GCP project and subscription mapping

When connecting GCP projects to Azure subscriptions, consider the following:

- GCP projects are connected to Microsoft Defender for Cloud at the project level.
- You can connect multiple GCP projects to a single Azure subscription.
- You can connect multiple GCP projects across multiple Azure subscriptions.

Note

For the best experience and performance in the Azure portal, we recommend limiting each portal view to 10,000 resources or fewer. For larger GCP environments, distribute GCP connectors among multiple Azure subscriptions. Use the Azure portal global filter to select the subscriptions you want to view. This recommendation doesn't apply to the Defender portal.

Learn more about the [Google Cloud resource hierarchy](https://cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy#resource-hierarchy-detail).

## Connect your GCP project

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Defender for Cloud** &gt; **Environment settings**.
4. Select **Add environment** &gt; **Google Cloud Platform**.

    [![Screenshot that shows where the GCP connector option is located.](media/quickstart-onboard-gcp/connector.png)](media/quickstart-onboard-gcp/connector.png#lightbox)
5. Select the **Subscription** in which the security connector will be created.
6. Select the **Resource group** in which the security connector will be created.
7. Select the **Location** where the security connector will be created.
8. Select an interval to scan the GCP environment every 4, 6, 12, or 24 hours. Some data collectors run with fixed scan intervals and aren't affected by custom interval configurations.

    Note

    The following data collectors use a fixed scan interval:

    | Data collector name | Scan interval |
    | --- | --- |
    | ComputeInstance  ArtifactRegistryRepositoryPolicy  ArtifactRegistryImage  ContainerCluster  ComputeInstanceGroup  ComputeZonalInstanceGroupInstance  ComputeRegionalInstanceGroupManager  ComputeZonalInstanceGroupManager  ComputeGlobalInstanceTemplate | 1 hour |
9. **Organization only:** Enter the GCP organization ID.
10. **Organization only:** If needed, enter project numbers to exclude.
11. **Organization only:** If needed, enter folder IDs to exclude.
12. **Single project only:** Enter the GCP project number.
13. **Single project only:** Enter the GCP project ID.
14. Select **Next: Select plans**.

    Note

    As the Log Analytics agent (also known as MMA) retired in [August 2024](https://azure.microsoft.com/updates/were-retiring-the-log-analytics-agent-in-azure-monitor-on-31-august-2024/), all Defender for Servers features and security capabilities that currently depend on it, including those described on this page, will be available through either [Microsoft Defender for Endpoint integration](integration-defender-for-endpoint) or [agentless scanning](concept-agentless-data-collection), before the retirement date. For more information about the roadmap for each of the features that are currently rely on Log Analytics Agent, see [this article](prepare-deprecation-log-analytics-mma-agent).
15. Choose the Defender plans you want to enable.

    Note

    Each plan might incur charges. Learn more about [Defender for Cloud pricing](https://azure.microsoft.com/pricing/details/defender-for-cloud).

    [![Screenshot that shows toggles turned on for all plans.](media/quickstart-onboard-gcp/select-plans.png)](media/quickstart-onboard-gcp/select-plans.png#lightbox)
16. Select **Next: Configure access**.
17. Select the permissions type:

    - **Default access**: Grants permissions required for current and future capabilities.
    - **Least privilege access**: Grants only the permissions required today. You might receive notifications if additional access is needed later.
18. Follow the on-screen instructions to configure access between Defender for Cloud and your GCP environment.

    [![Screenshot that shows deployment options and instructions for configuring access.](media/quickstart-onboard-gcp/add-gcp-project-configure-access.png)](media/quickstart-onboard-gcp/add-gcp-project-configure-access.png#lightbox)

    The generated `gcloud` script is based on the scope and Defender plans you selected. Run the script in the GCP environment you're onboarding.

    The script creates the required resources in your GCP environment, including:

    - Workload identity pool
    - Workload identity provider (per plan)
    - Service accounts
    - Project level policy bindings (service account has access only to the specific project)

    Note

    The following APIs must be enabled on the project where you run the onboarding script:

    - `iam.googleapis.com`
    - `sts.googleapis.com`
    - `cloudresourcemanager.googleapis.com`
    - `iamcredentials.googleapis.com`
    - `compute.googleapis.com`

    When you onboard at the organization level, enable these APIs on the management project.

    If these APIs aren't enabled, you can enable them during onboarding by running the GCP Cloud Shell script.
19. Select **Next: Review and generate**.
20. Review the connector details.

    [![Screenshot of the review and generate screen with all of your selections listed.](media/quickstart-onboard-gcp/review-and-generate.png)](media/quickstart-onboard-gcp/review-and-generate-big.png#lightbox)
21. Select **Create**.

Defender for Cloud starts scanning your GCP resources. Security recommendations appear within a few hours. If you enabled autoprovisioning, Azure Arc and any enabled extensions are installed automatically for each newly detected resource.

## Update GCP connector configuration

Update the GCP connector configuration when the permissions or resources required by Defender for Cloud change.

Update the configuration in the following cases:

- You enabled a new Defender plan, such as Defender CSPM, Defender for Databases, or Defender for Containers.
- You modified plan configuration, such as enabling auto provisioning or changing the selected scope.
- Microsoft released an updated onboarding script, such as a version that supports new features, fixes bugs, or updates permissions.
- You experience connector health issues related to missing permissions or missing GCP resources.

To update the configuration, return to the GCP connector in Defender for Cloud, generate the latest `gcloud` script for your selected scope and plans, and rerun the script in the GCP environment you're onboarding.

## Validate connector health

To confirm that your GCP connector is operating correctly:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Environment settings**.
3. Locate the GCP project and review the **Connectivity status** column to see whether the connection is healthy or has issues.
4. Select the value shown in the **Connectivity status** column to view more details.

The Environment details page lists any detected configuration or permission issues affecting the connection to the GCP project.

If an issue is present, you can select it to view a description of the problem and the recommended remediation steps. In some cases, a remediation script is provided to help resolve the issue.

Learn more about [troubleshooting multicloud connectors](troubleshoot-connectors).

## View your current coverage

Defender for Cloud provides access to [workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that provide insights into your security posture.

The [coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) helps you understand your current coverage by showing which plans are enabled on your subscriptions and resources.

## Enable GCP Cloud Logging ingestion (Preview)

GCP Cloud Logging ingestion enhances identity and permission insights by adding activity context for Cloud Infrastructure Entitlement Management (CIEM) assessments, risk-based recommendations, and attack path analysis.

Learn more about [ingesting GCP Cloud Logging with Pub/Sub (Preview)](logging-ingestion).