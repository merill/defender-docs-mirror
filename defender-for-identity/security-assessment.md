---
layout: Conceptual
title: Microsoft Defender for Identity Security Posture Assessments - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/security-assessment
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how Microsoft Defender for Identity security posture assessments identify misconfigurations and legacy components in Active Directory and provide recommended remediation actions.
ms.date: 2026-08-07T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: LiorShapiraa
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 2f3660ea-e5e4-5bbb-3862-6a46ee4ada56
document_version_independent_id: 2f3660ea-e5e4-5bbb-3862-6a46ee4ada56
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/security-assessment.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-assessment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/security-assessment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 82933fdf-dd0c-5fde-ba50-045f5e385373
---

# Microsoft Defender for Identity Security Posture Assessments - Microsoft Defender for Identity | Microsoft Learn

Typically, organizations of all sizes have limited visibility into whether or not their on-premise and cloud apps and services could introduce a security vulnerability to their organization. The problem of limited visibility is especially true regarding use of unsupported or outdated components.

While your company might invest significant time and effort on hardening identities and identity infrastructure (such as Active Directory, Active Directory Connect) as an ongoing project, it's easy to remain unaware of common misconfigurations and use of legacy components that represent one of the greatest threat risks to your organization.

Microsoft security research reveals that most identity attacks utilize common misconfigurations in Active Directory and continued use of legacy components (such as NTLMv1 protocol) to compromise identities and successfully breach your organization. To combat these misconfigurations and legacy-component risks effectively, Microsoft Defender for Identity now offers proactive identity security posture assessments to detect and recommend actions across your on-premise Active Directory configurations.

## What do Defender for Identity security assessments provide?

Defender for Identity security posture assessments are available in [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score), and provide:

- **Detections and contextual data** on known exploitable components and misconfigurations, along with relevant paths for remediation.
- **Active monitoring for your on-premise and cloud identities and identity infrastructure**, watching for weak spots with the existing Defender for Identity sensor.
- **Accurate assessment reports** of your current organization security posture, for quick responses and effect monitoring in a continuous cycle.

Microsoft Secure Score is a measurement of an organization's security posture, with a higher number indicating more recommended actions taken. It can be found at https://security.microsoft.com/securescore in the [Microsoft Defender portal](/en-us/microsoft-365/security/defender/microsoft-365-defender).

### Categorization of Defender for Identity security posture assessments

Defender for Identity security posture assessments have six key categories. Each category addresses specific identity security risks and provides remediation guidance.

- **Hybrid security**: Identifies misconfigurations in environments that integrate on-premises (e.g., Active Directory) and cloud-based identity providers (e.g., Microsoft Entra ID, Okta). Assesses risks related to synchronization, authentication, and authorization across platforms.
- **Identity infrastructure**: Detects misconfigurations and vulnerabilities in core identity components, including domain controllers.
- **Certificates**: Assesses Active Directory Certificate Services (AD CS), Microsoft's certificate infrastructure service, for security gaps, such as misconfigured certificate templates or weak certificate authority settings. Identifying and addressing these issues helps prevent unauthorized access that could arise from certificate-related vulnerabilities.
- **Group policy**: Analyzes Group Policy configurations to identify settings that might allow privilege escalation or unauthorized lateral movement within the network. Ensuring secure Group Policy settings helps maintain proper access controls and system configurations.
- **Accounts**: Reviews users, devices, and groups to pinpoint security risks such as weak passwords, inactive accounts, or improper permissions.
- **Cloud identities**: Evaluates cloud identity configurations in Okta accounts for security gaps, such as missing MFA settings or privileged Okta accounts, and provides remediation guidance.

## Prerequisites

- You must have a Defender for Identity license to view Defender for Identity security posture assessments in Microsoft Secure Score.
- While *certificate template* assessments are available to all customers with AD CS installed in their environment, *certificate authority* assessments are available only to customers who have installed a sensor on an AD CS server.
- Hybrid security recommendations will be available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services.

For more information, see [Configuring sensors for AD FS, AD CS and Microsoft Entra Connect.](https://aka.ms/DeployMdiSensorOnYourIdentityInfrastructure)

## Access Defender for Identity security posture assessments

You can view Defender for Identity security posture assessments in the Microsoft Secure Score dashboard in the Microsoft Defender portal.

To access identity security posture assessments:

1. Open the [Microsoft Secure Score dashboard](https://security.microsoft.com/securescore).
2. Select the **Recommended actions** tab. You can search for a particular recommended action, or filter the results (for example, by the category **Identity**).

    [![Screenshot of the Recommended actions tab in Microsoft Secure Score showing identity security posture assessments.](media/recommended-actions.png)](media/recommended-actions.png#lightbox)
3. For more details, select the assessment.

    [![Screenshot of the assessments list with a specific security posture assessment selected for detailed view.](media/select-assessment.png)](media/select-assessment.png#lightbox)

Note

While assessments are updated in near real time, scores and statuses are updated every 24 hours. While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status may still take time until it's marked as **Completed**.