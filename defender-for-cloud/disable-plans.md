---
layout: Conceptual
title: Disable Microsoft Defender for Cloud plans - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/disable-plans
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
description: Learn how to disable Microsoft Defender for Cloud plans at subscription and resource levels across Azure, AWS, and GCP to prevent unexpected charges.
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 2da26b5e-b217-4f48-f9cd-6c37572532d2
document_version_independent_id: 7b382db5-5d28-6b9a-749d-b318348ef4c7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/disable-plans.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/disable-plans
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/disable-plans.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 1e84e1e1-fb8e-c6b0-c1af-45c616fc26ed
---

# Disable Microsoft Defender for Cloud plans - Microsoft Defender for Cloud | Microsoft Learn

You can disable Microsoft Defender for Cloud plans on your connected environments to manage your security costs. When you disable a plan, the associated security features, recommendations, and alerts for that plan stop appearing in Defender for Cloud.

Each Defender for Cloud plan has a different pricing structure based on attached resources and enabled subplans. For more information, see [the Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

## Disable plans on the subscription level

Disabling a plan at the subscription level affects all resources under that subscription unless resource-level overrides are active.

If you created a resource to support a plan, such as a Log Analytics workspace or a Storage Account, delete it manually when it's no longer needed.

To disable plans at the subscription level:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant Azure, Amazon Web Services (AWS), or Google Cloud Project (GCP) subscription.

    [![Screenshot of the Environment settings page in Defender for Cloud showing Azure, AWS, and GCP subscription entries.](media/disable-plans/environment-settings-screen.png)](media/disable-plans/environment-settings-screen.png#lightbox)

### Disable plans by multicloud environment

After selecting the subscription, select the tab for your multicloud environment (Azure, AWS, or GCP) to continue.

# [Azure](#tab/Azure)
1. Find the plans you want to disable and toggle the switch to **Off**.

    [![Screenshot that shows all of the Defender for Cloud plans toggled to off in an Azure environment.](media/disable-plans/plans-disabled.png)](media/disable-plans/plans-disabled.png#lightbox)

    1. (Optional) To disable the Defender for Databases plan, use the pop-up to turn off all four Defender for Databases subplans.

        [![Screenshot that shows the four Defender for Databases subplans toggled to Off.](media/disable-plans/databases-disabled.png)](media/disable-plans/databases-disabled.png#lightbox)
2. Select **Continue**.
3. Select **Save**.

# [AWS](#tab/AWS)
1. Find the plans you want to disable and toggle the switch to **Off**.

    [![Screenshot that shows the Defender for Cloud plans disabled in an Amazon environment.](media/disable-plans/disable-amazon-plans.png)](media/disable-plans/disable-amazon-plans.png#lightbox)
2. Select **Next: Configure access**.
3. Select a deployment type:

    - **Default access**: Allows Defender for Cloud to scan your resources and automatically include future capabilities.
    - **Least privilege access**: Grants Defender for Cloud access only to the current permissions needed for the selected plans. If you select the least privileged permissions, you receive notifications on any new roles and permissions that are required to get full functionality for connector health.
4. Select a deployment method: **AWS CloudFormation** or **Terraform**.

    [![Screenshot that shows deployment options and instructions for configuring access.](media/quickstart-onboard-aws/add-aws-account-configure-access.png)](media/quickstart-onboard-aws/add-aws-account-configure-access.png#lightbox)
5. Follow the on-screen instructions for the selected deployment method to complete the required dependencies on AWS.
6. Select the check box to confirm you followed the instructions.
7. Select **Next: Review and generate**.
8. Select **Create**.

# [GCP](#tab/GCP)
1. Find the plans you want to disable and toggle the switch to **Off**.

    [![Screenshot that shows the Defender for Cloud plans disabled in a Google environment.](media/disable-plans/disable-google-plans.png)](media/disable-plans/disable-google-plans.png#lightbox)
2. Select **Next: Configure access**.
3. Select a deployment type:

    - **Default access**: Allows Defender for Cloud to scan your resources and automatically include future capabilities.
    - **Least privilege access**: Grants Defender for Cloud access only to the current permissions needed for the selected plans. If you select the least privileged permissions, you receive notifications on any new roles and permissions that are required to get full functionality for connector health.
4. Select a deployment method: **GCP Cloud shell** or **Terraform**.
5. Follow the on-screen instructions for the selected deployment method to complete the required dependencies on Google Cloud.

    [![Screenshot that shows the GCP configure access page with Cloud Shell and Terraform deployment options.](media/disable-plans/disable-google-configuration.png)](media/disable-plans/disable-google-configuration.png#lightbox)
6. Select the check box to confirm you followed the instructions.
7. Select **Next: Review and generate**.
8. Select **Create**.

---

Important

Defender for Cloud stops monitoring and onboarding all your resources after you disable all plans in your environment.

Disabling plans doesn't cancel your subscription. To cancel your subscription, use the Azure subscription cancellation process.

## Ensure plans are fully disabled

Turning off a plan at the subscription level doesn't prevent it from being turned on for a specific resource, which can generate charges. To fully disable a plan for a specific resource, check the resource-level configuration for that plan.

For security purposes, Defender for Cloud has multiple features that can re-enable themselves. Those mechanisms include:

- Autoprovisioning (agents/extensions that get reinstalled)
- Azure Policy assignments that redeploy Defender for Cloud components
- Resource-level settings

Note

To confirm that charges stop, check your billing meters in Cost Management + Billing.

# [1. Disable autoprovisioning](#tab/disable-auto-provisioning)
Autoprovisioning can silently reinstall agents or extensions after you turn off plans. To prevent reinstallation, disable autoprovisioning for Endpoint protection and Guest Configuration agent in Defender for Cloud settings.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings** &gt; **relevant subscription or resource**.
3. Select **Settings** for the relevant plans.

    [![Screenshot that shows an example of where the settings button is located on the plans page.](media/disable-plans/select-settings.png)](media/disable-plans/select-settings.png#lightbox)
4. Toggle Guest configuration agent to **Off**.
5. Toggle Endpoint protection to **Off**.
6. Select **Continue**.
7. Select **Save**.

# [2. Disable Azure Policy assignments](#tab/disable-azure-policy-assignments)
As a security measure, Defender for Cloud includes Azure Policy initiatives that automatically redeploy Defender for Cloud components if you uninstall them. To prevent this automatic redeployment, identify and disable any relevant Azure Policy assignments.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Policy**.
3. Select **Assignments**.

    [![Screenshot that shows the Assignments page in Azure Policy.](media/disable-plans/policy-assignments.png)](media/disable-plans/policy-assignments.png#lightbox)
4. Search policies starting with `Deploy Microsoft Defender for Endpoint...`.

    [![Screenshot that shows search results for policies beginning with 'Deploy Microsoft Defender for Endpoint'.](media/disable-plans/search-assignments.png)](media/disable-plans/search-assignments.png#lightbox)
5. Select each relevant policy assignment.
6. Select **Delete assignment**.

---

## Check resource-level settings

You can enable Microsoft Defender for Cloud for individual resources, even if you turn off the subscription-level plan. To fully stop charges, check and disable Microsoft Defender for Cloud on each supported resource type.

To check and disable Defender for Cloud at the resource level:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Open the specific Azure resource.
3. Locate and select **Microsoft Defender for Cloud**.
4. Turn Defender for Cloud to **Off**.
5. Select **Save**.

### Resource-specific instructions

The following resource types are the most common where Defender for Cloud stays enabled.

# [App Service](#tab/app-service)
App Service is the most common place where Defender for Cloud stays enabled accidentally. You pay for Defender for App Service per App Service plan. It can stay enabled even when the subscription plan is off.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Open the **App Service plan** (not the individual app).
3. Select **Microsoft Defender for Cloud**.
4. Set **Defender for App Service** to **Off**.
5. Select **Save**.

# [Storage Accounts](#tab/storage-accounts)
The Defender for Storage resource-level setting overrides the subscription-level setting. Charges stop for that storage account only.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Open the **Storage Account**.
3. Select **Microsoft Defender for Cloud**.
4. Toggle **Defender for Storage** to **Off**.
5. Select **Save**.

# [Virtual Machines](#tab/virtual-machines)
If autoprovisioning or an Azure Policy assignment is still active, agents might be reinstalled. This dependency is why subscription-level cleanup still matters.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Virtual Machines**.
3. Select a virtual machine (VM).
4. Ensure Defender for Servers displays **unknown**.

    [![Screenshot that shows the status displaying as Unknown.](media/disable-plans/display-unknown.png)](media/disable-plans/display-unknown.png#lightbox)
5. If Microsoft Defender for Servers displays `On`, go to **Microsoft Defender for Cloud** &gt; **Environment settings** &gt; **relevant subscription or resource**.
6. Toggle Defender for Servers to **Off**.
7. Select **Save**.

# [SQL / Databases](#tab/sql-databases)
To disable Defender for SQL at the resource level:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Open the **SQL Server** or **SQL Database** resource.
3. Select **Microsoft Defender for Cloud**.
4. Select **Configure**.

    [![Screenshot that shows where the Configure button is located on the SQL resource's Defender for Cloud page.](media/disable-plans/configure.jpg)](media/disable-plans/configure.jpg#lightbox)
5. Toggle Microsoft Defender for SQL to **Off**.
6. Select **Save**.

# [Servers](#tab/servers)
At the resource level, you can enable or disable Defender for Servers plan 1. For plan 2, you can disable it for specific resources only when plan 2 remains enabled at the subscription level.

For example, you can enable Defender for Servers plan 2 at the subscription level and disable it for specific resources within the subscription. However, you can't enable plan 2 only on specific resources. If you're still being billed even after you disable the plan, use the [Coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) to see what resources remain covered.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Environment settings**.
4. Select a relevant subscription or workspace.
5. Toggle **Defender for Servers plan 1** or **plan 2** to **Off**.
6. Select **Save**.
7. Repeat for each relevant subscription or workspace.

---

## Confirm resource-level Defender is off

To confirm that resource-level Defender is truly off, use billing as the source of truth.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Cost Management + Billing** &gt; **Cost analysis**.
3. Filter by **Service name** and **Meter name**.
4. Look for meters such as:

    - `Defender for App Service`
    - `Defender for Storage`
    - `Defender for Servers`
    - `Defender CSPM` (Cloud Security Posture Management)

If charges still appear, there's at least one resource with Defender still enabled, or a policy or autoprovisioning rule is re-enabling it.

## Confirm you're no longer covered

After you disable the plans and confirm that you're no longer billed, use the [Coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) to verify your current coverage.