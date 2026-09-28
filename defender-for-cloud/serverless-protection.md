---
layout: Conceptual
title: What is Serverless protection? - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/serverless-protection
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
description: Learn how Serverless protection in Microsoft Defender for Cloud helps secure serverless resources across Azure and AWS.
ms.topic: overview
ms.date: 2026-08-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e0526dd2-13d8-6c15-fc5a-4c3bcd41e22e
document_version_independent_id: 36ce191e-61b5-488e-baa0-06991d8ee0d3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/serverless-protection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/serverless-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/serverless-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: bf5ea159-8f77-b8e9-b953-5849a763f486
---

# What is Serverless protection? - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud, as a cloud-native application protection platform (CNAPP), delivers visibility, security, and posture management for serverless workloads across multicloud environments. It extends coverage to Azure Web Apps, Azure Functions, and Amazon Web Services (AWS) Lambda.

Serverless protection automatically discovers and inventories Web Apps, Azure Functions, and AWS Lambda functions in your environment. After discovery, Defender for Cloud identifies misconfigurations, vulnerabilities, and insecure dependencies. It then provides remediation guidance and continuous posture assessment to help organizations reduce risk in dynamic serverless architectures.

Learn more about the [cloud availability](support-matrix-defender-for-cloud#cloud-support) for this feature.

## Serverless protection requirements and availability

Note

Starting August 18, stale recommendations will be removed. This change may impact your secure score if the recommendations were present in your subscriptions. To keep serverless coverage for your subscriptions, make sure to enable Serverless protection following the steps shared below (billing applies).

Serverless protection is available as part of the [Defender cloud security posture management (Defender CSPM) plan](concept-cloud-security-posture-management#cspm-plans).

To enable serverless protection, you must [enable the Defender CSPM plan](tutorial-enable-cspm-plan) on your subscription and [enable the Serverless protection component](tutorial-enable-cspm-plan#enable-the-components-of-the-defender-cspm-plan) of that plan.

Currently, the available features vary by portal. The following table shows which features are available in each portal:

| Feature | Defender for Cloud portal | Defender portal |
| --- | --- | --- |
| Onboarding through the Defender CSPM plan | ![](media/icons/yes-icon.png) | ![](media/icons/no-icon.png) |
| Review misconfiguration recommendations | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Build queries with Cloud Security Explorer | ![](media/icons/yes-icon.png) | ![](media/icons/no-icon.png) |
| Explore workloads in Cloud Inventory | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Investigate attack paths | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Vulnerability assessment | - | ![](media/icons/yes-icon.png) |

To view the availability, see [cloud support](support-matrix-defender-for-cloud#cloud-support).

See limitations for serverless resources.

## Benefits of serverless protection

Defender for Cloud extends its CSPM capabilities to serverless workloads by providing continuous visibility and risk assessment with the following features:

- **Automatic resource discovery**: Detects all serverless resources (Azure Functions, Web Apps, AWS Lambda) and lists them in a unified inventory.
- **Continuous posture assessment**: Evaluates configurations for risks like public endpoints, weak authentication, and missing encryption.
- **Misconfiguration detection**: Highlights risks in:
    - **Access control**: Restricts network exposure and enforces authentication.
    - **Identity and permissions**: Helps prevent lateral movement, data exfiltration, and privilege abuse.
    - **Code integrity**: Helps protect against unauthorized code changes, such as AWS Lambda code signing bypass risks.
- **Vulnerability assessment**: Scans function packages for vulnerable dependencies and provides remediation guidance.
- **Attack path analysis**: Maps potential attack chains that involve serverless resources so you can prioritize high-risk issues.

Defender for Cloud uses these features to help organizations secure serverless workloads in dynamic cloud environments.

Beyond these core benefits, serverless security in Defender for Cloud aligns with the broader CNAPP vision to secure applications throughout their lifecycle.

Serverless protection is also integrated into the Defender portal. This integration provides visibility for misconfiguration detection, attack path analysis, and vulnerability assessment in a single interface.

View the [serverless protection security recommendations](recommendations-reference-serverless-protection).

## How serverless protection works

Serverless protection in Defender for Cloud works through a combination of automated discovery, continuous monitoring, and risk assessment. When you enable the Defender CSPM plan and activate the serverless protection component, Defender for Cloud scans your cloud environment to identify all serverless resources, including Azure Web Apps, Azure Functions, and AWS Lambda functions.

After Defender for Cloud discovers the resources, it continuously monitors their configurations and runtime environments. It evaluates these resources against a set of security best practices and compliance standards to identify misconfigurations, vulnerabilities, and insecure dependencies. When it detects a risk, Defender for Cloud generates security recommendations with detailed remediation steps to help you address the issues.

## Enable Serverless protection for your environment

Use the following steps to enable Serverless protection for each environment. You need the appropriate permissions to change Defender CSPM settings.

### Azure

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the Azure subscription where you want to enable Serverless protection.
4. Select **Defender CSPM** and turn on the **Serverless protection** toggle.

    [![Screenshot that shows the Serverless protection component turned on in the Defender CSPM plan settings for an Azure subscription.](media/serverless-protection/enable-serverless-protection-azure.png)](media/serverless-protection/enable-serverless-protection-azure.png#lightbox)
5. Select **Save and close**.

Repeat these steps for each Azure subscription that requires serverless coverage.

### AWS

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the connected AWS account where you want to enable Serverless protection.
4. Select **Defender CSPM** and turn on the **Serverless protection** toggle.

    [![Screenshot that shows the Serverless protection component turned on in the Defender CSPM plan configuration for a connected AWS account.](media/serverless-protection/enable-serverless-protection-aws.png)](media/serverless-protection/enable-serverless-protection-aws.png#lightbox)
5. Select **Save and close**.

Repeat these steps for each connected AWS account that requires serverless coverage.

### Inventory

Defender for Cloud provides a unified inventory of all discovered serverless resources, so you can easily view and manage them. The inventory page includes details such as resource names, types, locations, and associated security findings. Simply filter the results based on resource type to focus on Web Apps, Azure Functions, or AWS Lambda functions.

[![Cloud inventory page filtered to serverless resources, showing Azure Web Apps, Azure Functions, and AWS Lambda entries.](media/serverless-protection/serverless-inventory.png)](media/serverless-protection/serverless-inventory.png#lightbox)

After you filter your results, select a resource to view details about its security posture, including active security recommendations and their severity levels.

[![Resource details page for a serverless workload showing security health, active recommendations, and severity information.](media/serverless-protection/resource-health.png)](media/serverless-protection/resource-health.png#lightbox) You can also review the security recommendations associated with each resource to prioritize remediation based on finding severity.

Learn how to [remediate security recommendations](implement-security-recommendations).

### Cloud Security Explorer

Defender for Cloud's Cloud Security Explorer provides advanced filtering and query capabilities so you can analyze the security posture of your serverless resources. You can create custom queries to identify specific misconfigurations or vulnerabilities across your serverless workloads.

[![Screenshot of the Cloud Security Explorer page with a query specific to serverless protection entered.](media/serverless-protection/serverless-cloud-security-explorer.png)](media/serverless-protection/serverless-cloud-security-explorer.png#lightbox)

Learn how to [build queries with Cloud Security Explorer](how-to-manage-cloud-security-explorer).

## Limitations

Serverless resources that aren't eligible for vulnerability assessment include:

- Web Apps and function apps that don't have a Running power state.
- Web Apps and function apps that have public network access disabled.
- Web Apps and function apps with the following kind values:
    - `app,migration`
    - `functionapp,botapp`
    - `app,linux,aspiredashboard`
    - `app,container,xenon`
    - `app,botapp`
    - `app,linux,Kubernetes`
    - `app,functionapp,windows`
    - `functionapp,linux,container,Kubernetes`
    - `app,linux,container,Kubernetes`
    - `app,xenon`
    - `functionapp,linux,Kubernetes`
    - `app,functionapp`