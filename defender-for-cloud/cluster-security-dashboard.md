---
layout: Conceptual
title: Review Security Findings in the AKS Security Dashboard - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/cluster-security-dashboard
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
description: Learn how to investigate alerts, vulnerabilities, misconfigurations, and compliance findings in the AKS security dashboard in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: b41ed3e7-9ac8-47b0-dc49-aacf09dddecc
document_version_independent_id: 3c61b20b-388f-6f18-8184-585d99452fa3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/cluster-security-dashboard.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/cluster-security-dashboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/cluster-security-dashboard.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d8979d56-d0df-c3c8-81b8-a2d705082747
---

# Review Security Findings in the AKS Security Dashboard - Microsoft Defender for Cloud | Microsoft Learn

The AKS security dashboard shows security findings for an Azure Kubernetes Service (AKS) cluster in Microsoft Defender for Cloud. You can review, investigate, and remediate security alerts, vulnerabilities, misconfigurations, and compliance findings in the dashboard.

## Prerequisites

To use the AKS security dashboard, ensure you have:

- A Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) enabled with one of the following plans:

    - [Defender for Containers](tutorial-enable-containers-azure)
    - [Defender Cloud Security Posture Management (Defender CSPM)](tutorial-enable-cspm-plan)

## Review security findings

Use the following sections to review alerts, vulnerabilities, misconfigurations, and compliance results in the AKS security dashboard.

## Security alerts

Security alerts indicate suspicious activity or potential threats detected in the cluster.

For example, the **Exposed Kubernetes service detected** alert is raised when a Kubernetes Service of type `LoadBalancer` is created or updated and publicly exposes workloads. Prioritize this alert when exposure is unintended, or when internet-facing services have weak or missing authentication.

Alerts are prioritized by severity to help you identify which issues to investigate first:

- **High**: High probability that the resource is compromised. Investigate immediately.
- **Medium**: Indicates suspicious activity that might represent a compromise.
- **Low**: Might indicate a benign or blocked activity.
- **Informational**: Provides context and might be relevant when correlated with other alerts.

### Investigate a security alert

To investigate a security alert:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Kubernetes services** &gt; **Clusters**.
3. Select the relevant AKS cluster.
4. Select **Microsoft Defender for Cloud**.
5. In the **Security alerts** tab, select an alert to open the details pane.

In the details pane:

- Review the alert details and recommended remediation steps.
- Use related entities to identify affected resources.
- Select **Open logs** to investigate activity within the relevant timeframe.
- Create a suppression rule if the alert isn't relevant for your organization.
- Configure security rules for supported alert types.

After you mitigate the issue, update the alert status.

[![Screenshot of the Security alerts tab showing alert details.](media/cluster-security-dashboard/alerts-tab-security-findings.png)](media/cluster-security-dashboard/alerts-tab-security-findings.png#lightbox)

## Vulnerability assessment

The vulnerability assessment section shows vulnerabilities for running container images and Kubernetes node pools.

Findings are prioritized by severity. When Defender CSPM is enabled, prioritization also considers contextual risk signals.

Each finding includes affected packages, associated common vulnerabilities and exposures (CVEs), and the fixed version to remediate the issue.

Vulnerabilities can include:

- **OS packages** (Linux and Windows)
- **Language-specific packages** (Linux)

For supported configurations, see the [support matrix for Defender for Containers](/en-us/azure/defender-for-cloud/support-matrix-defender-for-containers).

### Review vulnerability findings

To review vulnerability findings:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Kubernetes services** &gt; **Clusters**.
3. Select the relevant AKS cluster.
4. Select **Microsoft Defender for Cloud**.
5. In the **Vulnerabilities** tab, select a component to open the details pane.

In the details pane:

- Review affected packages and associated CVEs.
- Identify the fixed version for the vulnerable package.
- Update the container image or dependency to fix the issue.

If expected vulnerabilities don't appear, verify that the image, package type, and environment are supported. See the [support matrix for Defender for Containers](/en-us/azure/defender-for-cloud/support-matrix-defender-for-containers).

[![Screenshot of the Vulnerabilities tab showing vulnerable components and severity.](media/cluster-security-dashboard/vulnerabilities-assessment-tab.png)](media/cluster-security-dashboard/vulnerabilities-assessment-tab.png#lightbox)

## Misconfigurations

Misconfigurations identify security configuration issues in Kubernetes resources, cluster settings, and running workloads.

Findings are based on Azure Policy and Kubernetes configuration assessments.

Review these findings with network exposure in mind, including Kubernetes service types and ingress configurations that can unintentionally expose workloads to the internet.

Each finding includes remediation guidance. Some findings support automated remediation through **Quick Fix** or policy enforcement.

### Review and remediate misconfigurations

To review and remediate misconfigurations:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Kubernetes services** &gt; **Clusters**.
3. Select the relevant AKS cluster.
4. Select **Microsoft Defender for Cloud**.
5. In the **Misconfigurations** tab, select a finding to open the details pane.

In the details pane:

- Review the description and remediation steps.
- Review Kubernetes service types and ingress exposure settings to reduce unintended internet-facing access.
- For cluster-level misconfigurations, select **Quick Fix** when available.
- For workload issues, apply the recommended Azure Policy to prevent recurrence.
- Assign an owner to track remediation (requires Defender CSPM).

[![Screenshot of the Misconfigurations tab displaying security configuration issues.](media/cluster-security-dashboard/misconfigurations-assessment-tab.png)](media/cluster-security-dashboard/misconfigurations-assessment-tab.png#lightbox)

## Compliance

The compliance section shows the cluster's status against regulatory standards and benchmarks.

It lists controls that the cluster doesn't meet and provides recommendations to help you remediate them.

### Assess compliance

To assess compliance:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Kubernetes services** &gt; **Clusters**.
3. Select the relevant AKS cluster.
4. Select **Microsoft Defender for Cloud**.
5. In the **Compliance** tab, review failing controls.
6. Select a control to open the details pane.

In the details pane:

- Review the recommendation and remediation steps.
- Apply the required changes to meet the control.

[![Screenshot of the Compliance tab showing regulatory compliance assessment results.](media/cluster-security-dashboard/compliance-standards-tab.png)](media/cluster-security-dashboard/compliance-standards-tab.png#lightbox)