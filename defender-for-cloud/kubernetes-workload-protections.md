---
layout: Conceptual
title: Kubernetes Data Plane Hardening - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/kubernetes-workload-protections
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
description: Review Kubernetes data plane hardening recommendations in Microsoft Defender for Cloud and enforce secure workload settings across your clusters.
ms.topic: how-to
ms.date: 2026-08-07T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 18136a1d-fc0a-6b42-6210-7a58e4d8cc25
document_version_independent_id: fb428726-7cb2-1341-632a-fa50eeba8154
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/kubernetes-workload-protections.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/kubernetes-workload-protections
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/kubernetes-workload-protections.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 3d0266a0-c52b-b148-7cf2-b97cbabbf7ea
---

# Kubernetes Data Plane Hardening - Microsoft Defender for Cloud | Microsoft Learn

Kubernetes data plane hardening helps enforce secure configurations for workloads running in your cluster, such as restricting privileged containers, enforcing resource limits, and limiting network access.

In Defender for Cloud, you implement data plane hardening by using [Azure Policy for Kubernetes](defender-for-cloud-glossary#azure-policy-for-kubernetes) to evaluate and enforce these configurations. Microsoft Defender for Containers automatically deploys Azure Policy when you enable automatic provisioning.

If you turn off Azure Policy for Kubernetes in the Defender for Containers plan settings, you can deploy it by remediating the relevant recommendation. You can also deploy Azure Policy manually by using [Azure CLI to deploy Defender for Containers components](defender-for-containers-deploy-azure-cli) or [Helm to deploy Defender for Containers components](deploy-helm) if you disable automatic provisioning during enablement or exclude specific clusters from automatic provisioning.

After you deploy Azure Policy for Kubernetes, Defender for Cloud generates data plane hardening recommendations based on your cluster configuration. You can review these recommendations, configure policy parameters, and enforce them on your clusters.

## Prerequisites

To begin, ensure that you:

- [Enable Defender for Containers on your subscription](defender-for-containers-enable-plan).
- Add the [required FQDN/application rules for Azure policy](/en-us/azure/aks/outbound-rules-control-egress#azure-policy).
- (For non-AKS clusters) [Connect your Kubernetes cluster to Azure Arc](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster).

## Enable Azure Policy for Kubernetes by remediating recommendations

If you didn't deploy Azure Policy for Kubernetes or turned it off in the Defender for Containers plan settings, install it by remediating the recommendation that matches your cluster type in Defender for Cloud.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Search for the relevant recommendation:

    - **Azure**: Azure Kubernetes Service clusters should have the Azure Policy add-on for Kubernetes installed
    - **GCP**: GKE clusters should have the Azure Policy extension installed
    - **AWS/Arc-enabled Kubernetes**: Azure Arc-enabled Kubernetes clusters should have the Azure Policy extension installed

    [![Screenshot showing the Azure Kubernetes service clusters recommendation.](media/kubernetes-workload-protections/azure-kubernetes-service-clusters-recommendation.png)](media/kubernetes-workload-protections/azure-kubernetes-service-clusters-recommendation.png#lightbox)
4. Select a recommendation.
5. In the **Take action** tab, select **Fix**.

    [![Screenshot of a recommendation with the Fix button highlighted.](media/kubernetes-workload-protections/azure-kubernetes-service-clusters-recommendation-fix.png)](media/kubernetes-workload-protections/azure-kubernetes-service-clusters-recommendation-fix.png#lightbox)
6. Select **Fix** to remediate the selected resources.
7. Repeat for each recommendation.

## Data plane hardening recommendations

After you deploy Azure Policy for Kubernetes, Defender for Cloud evaluates your cluster configuration and generates data plane hardening recommendations. This process can take up to 30 minutes.

Note

Microsoft components, such as the Defender sensor, are deployed in the `kube-system` namespace by default and aren't marked as noncompliant. Third-party components installed in other namespaces might be flagged. To exclude specific namespaces, configure Azure policy exclusions.

The following table lists common data plane hardening recommendations:

| Recommendation name | Security control | Configuration required |
| --- | --- | --- |
| Container CPU and memory limits should be enforced | Protect applications against DDoS attack | **Yes** |
| Container images should be deployed from trusted registries only | Remediate vulnerabilities | **Yes** |
| Least privileged Linux capabilities should be enforced for containers | Manage access and permissions | **Yes** |
| Containers should only use allowed AppArmor profiles | Remediate security configurations | **Yes** |
| Services should listen on allowed ports only | Restrict unauthorized network access | **Yes** |
| Usage of host networking and ports should be restricted | Restrict unauthorized network access | **Yes** |
| Usage of pod HostPath volume mounts should be restricted to a known list | Manage access and permissions | **Yes** |
| Container with privilege escalation should be avoided | Manage access and permissions | No |
| Containers sharing sensitive host namespaces should be avoided | Manage access and permissions | No |
| Immutable (read-only) root filesystem should be enforced for containers | Manage access and permissions | No |
| Kubernetes clusters should be accessible only over HTTPS | Encrypt data in transit | No |
| Kubernetes clusters should disable automounting API credentials | Manage access and permissions | No |
| Kubernetes clusters shouldn't use the default namespace | Implement security best practices | No |
| Kubernetes clusters shouldn't grant CAP\_SYS\_ADMIN capabilities | Manage access and permissions | No |
| Privileged containers should be avoided | Manage access and permissions | No |
| Running containers as root user should be avoided | Manage access and permissions | No |

### View recommendations for a cluster

To view data plane hardening recommendations for a specific cluster:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Defender for Cloud** &gt; **Inventory**.
3. Set the resource type filter to **Kubernetes service** and select **Apply**.

    [![Screenshot of using the resource type filter to select kubernetes service.](media/kubernetes-workload-protections/resource-type-kubernetes-service.png)](media/kubernetes-workload-protections/resource-type-kubernetes-service.png#lightbox)
4. Select the relevant cluster.
5. Review the available recommendations. Data plane hardening recommendations show the number of affected Kubernetes components.
6. Select a recommendation to view affected resources.

    [![Screenshot of selecting a recommendation from the Resource health page.](media/kubernetes-workload-protections/resource-health-recommendation.png)](media/kubernetes-workload-protections/resource-health-recommendation.png#lightbox)
7. Select **Take action** to review remediation options.

    [![Screenshot of the Take action tab, used to view remediation steps for a recommendation.](media/kubernetes-workload-protections/take-action-tab.png)](media/kubernetes-workload-protections/take-action-tab.png#lightbox)

## Configure policy parameters

Some recommendations include parameters that limit the Kubernetes resources evaluated by the underlying Azure Policy. For example, the policy for **Immutable (read-only) root filesystem should be enforced for containers** includes the `excludedContainers`, `excludedImages`, and `excludedNamespaces` parameters.

Container exclusions match container names. Image exclusions support prefix matching when the value ends in `*`, such as `myregistry.azurecr.io/istio:*`. Use a fully qualified image name to avoid unintentionally excluding an image from an untrusted registry.

Other recommendations require parameter configuration to be effective. For example, the recommendation **Container images should be deployed from trusted registries only** requires you to define a list of trusted registries.

If required parameters aren't configured, resources are shown as unhealthy.

To configure policy parameters:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Select **Security policies**.

    [![Screenshot of the Security policies page.](media/kubernetes-workload-protections/security-policies-page.png)](media/kubernetes-workload-protections/security-policies-page.png#lightbox)
5. On the **Standards** tab, select the relevant security standard.
6. Select the relevant policy assignment's three-dot menu and select **Manage effect and parameters**.

    [![Screenshot of selecting the three-dot menu and then selecting Manage effect and parameters.](media/kubernetes-workload-protections/select-manage-effect-and-parameters.png)](media/kubernetes-workload-protections/select-manage-effect-and-parameters.png#lightbox)
7. Update the required parameter values.

    [![Screenshot of the parameters panel.](media/kubernetes-workload-protections/manage-effect-and-parameters.png)](media/kubernetes-workload-protections/manage-effect-and-parameters.png#lightbox)
8. Select **Save**.

## Enforce data plane hardening policies

By default, policies evaluate resources in audit mode. To enforce a policy, set its effect to **Deny**.

To enforce a recommendation:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Search for and select the relevant data plane hardening recommendation.
4. On the **Take action** tab, select **Deny**.

    [![Screenshot showing the Deny option for Azure Policy parameter.](media/kubernetes-workload-protections/enforce-workload-protection-example.png)](media/kubernetes-workload-protections/enforce-workload-protection-example.png#lightbox)
5. Set the scope.
6. Select **Change to deny**.

## Test policy enforcement

You can validate data plane hardening policies by deploying test workloads.

- A compliant deployment that meets data plane hardening requirements
- A noncompliant deployment that violates multiple policies

Deploy the following example YAML files to verify that compliant workloads are deployed successfully and noncompliant workloads are flagged or blocked, depending on policy enforcement settings.

### Compliant deployment example

The following deployment uses a trusted container registry, enforces CPU and memory limits, and applies a restrictive security context that disables privilege escalation and runs as a non-root user.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-healthy-deployment
  labels:
    app: redis
spec:
  replicas: 3
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
      annotations:
        container.apparmor.security.beta.kubernetes.io/redis: runtime/default
    spec:
      containers:
      - name: redis
        image: <customer-registry>.azurecr.io/redis:latest
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 100m
            memory: 250Mi
        securityContext:
          privileged: false
          readOnlyRootFilesystem: true
          allowPrivilegeEscalation: false
          runAsNonRoot: true
          runAsUser: 1000
---
apiVersion: v1
kind: Service
metadata:
  name: redis-healthy-service
spec:
  type: LoadBalancer
  selector:
    app: redis
  ports:
  - port: 80
    targetPort: 80
```

### Noncompliant deployment example

The following deployment intentionally violates multiple data plane hardening policies, including running a privileged container as root, enabling host networking and shared namespaces, and mounting a host path volume.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-unhealthy-deployment
  labels:
    app: redis
spec:
  replicas: 3
  selector:
    matchLabels:
      app: redis
  template:
    metadata:      
      labels:
        app: redis
    spec:
      hostNetwork: true
      hostPID: true 
      hostIPC: true
      containers:
      - name: redis
        image: redis:latest
        ports:
        - containerPort: 9001
          hostPort: 9001
        securityContext:
          privileged: true
          readOnlyRootFilesystem: false
          allowPrivilegeEscalation: true
          runAsUser: 0
          capabilities:
            add:
              - NET_ADMIN
        volumeMounts:
        - mountPath: /test-pd
          name: test-volume
          readOnly: true
      volumes:
      - name: test-volume
        hostPath:
          # directory location on host
          path: /tmp
---
apiVersion: v1
kind: Service
metadata:
  name: redis-unhealthy-service
spec:
  type: LoadBalancer
  selector:
    app: redis
  ports:
  - port: 6001
    targetPort: 9001
```