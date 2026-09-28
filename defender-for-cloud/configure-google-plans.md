---
layout: Conceptual
title: Configure GCP plans - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/configure-google-plans
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
description: Learn how to configure Microsoft Defender for Cloud plans for your Google Cloud Platform (GCP) projects.
ms.topic: install-set-up-deploy
ms.date: 2026-01-14T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: c20c52ac-3c4f-2c79-7d6f-c934713f8775
document_version_independent_id: 147a63b1-4c59-8e00-6f8b-fe3bbfed1c0d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/configure-google-plans.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/configure-google-plans
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/configure-google-plans.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: bdf61915-4e3c-1c82-213c-685f590428ca
---

# Configure GCP plans - Microsoft Defender for Cloud | Microsoft Learn

When you onboard your Google Cloud Platform (GCP) projects to Microsoft Defender for Cloud, select the plans to enable for your projects. Each plan provides different security features and capabilities. By default, all plans are **On**, but turn off unnecessary plans.

# [Defender CSPM](#tab/defender-cspm)
Foundational CSPM is included for free with Defender for Cloud. It provides security posture management and threat protection for your GCP resources. However, to get the full value of Defender CSPM, you need to enable the Defender CSPM plan, which comes with additional costs. For more information about costs, see the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/?msockid=37d5586afa3461fd27164e8bfbe16006).

Learn more about [CSPM and the differences between the plans](concept-cloud-security-posture-management).

#### Prerequisites

- The **Subscription Owner** must enable the plan.
- To enable Cloud Infrastructure Entitlement Management (CIEM) capabilities, the Entra ID account used for the onboarding process must have either the **Application Administrator** or **Cloud Application Administrator** directory role for your tenant (or equivalent administrator rights to create app registrations). This requirement is only necessary during the onboarding process.

#### Configuration

To configure the Defender CSPM plan:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Environment settings**.
4. Select the relevant GCP connector.
5. Locate the Defender CSPM row and select **Settings**.

    [![Screenshot that shows the link for configuring the Defender CSPM plan.](media/quickstart-onboard-gcp/view-configuration.png)](media/quickstart-onboard-gcp/view-configuration.png#lightbox)
6. Toggle the switches to **On** or **Off**, depending on your need. To get the full value of Defender CSPM, turn all toggles to **On**.

    [![Screenshot that shows toggles for Defender CSPM.](media/quickstart-onboard-gcp/cspm-configuration.png)](media/quickstart-onboard-gcp/cspm-configuration.png#lightbox)
7. Select **Save**.
8. Continue from step 8 of the [Connect your GCP project](quickstart-onboard-gcp#connect-your-gcp-project) instructions.

# [Defender for Servers](#tab/defender-for-servers)
[Defender for Servers](defender-for-servers-overview) brings threat detection and advanced defenses to your GCP virtual machine (VM) instances. To have full visibility into Defender for Servers security content, connect your GCP VM instances to Azure Arc.

#### Prerequisites

- Azure Arc for servers installed on your VM instances.

Use the autoprovisioning process to install Azure Arc on your VM instances. Autoprovisioning is enabled by default in the onboarding process and requires **Owner** permissions on the subscription. The Azure Arc autoprovisioning process uses the [OS Config agent on the GCP machines](https://cloud.google.com/compute/docs/images/os-details#vm-manager).

The Azure Arc autoprovisioning process uses the VM manager on GCP to enforce policies on your VMs through the OS Config agent. A VM that has an [active OS Config agent](https://cloud.google.com/compute/docs/manage-os#agent-state) incurs a cost according to GCP. To see how this cost might affect your account, refer to the [GCP technical documentation](https://cloud.google.com/compute/docs/vm-manager#pricing).

Defender for Servers doesn't install the OS Config agent to a VM that doesn't have it installed. However, Defender for Servers enables communication between the OS Config agent and the OS Config service if the agent is already installed but not communicating with the service. This communication can change the OS Config agent from `inactive` to `active` and lead to more costs.

Alternatively, you can manually connect your VM instances to Azure Arc for servers. Instances in projects with the Defender for Servers plan enabled that aren't connected to Azure Arc are surfaced by the recommendation **GCP VM instances should be connected to Azure Arc**. Select the **Fix** option in the recommendation to install Azure Arc on the selected machines.

The respective Azure Arc servers for GCP virtual machines that no longer exist (and the respective Azure Arc servers with a status of [Disconnected or Expired](/en-us/azure/azure-arc/servers/overview)) are removed after seven days. This process removes irrelevant Azure Arc entities to ensure that only Azure Arc servers related to existing instances are displayed.

Ensure that you fulfill the [network requirements for Azure Arc](/en-us/azure/azure-arc/servers/network-requirements?tabs=azure-cloud).

Enable these other extensions on the Azure Arc-connected machines:

- Defender for Endpoint
- A vulnerability assessment solution (Microsoft Defender Vulnerability Management or Qualys)

Defender for Servers assigns tags to your Azure Arc GCP resources to manage the autoprovisioning process. You must have these tags properly assigned to your resources so that Defender for Servers can manage your resources: `Cloud`, `InstanceName`, `MDFCSecurityConnector`, `MachineId`, `ProjectId`, and `ProjectNumber`.

#### Configuration

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Environment settings**.
4. Select the relevant GCP connector.
5. Locate the Defender for Servers row and select **Settings**.

    [![Screenshot that shows the link for the settings are located.](media/quickstart-onboard-gcp/view-configuration.png)](media/quickstart-onboard-gcp/view-configuration.png#lightbox)
6. Toggle the switches to **On** or **Off**, depending on your need.

    [![Screenshot that shows the toggles for the Defender for Servers plan.](media/quickstart-onboard-gcp/auto-provision-screen.png)](media/quickstart-onboard-gcp/auto-provision-screen.png#lightbox)

    If **Azure Arc agent** is **Off**, you need to follow the manual installation process mentioned earlier.
7. Select **Save**.
8. Continue from step 8 of the [Connect your GCP project](quickstart-onboard-gcp#connect-your-gcp-project) instructions.

# [Defender for Databases](#tab/defender-for-databases)
[Defender for Databases](defender-for-databases-overview) brings advanced threat protection to your GCP Cloud SQL instances. Defender for Databases provides vulnerability assessments and advanced threat detection capabilities for your GCP VM instances that are connected to Azure Arc.

#### Configuration

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Environment settings**.
4. Select the relevant GCP connector.
5. Locate the Defender for Databases row and select **Settings**.

    [![Screenshot that shows the link for the settings are located.](media/quickstart-onboard-gcp/view-configuration.png)](media/quickstart-onboard-gcp/view-configuration.png#lightbox)
6. Toggle the switches to **On** or **Off**, depending on your need.

    [![Screenshot that shows the toggles for the Defender for Databases plan.](media/quickstart-onboard-gcp/auto-provision-databases-screen.png)](media/quickstart-onboard-gcp/auto-provision-databases-screen-big.png#lightbox)

    If the toggle for Azure Arc is **Off**, you need to follow the manual installation process mentioned earlier.
7. Select **Save**.
8. Continue from step 8 of the [Connect your GCP project](quickstart-onboard-gcp#connect-your-gcp-project) instructions.

# [Defender for Containers](#tab/defender-for-containers)
[Defender for Containers](defender-for-containers-introduction) brings threat detection and advanced defenses to your GCP Google Kubernetes Engine (GKE) Standard clusters. To get the full security value out of Defender for Containers and to fully protect GCP clusters, ensure that you meet the following requirements.

Note

- If you choose to disable the available configuration options, the deployment process doesn't deploy any agents or components to your clusters. [Learn more about feature availability](support-matrix-defender-for-containers).
- When you deploy Defender for Containers on GCP, it might incur external costs such as [logging costs](https://cloud.google.com/stackdriver/pricing), [pub/sub costs](https://cloud.google.com/pubsub/pricing), and [egress costs](https://cloud.google.com/vpc/network-pricing#:%7E:text=Platform%20SKUs%20apply.-%2cInternet%20egress%20rates%2c-Premium%20Tier%20pricing).

- **Kubernetes audit logs to Defender for Cloud**: Enabled by default. This configuration is available at the GCP project level only. It provides agentless collection of the audit log data through [GCP Cloud Logging](https://cloud.google.com/logging/) to the Defender for Cloud back end for further analysis. Defender for Containers requires control plane audit logs to provide [runtime threat protection](defender-for-containers-introduction#run-time-protection-for-kubernetes-nodes-and-clusters). To send Kubernetes audit logs to Defender, toggle the setting to **On**.

    Note

    If you disable this configuration, the `Threat detection (control plane)` feature is disabled. Learn more about [features availability](support-matrix-defender-for-containers).
- **Auto provision Defender's sensor for Azure Arc** and **Auto provision Azure Policy extension for Azure Arc**: Enabled by default. You can install Azure Arc-enabled Kubernetes and its extensions on your GKE clusters in three ways:

    - Enable Defender for Containers autoprovisioning at the project level, as explained in the instructions in this section. Use this method.
    - Use Defender for Cloud recommendations for per-cluster installation. They appear on the Defender for Cloud recommendations page. [Learn how to deploy the solution to specific clusters](cluster-security-dashboard).
    - Manually install [Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster) and [extensions](/en-us/azure/azure-arc/kubernetes/extensions).
- The [K8S API access](defender-for-containers-architecture#how-does-agentless-discovery-for-kubernetes-in-gcp-work) feature provides API-based discovery of your Kubernetes clusters. To enable, set the **K8S API access** toggle to **On**.
- The [Registry access](agentless-vulnerability-assessment-gcp) feature provides vulnerability management for images stored in Google Container Registry (GCR) and Google Artifact Registry (GAR) and running images on your GKE clusters. To enable, set the **Registry access** toggle to **On**.

#### Configuration

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Environment settings**.
4. Select the relevant GCP connector.
5. Locate the Defender for Containers row and select **Settings**.

    [![Screenshot that shows the link for the settings are located.](media/quickstart-onboard-gcp/view-configuration.png)](media/quickstart-onboard-gcp/view-configuration.png#lightbox)
6. Toggle the switches to **On** or **Off**, depending on your need.

    [![Screenshot of Defender for Cloud's environment settings page showing the settings for the Containers plan.](media/tutorial-enable-containers-gcp/containers-settings-gcp.png)](media/tutorial-enable-containers-gcp/containers-settings-gcp.png#lightbox)
7. Select **Save**.
8. Continue from step 8 of the [Connect your GCP project](quickstart-onboard-gcp#connect-your-gcp-project) instructions.

---