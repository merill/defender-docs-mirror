---
layout: Conceptual
title: Determine Ownership Requirements for Multicloud Security Planning - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-multicloud-security-determine-ownership-requirements
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
description: Learn about determining ownership requirements when planning multicloud deployment with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 1be11b67-4ae1-ff38-cd77-dfe6407ab3ee
document_version_independent_id: fb9d3259-1c78-8626-8dae-9791992716f2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-multicloud-security-determine-ownership-requirements.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-multicloud-security-determine-ownership-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-multicloud-security-determine-ownership-requirements.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: a35b671a-4528-0649-a330-b637fdf69d92
---

# Determine Ownership Requirements for Multicloud Security Planning - Microsoft Defender for Cloud | Microsoft Learn

## Identify teams and ownership for multicloud security

When you deploy a multicloud security solution with Microsoft Defender for Cloud, you need to determine which teams own specific security functions. This article helps you plan ownership requirements as you design a cloud security posture management (CSPM) and cloud workload protection platform (CWPP) solution for multicloud resources. It helps you identify the security teams involved in your multicloud environment, define their functions and responsibilities, align teams on ownership for security decision making, and choose between centralized and decentralized operating models.

## Ownership planning goals

Identify the teams involved in your multicloud security solution, and plan how they align and work together.

## Define security functions and responsibilities

Depending on the size of your organization, separate teams might manage [security functions](/en-us/azure/cloud-adoption-framework/organize/cloud-security-compliance-management). In a complex enterprise, functions might be numerous. For more information, see [Security teams, roles, and functions](/en-us/azure/cloud-adoption-framework/secure/teams-roles).

| Security function | Details |
| --- | --- |
| Security Operations (SecOps) | Reducing organizational risk by reducing the time in which bad actors have access to corporate resources. Reactive detection, analysis, response, and remediation of attacks. Proactive threat hunting. |
| Security architecture | Security design summarizing and documenting the components, tools, processes, teams, and technologies that protect your business from risk. |
| Security compliance management | Processes that ensure the organization is compliant with regulatory requirements and internal policies. |
| People security | Protecting the organization from human risk to security. |
| Application security and DevSecOps | Integrating security into DevOps processes and apps. |
| Data security | Protecting your organizational data. |
| Infrastructure and endpoint security | Providing protection, detection, and response for infrastructure, networks, and endpoint devices used by apps and users. |
| Identity and key management | Authenticating and authorizing users, services, devices, and apps. Provide secure distribution and access for cryptographic operations. |
| Threat intelligence | Making decisions and acting on security threat intelligence that provides context and actionable insights on active attacks and potential threats. |
| Posture management | Continuously reporting on, and improving, your organizational security posture. |
| Incident preparation | Building tools, processes, and expertise to respond to security incidents. |

## Align teams on ownership responsibilities

If different teams manage cloud security, it's critical that they work together and know who's responsible for decision making in the multicloud environment. Lack of ownership creates friction that can result in stalled projects and insecure deployments that couldn't wait for security approval.

Security leadership, most commonly under the CISO, should specify who's accountable for security decision making. Typically, responsibilities align as summarized in the following table.

| Category | Description | Typical Team |
| --- | --- | --- |
| Server endpoint security | Monitor and remediate server security, includes patching, configuration, endpoint security, and similar tasks. | Joint responsibility of [central IT operations](/en-us/azure/cloud-adoption-framework/organize/central-it) and [Infrastructure and endpoint security](/en-us/azure/cloud-adoption-framework/organize/central-it) teams. |
| Incident monitoring and response | Investigate and remediate security incidents in your organization's SIEM or source console. | [Security operations](/en-us/azure/cloud-adoption-framework/organize/cloud-security-operations-center) team. |
| Policy management | Set direction for Azure role-based access control (Azure RBAC), Microsoft Defender for Cloud, administrator protection strategy, and Azure Policy to govern Azure resources and custom AWS/GCP recommendations. | Joint responsibility of [policy and standards](/en-us/azure/cloud-adoption-framework/organize/cloud-security-policy-standards) and [security architecture](/en-us/azure/cloud-adoption-framework/organize/cloud-security-architecture) teams. |
| Threat and vulnerability management | Maintain complete visibility and control of the infrastructure, to ensure that critical issues are discovered and remediated as efficiently as possible. | Joint responsibility of [central IT operations](/en-us/azure/cloud-adoption-framework/organize/central-it) and [Infrastructure and endpoint security](/en-us/azure/cloud-adoption-framework/organize/central-it) teams. |
| Application workloads | Focus on security controls for specific workloads. The goal is to integrate security assurances into development processes and custom line of business (LOB) applications. | Joint responsibility of [application development](/en-us/azure/cloud-adoption-framework/organize/cloud-security-application-security-devsecops) and [central IT operations](/en-us/azure/cloud-adoption-framework/organize/central-it) teams. |
| Identity security and standards | Understand Permission Creep Index (PCI) for Azure subscriptions, AWS accounts, and GCP projects, in order to identify risks associated with unused or excessive permissions for identities and resources. | Joint responsibility of [identity and key management](/en-us/azure/cloud-adoption-framework/organize/cloud-security-identity-keys), [policy and standards](/en-us/azure/cloud-adoption-framework/organize/cloud-security-policy-standards), and [security architecture](/en-us/azure/cloud-adoption-framework/organize/cloud-security-architecture) teams. |

## Best practices for assigning ownership

Consider the following best practices when assigning ownership and aligning teams in a multicloud security model:

- Although you might divide multicloud security for different areas of the business, have teams manage security for the entire multicloud estate. This approach is better than having different teams secure different cloud environments. For example, one team manages Azure and another team manages AWS. Teams working in multicloud environments help prevent sprawl within the organization. They also help ensure that security policies and compliance requirements are applied in every environment.
- Often, teams that manage Defender for Cloud don't have privileges to remediate recommendations in workloads. For example, the Defender for Cloud team might not be able to remediate vulnerabilities in an AWS EC2 instance. The security team might be responsible for improving the security posture, but unable to fix the resulting security recommendations. To address the gap between security posture responsibility and remediation authority:

    - Involve the AWS workload owners. [Assigning owners with due dates](governance-rules) and [defining governance rules](governance-rules) creates accountability and transparency as you drive processes to improve security posture.
- Depending on organizational models, you might commonly see these options for central security teams operating with workload owners:

    - **Option 1: Centralized model.** A central team defines, deploys, and monitors security controls.

        - The central security team decides which security policies to implement in the organization and who has permissions to control the set policy.
        - The team might also have the power to remediate non-compliant resources and enforce resource isolation in case of a security threat or configuration issue.
        - Workload owners are responsible for managing their cloud workloads but need to follow the security policies that the central team deploys.
        - This model is most suitable for companies with a high level of automation, to ensure automated response processes to vulnerabilities and threats.
    - **Option 2: Decentralized model.** Workload owners define, deploy, and monitor security controls.

        - Workload owners deploy security controls because they own the policy set and can decide which security policies are applicable to their resources.
        - Owners need to be aware of, understand, and act upon security alerts and recommendations for their own resources.
        - The central security team acts as a controlling entity, without write-access to any of the workloads.
        - The security team usually has insights into the overall security posture of the organization, and they might hold the workload owners accountable for improving their security posture.
        - This model is most suitable for organizations that need visibility into their overall security posture but at the same time want to keep responsibility for security with the workload owners.
        - Currently, the only way to achieve Option 2 in Defender for Cloud is to assign the workload owners with Security Reader permissions to the subscription that's hosting the multicloud connector resource.