---
layout: Conceptual
title: Kubernetes Misconfiguration Enforcement - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/kubernetes-misconfiguration-enforcement
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
description: Learn about Kubernetes misconfiguration enforcement in Microsoft Defender for Containers to audit or block misconfigured workloads at deployment time.
ms.custom: msecd-doc-authoring-1013
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: 65f4703d-0523-c50e-b368-c8882b2eeca7
document_version_independent_id: e507f4dc-fc7f-9e94-d344-c62cb17db7f2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/kubernetes-misconfiguration-enforcement.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/kubernetes-misconfiguration-enforcement
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/kubernetes-misconfiguration-enforcement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
platformId: dfdae6a8-3ed1-2bbe-765b-59f152b4c0dd
---

# Kubernetes Misconfiguration Enforcement - Microsoft Defender for Cloud | Microsoft Learn

Kubernetes misconfiguration enforcement is a Microsoft Defender for Containers capability that evaluates Kubernetes resources before they're admitted into a cluster. Use it to audit or block deployments that don't meet Microsoft security best-practice rules.

After you enable the feature, Defender for Containers creates a default security rule named **Default K8s misconfiguration rule**. The default rule is created in **Audit** mode and applies to all Kubernetes clusters in scope. You can change the rule action to **Block**, configure individual rules and parameters, or create custom policies for specific scopes.

Use Kubernetes misconfiguration enforcement to help:

- Audit or block Kubernetes workloads with unsafe security configurations.
- Enforce non-root execution and approved user or group IDs.
- Prevent automatic mounting of Kubernetes API credentials.
- Block workloads from running in the default Kubernetes namespace.
- Prevent containers from sharing sensitive host namespaces, such as PID, IPC, or network.
- Restrict container images to trusted registries or approved patterns.
- Enforce CPU and memory limits.
- Require HTTPS for Kubernetes Ingress resources.
- Block privilege escalation and fully privileged containers.
- Require containers to use a read-only root filesystem.

## Prerequisites

Before you begin, ensure that:

- [Defender for Containers is enabled on the subscription or cloud account](defender-for-containers-enable-plan) where the Kubernetes cluster is running.
- Your Kubernetes cluster is supported.
- The cluster uses AKS, Azure Arc-enabled Kubernetes, EKS, or GKE.
- **If you're using automatic provisioning:** The required Defender for Containers components are enabled for your environment:

    - **AKS and Azure Arc-enabled Kubernetes**: Kubernetes API access is enabled.
    - **AWS and GCP**: Agentless threat protection is enabled to collect audit logs.

    Note

    Agentless threat protection is enabled by default when you enable Defender for Containers for AWS or GCP. If it was disabled, enable it before you configure Kubernetes misconfiguration enforcement.
- **If you're using Helm for manual deployment:** Make sure Helm is installed ([Helm installation instructions](https://helm.sh/docs/intro/install/)) and available in your command-line environment. Then, manually enable misconfiguration enforcement with Helm.
- Kubernetes ValidatingAdmissionPolicy is enabled on the cluster. Kubernetes 1.30 and later versions enable this capability by default.
- You have the required permissions:

    - To enable and manage deployment-time enforcement policies, you need **Subscription Owner** or **Security Admin** permissions.
    - To view policies and monitoring information, you need **Security Reader** or equivalent permissions.

## Manually enable misconfiguration enforcement with Helm

To manually enable misconfiguration enforcement with Helm:

1. Follow the [Helm installation guide for the Defender for Containers sensor](deploy-helm) for your environment.
2. During Helm chart installation, use the latest supported chart tag. Use the following OCI artifact reference to select the Microsoft Defender for Containers policy bundle during gated deployment configuration:

    ```bash
    oci://mcr.microsoft.com/azuredefender-preview/microsoft-defender-for-containers
    ```
3. Set the following Helm value to enable misconfiguration policies in the Defender admission controller so that policy enforcement is applied to your cluster:

    ```bash
    defender-admission-controller.enableMisconfigurationPolicies=true
    ```

After misconfiguration enforcement is enabled, the default audit rule is created automatically in the portal.

## Create a misconfiguration enforcement policy

By default, Defender for Containers creates the **Default K8s misconfiguration rule** in **Audit** mode, scoped to all resources. The admission controller is the Kubernetes component that evaluates resources against your policies before they're admitted into the cluster. While in **Audit** mode, the admission controller logs violations but allows deployments to continue. You can create custom policies scoped to specific subscriptions, clusters, or namespaces.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Security rules**.

    [![Screenshot of the Security Rules tile in Environment Settings.](media/kubernetes-misconfiguration-enforcement/security-rules.png)](media/kubernetes-misconfiguration-enforcement/security-rules.png#lightbox)
4. Select **Gated deployment** &gt; **Misconfigurations** to view available policies.

    [![Screenshot of the Misconfiguration tab in Security Rules showing the default policy.](media/kubernetes-misconfiguration-enforcement/misconfigurations.png)](media/kubernetes-misconfiguration-enforcement/misconfigurations.png#lightbox)
5. Select **Create new policy**.
6. Enter a **Policy name**.

    [![Screenshot of the Create new policy panel showing Policy name and Action fields.](media/kubernetes-misconfiguration-enforcement/create-new-policy.png)](media/kubernetes-misconfiguration-enforcement/create-new-policy.png#lightbox)
7. Select an **Action**:

    - **Audit**: Logs violations without blocking deployments.
    - **Block**: Denies noncompliant deployments.

    Note

    Selecting **Block** mode can introduce a short delay during deployments because of real-time policy enforcement.
8. If needed, enter a **Rule description**.
9. Enter a **Scope name**.
10. Select the **Cloud scope**.
11. Under **Resource scope**, keep the default scope or select **Add condition** to narrow the rule scope.
12. Select **Next**.
13. Select each rule that you want to enable.

    [![Screenshot of the Rules tab showing individual rules that can be enabled or disabled.](media/kubernetes-misconfiguration-enforcement/choose-policy-rules.png)](media/kubernetes-misconfiguration-enforcement/choose-policy-rules.png#lightbox)
14. To configure parameters for a rule, select the rule name.

    Some rules include configurable parameters. If parameters are available, update them as needed, and then select **Save**.

    [![Screenshot of the rule configuration panel showing customizable parameters and their default values.](media/kubernetes-misconfiguration-enforcement/configure-rule.png)](media/kubernetes-misconfiguration-enforcement/configure-rule.png#lightbox)
15. Select **Next**.
16. Review the policy configuration.
17. Select **Add policy**.

## Edit a misconfiguration enforcement policy

You can edit an existing misconfiguration enforcement policy to update its action, enabled rules, and configurable rule parameters.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Security rules**.
4. Select **Gated deployment** &gt; **Misconfigurations**.
5. Select the policy that you want to edit.
6. Select **Edit**.
7. Update the policy settings as needed.
8. Select **Save policy**.

### Default policy limitations

The built-in **Default K8s misconfiguration rule** has the following limitations:

- You can change the **Action** between **Audit** and **Block**.
- You can enable or disable individual rules.
- You can configure parameters for rules that support customization.
- You can't edit the policy name, description, or scope.

Custom policies you create don't have these restrictions.

## Built-in misconfiguration rules

Kubernetes misconfiguration enforcement includes built-in rules based on Microsoft security best practices.

Built-in rules help enforce controls for:

- **Container resource limits (CPU and memory)**: Ensures containers don't exceed specified limits to prevent resource exhaustion.
- **Privilege and capability management**: Prevents containers from running with elevated privileges, unnecessary Linux capabilities, or privilege escalation paths.
- **Non-root execution**: Enforces non-root user and group IDs so containers can't run with excessive OS privileges.
- **API credential mounting**: Prevents containers from automatically mounting Kubernetes API credentials.
- **Default namespace**: Blocks workloads from running in the default Kubernetes namespace.
- **Host namespace isolation**: Blocks containers from sharing the host PID, IPC, or network namespace.
- **Trusted image sources**: Restricts container images to trusted registries or approved patterns.
- **Network security**: Enforces HTTPS for Kubernetes Ingress resources.
- **Runtime security**: Requires containers to use a read-only root filesystem and blocks fully privileged containers.

You can enable or disable individual rules within a policy and configure parameters for rules that support customization.