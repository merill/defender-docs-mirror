---
layout: Conceptual
title: Cloud infrastructure entitlement management (CIEM) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/permissions-management
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
description: Learn about CIEM in Microsoft Defender for Cloud and enhance the security of your cloud infrastructure.
ms.topic: concept-article
ms.date: 2025-07-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 64cc0cf0-3052-d55b-d50c-7d3020215f45
document_version_independent_id: 613d7cdf-926a-f096-6c42-5a1500b96ba8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/permissions-management.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/permissions-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/permissions-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: a3305f0d-2056-57a9-250f-acd83bd5e9f0
---

# Cloud infrastructure entitlement management (CIEM) - Microsoft Defender for Cloud | Microsoft Learn

Note

The deprecation of Microsoft Entra Permissions Management doesn't affect any existing CIEM capabilities in Microsoft Defender for Cloud. Learn more about [the future of CIEM in Microsoft Defender for Cloud](https://aka.ms/mdc-ciem).

Microsoft Defender for Cloud includes native cloud infrastructure Entitlement Management (CIEM) capabilities within the Defender [Cloud Security Posture Management (CSPM)](concept-cloud-security-posture-management) plan to help organizations discover, assess, and manage identity and access risks across their multicloud environments. These capabilities are designed to secure infrastructure by enforcing the principle of least privilege (PoLP), reducing the attack surface, and preventing the misuse of human and non-human identities across Azure, AWS, and GCP.

## How Defender for Cloud analyzes permissions

Defender for Cloud continuously analyzes identity configurations and usage patterns to identify excessive, unused, or misconfigured permissions. It assesses human and application identities, including users, service principals, groups, managed identities, and service accounts, and provides recommendations to reduce the risk of privilege misuse.

CIEM capabilities in Defender for Cloud support:

- Microsoft Entra ID users, groups, and service principals
- AWS IAM users, roles, and groups
- Google Cloud IAM users, groups, and service accounts

## Key capabilities

### Multicloud identity discovery

Track and analyze permissions across Azure, AWS, and GCP in a single, unified view. Identify which users, groups, service principals, or AWS roles have access to cloud resources and how those permissions are used.

### Effective permission analysis

Understand not just who has access, but the potential risk of what they can access. Defender for Cloud evaluates effective permissions to identify identities that can reach sensitive or business-critical resources. Use **Cloud Security Explorer** to search for specific identities or critical resources (for example, containing sensitive data, exposed to the internet) and determine who has access, what level of access they have, and how that access could be exploited.

### Identity risk insights

Reduce identity-related risk by receiving proactive guidance via recommendations. Defender for Cloud surfaces recommendations such as:

- Removing inactive, guest, or blocked accounts with access
- Limiting administrative privileges to a defined set of users
- Right-sizing permissions for overprovisioned identities based on actual usage
- Enforcing MFA and strong password policies for IAM users

### Lateral movement detections

Defender for Cloud correlates identity risks with attack path analysis, surfacing lateral movement opportunities that originate from overprivileged identities or misconfigurations. For example, an attacker could compromise a service principal with excessive rights to move laterally from a compromised resource to a sensitive database. This context allows security teams to prioritize high-impact identity issues that might otherwise go unnoticed.

## How to view identity and permission risks

Defender for Cloud provides several ways to monitor and address access risk:

- [Cloud Security Explorer](/en-us/azure/defender-for-cloud/how-to-manage-cloud-security-explorer): The Security Explorer allows you to query all identities in your environment with access to resources. These queries allow you to get a complete mapping of all your cloud entitlements with contextual information for the resources that the identities have permissions to.
- [Attack Path Analysis](/en-us/azure/defender-for-cloud/how-to-manage-attack-path): The Attack Path Analysis page lets you view attack paths that an attacker could take to reach a specific resource. With Attack Path Analysis, you can view a visual representation of the attack path and see which resources are exposed to the internet. Internet exposure often serves as an entry point for attack paths, especially when the resource has vulnerabilities. Internet-exposed resources often lead to targets with sensitive data.
- [Recommendations](recommendations-reference-identity-access): Defender for Cloud provides risk-based recommendations for various CIEM misconfigurations. The built-in recommendations provide guidance for remediating inactive identities, overprovisioned permissions, and insecure identity settings.
- [CIEM Workbook](/en-us/azure/defender-for-cloud/custom-dashboards-azure-workbooks): The CIEM workbook provides a customizable visual report of your cloud identity security posture. You can use this workbook to view insights about your identities, unhealthy recommendations, and attack paths.