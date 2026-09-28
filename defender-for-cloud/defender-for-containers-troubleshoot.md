---
layout: Conceptual
title: Troubleshoot Microsoft Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-troubleshoot
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
description: Troubleshoot common deployment and post-deployment issues in Microsoft Defender for Containers across supported Kubernetes environments.
ms.topic: troubleshooting
ms.date: 2026-01-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7b038f76-941e-1749-1094-37926ad1cf3e
document_version_independent_id: 47daadc3-3a9e-38e7-8d9b-2607653d6d12
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-troubleshoot.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-troubleshoot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6cf2543f-075f-2fe7-e688-67041cddff41
---

# Troubleshoot Microsoft Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn

This article provides troubleshooting guidance for common deployment and operational issues in Microsoft Defender for Containers across all supported environments.

# [Azure Kubernetes Service (AKS)](#tab/aks)
### Common deployment issues

- **Defender sensor installation fails**

    - **Symptoms:**`kubectl get pods -n kube-system -l app=defender` shows **Defender sensor** pods in `Pending`, `CrashLoopBackOff`, or `Error`.
    - **Resolution:**
        - **Insufficient resources:** Check node capacity. Use `kubectl top nodes` to verify if nodes have enough CPU and memory to schedule the sensor.
        - **Network egress:** Verify your cluster firewall or NSG allows outbound traffic to the [required FQDNs](defender-for-containers-azure-overview#prerequisites).
        - **Taints and Tolerations:** Ensure node taints aren't preventing the pods from scheduling on specific node pools.
- **Missing recommendations**

    - **Symptoms:** Clusters show as "Healthy" but specific recommendations like "AKS clusters should have **Defender profile** enabled" are missing.
    - **Resolution:**
        - **Wait time:** Assessment scans can take up to 24 hours to reflect in the dashboard.
        - **Exclusion tags:** Check if the resource has the tag `ms_defender_container_exclude_sensors` = `true`.
        - **Policy Add-on:** Ensure the Azure Policy add-on is installed; without it, configuration-based recommendations will not trigger.

### Vulnerability scan issues

- **Missing vulnerability findings for images in Azure Container Registry**

    - **Symptoms:** Vulnerability findings don't appear for images stored in Azure Container Registry.
    - **Resolution:**
        - **Registry scanning:** Confirm that the relevant registry scanning capability is enabled for Defender for Containers. In the Azure portal, verify that **Registry access** is enabled for the relevant scope.
        - **Further investigation:** If registry scanning is enabled and findings are still missing, open a support case with the registry name, image name, image digest, and expected finding details.
- **Missing vulnerability findings for images running on AKS clusters**

    - **Symptoms:** Vulnerability findings don't appear for images that are currently running in AKS workloads.
    - **Resolution:**
        - **Vulnerability scanning:** Confirm that the relevant vulnerability scanning capability is enabled for Defender for Containers. Runtime vulnerability findings depend on available scan results for the running image, such as registry scan or disk scan results.
        - **Pod inventory collection:** Confirm that pod inventory collection is enabled for the cluster. For AKS, pod inventory can be collected by the Defender sensor or by agentless collection, depending on the deployment configuration.
        - **Further investigation:** If vulnerability scanning and pod inventory collection are enabled but findings are still missing, open a support case with the cluster name, namespace, workload name, image name, and image digest.

# [Amazon Elastic Kubernetes Service (EKS)](#tab/eks)
### Connector and Discovery

- **AWS connector disconnected**

    - **CloudFormation status:** Check the AWS CloudFormation console to ensure the onboarding stack is in the `CREATE_COMPLETE` state.
    - **Permissions:** Verify the `MDCContainersAgentlessDiscoveryK8sRole` role has not been modified. This role is required for Defender for Cloud to discover your clusters via the EKS API.
- **EKS clusters not appearing in inventory**

    - **Kubernetes API access:** Ensure this component is toggled **On** in the AWS connector settings.
    - **IAM identity mapping:** Ensure the `aws-auth` ConfigMap has been updated to include the Defender for Cloud role, or that an **EKS Access Entry** has been created for the role.

### Vulnerability scan issues

- **Missing vulnerability findings for images in Amazon Elastic Container Registry**

    - **Symptoms:** Vulnerability findings don't appear for images stored in Amazon Elastic Container Registry.
    - **Resolution:**
        - **Registry scanning:** Confirm that the relevant registry scanning capability is enabled for Defender for Containers. In the AWS connector settings, verify that **Registry access** is enabled.
        - **Further investigation:** If registry scanning is enabled and findings are still missing, open a support case with the registry name, image name, image digest, and expected finding details.
- **Missing vulnerability findings for images running on EKS clusters**

    - **Symptoms:** Vulnerability findings don't appear for images that are currently running in EKS workloads.
    - **Resolution:**
        - **Vulnerability scanning:** Confirm that the relevant vulnerability scanning capability is enabled for Defender for Containers. Runtime vulnerability findings depend on available scan results for the running image, such as registry scan or disk scan results.
        - **Pod inventory collection:** Confirm that pod inventory collection is enabled for the cluster. Pod inventory can be collected by the Defender sensor or by agentless collection, depending on the deployment configuration.
        - **Connector and permissions:** Verify that the AWS connector and required cloud permissions are configured correctly.
        - **Further investigation:** If vulnerability scanning, pod inventory collection, and connector permissions are configured but findings are still missing, open a support case with the cluster name, namespace, workload name, image name, and image digest.

### Runtime Alerts

- **No control plane alerts generated**
    - **Audit logging:** Audit logs must be enabled for each cluster. Run: `aws eks update-cluster-config --name <cluster-name> --logging '{"clusterLogging":[{"types":["audit","authenticator"],"enabled":true}]}'`
    - **SQS Configuration:** Verify that CloudTrail is correctly sending logs to the SQS queue used by the connector. Verify that the SQS ARN is accurate in the connector settings.

# [Google Kubernetes Engine (GKE)](#tab/gke)
### Posture and Discovery

- **GKE Autopilot limitations**

    Important

    On GKE Autopilot clusters, you cannot manually configure or override resource limits for the Defender sensor. The sensor is designed to request the minimum resources required by Autopilot's specialized scheduling automatically.
- **Service Account errors**

    - **Service Account Email:** Confirm the Service Account email in the Azure portal matches the email generated in the GCP console.
    - **IAM Roles:** Ensure the Service Account has the `container.viewer` and `container.clusters.update` roles at the project level.

### Registry assessment issues

- **Missing vulnerability findings in Artifact Registry**

    - **Symptoms:** Vulnerability findings don't appear for images stored in Google Artifact Registry.
    - **Resolution:**
        - **Registry scanning:** Confirm that the relevant registry scanning capability is enabled for Defender for Containers. In the GCP connector settings, verify that **Registry access** is enabled.
        - **Further investigation:** If registry scanning is enabled and findings are still missing, open a support case with the registry name, image name, image digest, and expected finding details.
- **Missing vulnerability findings for images running on GKE clusters**

    - **Symptoms:** Vulnerability findings don't appear for images that are currently running in GKE workloads.
    - **Resolution:**
        - **Vulnerability scanning:** Confirm that the relevant vulnerability scanning capability is enabled for Defender for Containers. Runtime vulnerability findings depend on available scan results for the running image, such as registry scan or disk scan results.
        - **Pod inventory collection:** Confirm that pod inventory collection is enabled for the cluster. Pod inventory can be collected by the Defender sensor or by agentless collection, depending on the deployment configuration.
        - **Connector and permissions:** Verify that the GCP connector and required cloud permissions are configured correctly.
        - **Further investigation:** If vulnerability scanning and pod inventory collection are enabled but findings are still missing, open a support case with the cluster name, namespace, workload name, image name, and image digest.

# [Arc-enabled Kubernetes](#tab/arc)
### Arc Connectivity

- **Cluster status "Disconnected"**
    - **Network Egress:** Ensure the cluster can reach the required Azure Arc endpoints on TCP 443.
    - **Time Sync:** Ensure node system time is accurate and synced via NTP. If the node time drifts significantly, the Arc certificate handshake will fail, preventing components from deploying.
    - **Proxy configuration:** If your environment uses a proxy, ensure the Arc agents are configured with the correct `http_proxy` and `https_proxy` settings during the `az connectedk8s connect` step.

### Extension Management

- **Defender extension stuck in "Creating" or "Failed"**

    - **Agent logs:** Check the Arc agent logs for detailed errors: `kubectl logs -n azure-arc -l app.kubernetes.io/component=cluster-agent`
    - **Reinstallation:** If the extension remains stuck, delete and recreate it via CLI: `az k8s-extension delete --cluster-name <name> --resource-group <rg> --cluster-type connectedClusters --name microsoft.azuredefender.kubernetes`
- **Defender sensor pod "ImagePullBackOff"**

    - **Symptoms:** Pods fail to start with an image pull error.
    - **Resolution:**
        - **MCR Connectivity:** Verify nodes can reach `mcr.microsoft.com` to pull the **Defender sensor** image.
        - **Namespace conflicts:** Ensure no other security solutions or admission controllers are interfering with the `mdc` namespace.

---

## Verification via alert simulation

Use the [Kubernetes alerts simulation tool](alerts-containers#kubernetes-alerts-simulation-tool) to verify that Defender for Containers can generate alerts for your cluster and send them to Defender for Cloud.