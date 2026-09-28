---
layout: Conceptual
title: Troubleshoot Gated Deployment in Kubernetes - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/troubleshooting-runtime-gated
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
description: Troubleshoot Gated Deployment in Kubernetes with this guide. Resolve onboarding, rule configuration, and exclusion issues to secure your container images.
ms.date: 2025-10-29T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: b20a23dd-bb14-084f-101c-e22712244782
document_version_independent_id: ce41ca9f-e5e9-7948-6860-581fe948d886
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/troubleshooting-runtime-gated.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/troubleshooting-runtime-gated
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/troubleshooting-runtime-gated.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cb49e66a-8528-497d-adaa-eade2d009d1b
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/472c9d15-157b-443c-afa2-e209c8fecf58
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 549400f3-8f52-0996-90d1-47d6d52a650f
---

# Troubleshoot Gated Deployment in Kubernetes - Microsoft Defender for Cloud | Microsoft Learn

This article helps you fix common issues when you set up or use gated deployment in Kubernetes with Microsoft Defender for Containers.

Gated deployment enforces container image security policies at deploy time based on vulnerability scan results from supported container registries. It integrates with the Kubernetes admission controller to check images before they enter the cluster.

## Onboarding and configuration issues

### Issue: Gated deployment isn't active after enabling Defender for Containers

**Possible causes:**

- Required plan extensions are disabled
- Defender Sensor is disabled or not provisioned to the cluster
- Kubernetes cluster version is earlier than 1.31
- Defender for Containers plan or relevant extensions (Registry Access or Security Findings extensions) are disabled in the container registry scope

**Resolution:**

- Confirm the following toggles are enabled in the Defender for Containers plan:

    - Defender Sensor
    - Security Gating
    - Registry Access
    - Security Findings
- Make sure your Kubernetes cluster runs version 1.31 or later.
- For Azure: Check that the cluster has access to the container registry (ACR) and that Microsoft Entra ID authentication is configured. For AKS clusters, make sure the cluster has a *kubelet* identity, and that the admission controller pod's service account is included in the *kubelet* identity's federated credentials.

### Issue: Security rule doesn't trigger

**Possible causes:**

- Rule scope doesn't match the deployed resource.
- CVE conditions aren't met.
- The image deploys before scan results are available.
- The vulnerability findings artifact isn't available for the image in the container registry.

**Resolution:**

- Check the rule scope and matching criteria.
- Check that the image has vulnerabilities that match the rule conditions.
- Make sure the image is in a supported container registry. The registry must belong to a subscription, account, or project with Registry Access and Security Findings enabled.
- Make sure Defender for Cloud scans the image before deployment. If it doesn't, gating doesn't apply.

    Note

    Defender for Containers scans an image in a supported container registry within a few hours after the initial push event. For more information about scanning triggers, see [Vulnerability assessments for Defender for Container supported environments](/en-us/azure/defender-for-cloud/agentless-vulnerability-assessment-azure?tabs=azure-new%2Cazure-old#scanning-images-in-defender-for-containers-supported-registries).
- For ACR images, check that the vulnerability findings artifact is available and signed:

    1. Sign in to the [Azure portal](https://portal.azure.com).
    2. Go to **Container registries**.
    3. Select the relevant registry.
    4. Select **Repositories**.
    5. Select the repository and image tag or digest.
    6. Select the **Referrers** tab.
    7. Confirm that the image has a vulnerability findings artifact and a signature.

    [![Screenshot of an Azure Container Registry image Referrers tab showing a vulnerability findings artifact and signature artifact.](media/troubleshooting-runtime-gated/container-registries-security-artifact.png)](media/troubleshooting-runtime-gated/container-registries-security-artifact.png#lightbox)

If the artifact or signature is missing, gated deployment can't validate the image. Confirm that the image was scanned and that **Security findings** is enabled for the registry scope.

### Issue: Exclusion not applied

**Possible causes:**

- The exclusion scope doesn't match the resource.
- The exclusion expired.
- The matching criteria are misconfigured.

**Resolution:**

- Review the exclusion configuration when you create the rule.
- Confirm the exclusion is still active.
- Check that the resource (like image, pod, or namespace) matches the exclusion criteria.

[![Screenshot of exemption configuration panel with time-bound toggle.](media/enablement-guide-runtime-gating/exemption-configuration-panel.png)](media/enablement-guide-runtime-gating/exemption-configuration-panel.png#lightbox)

## Developer experience and CI/CD integration

Gated deployment enforces policies when you deploy. You might see specific messages or behaviors when you deploy container images.

### Common developer messages

| **Scenario** | **Message** |
| --- | --- |
| Image blocked due to CVE | Error from server: admission webhook "defender-admission-controller.kube-system.svc" denied the request: mcr.microsoft.com/mdc/dev/defender-admission-controller/test-images:one-high:Image contains 2 high or higher CVEs, which is more than the allowed count of: 0” |
| Image blocked because scan results are missing | No valid reports found on ratify response  Unscanned images are not allowed by policy |
| Image allowed but monitored (audit mode) | Admission request allowed. A security scan runs in the background (audit mode). Learn more: https://aka.ms/KubernetesDefenderAuditRule |
| Image allowed without scan results (audit mode) | Admission request allowed. A security scan runs in the background (audit mode). Learn more: [https://aka.ms/KubernetesDefenderAuditRule|](https://aka.ms/KubernetesDefenderAuditRule%7C) |

[![Screenshot of Admission Monitoring view showing developer-facing results.](media/enablement-guide-runtime-gating/admission-monitoring.png)](media/enablement-guide-runtime-gating/admission-monitoring.png#lightbox)