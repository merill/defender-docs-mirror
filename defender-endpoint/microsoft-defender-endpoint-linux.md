---
layout: Conceptual
title: Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint-linux
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: gopkr, pahuijbr, megphapriya
description: Learn how Microsoft Defender for Endpoint on Linux protects servers with next-gen antivirus, EDR, and vulnerability management.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: article
ms.subservice: linux
search.appverid: met150
ai-usage: ai-assisted
ms.date: 2026-05-18T00:00:00.0000000Z
locale: en-us
document_id: f1cddfc6-07af-eccb-f191-ca50b2c31976
document_version_independent_id: f1cddfc6-07af-eccb-f191-ca50b2c31976
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-endpoint-linux.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-endpoint-linux
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-endpoint-linux.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 72a9eeb9-4920-4146-155f-6761abad9b23
---

# Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint on Linux protects Linux server workloads in on-premises, cloud, and hybrid environments. It helps you prevent, detect, investigate, and respond to advanced threats with unified visibility through the Microsoft Defender portal.

Defender uses a lightweight [eBPF-based](linux-support-ebpf) sensor architecture without kernel modules, providing protection with minimal overhead and zero workload disruption on resource-constrained systems.

As Linux threats evolve beyond traditional malware into fileless and in-memory attacks, Defender combines [next-generation antivirus protection](next-generation-protection), AI-driven [endpoint detection and response](overview-endpoint-detection-response) (EDR), behavioral analytics, and Microsoft Threat Intelligence to detect and disrupt attacker techniques. These techniques include ransomware, memory injection, lateral movement, and advanced persistence threats.

With broad Linux distribution support and deep integration with the Microsoft Defender ecosystem, you can standardize security operations, gain end-to-end visibility, and accelerate threat response through a unified platform.

## Security capabilities for Linux server environments

The following table describes the core security capabilities offered by Microsoft Defender for Endpoint on Linux.

| Capability | Description |
| --- | --- |
| **Next-generation protection** | Provides real-time prevention against malware and emerging threats by analyzing execution patterns and blocking malicious activity. |
| **Endpoint detection and response (EDR)** | Delivers deep visibility into endpoint activity and enables rapid investigation and response to advanced attacks. |
| **[Vulnerability management](/en-us/defender-vulnerability-management/defender-vulnerability-management)** | Identifies security gaps and prioritizes remediation actions to continuously reduce risk exposure. |
| **Streamlined management and operations** | Simplifies onboarding, configuration, monitoring, and management of Defender in large Linux environments. |
| **Seamless integration and extensibility** | Extends visibility and response through seamless connectivity with security tools, APIs, and the broader Defender platform. |

### Next-generation protection

Protect Linux endpoints from malware and advanced threats using real-time, behavior-based, and cloud-powered protection capabilities.

| Capability | Description |
| --- | --- |
| **Real-time protection** | Antivirus and antimalware protection using behavior-based, cloud-delivered, and machine-learning techniques. |
| **Behavioral monitoring** | Monitors process behavior in real time to detect and block malicious activity based on execution patterns and intent. |
| **Passive mode** | Provides antivirus protection in a passive state without automatic remediation while preserving full EDR visibility. Allows coexistence with other third-party antivirus solutions. |
| **Cloud-delivered protection** | Uses machine learning and threat intelligence to detect emerging threats quickly. |
| **[Scheduled and on-demand scans](schedule-anti-virus-scans-linux)** | Provides flexibility to perform quick, full, or custom scans on endpoints based on operational requirements. |

### Endpoint detection and response (EDR)

Detect, investigate, and respond to sophisticated attacks powered by AI-driven analytics, behavioral detections, and Microsoft Threat Intelligence.

| Feature | Description |
| --- | --- |
| **Behavior-based detections** | Detects advanced threats using AI-driven behavioral analytics. |
| **MITRE ATT&CK-aligned detections** | Maps detections to attacker techniques for better investigation. |
| **Alert correlation** | Groups related alerts into incidents for streamlined investigation. |
| **Device timeline** | Provides a detailed view of activity on the endpoint. |
| **[Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview)** | Enables proactive threat hunting using query-based analysis. |
| **[Live Response](live-response)** | Allows remote investigation, script execution, and remediation such as file deletion, process termination, and evidence collection. |
| **Block file using file indicators** | Blocks or allows files on endpoints using custom indicators, helping prevent known malicious files from execution. |
| **[Device isolation](respond-machine-alerts)** | Helps contain compromised devices from lateral movement. |
| **Investigation package collection** | Collects forensic data for deeper analysis. |
| **Remote scanning** | Initiates antivirus scans to identify and remediate threats. |

### Vulnerability management

Continuously assess vulnerabilities, misconfigurations, and security posture to reduce risk exposure and prioritize remediation.

| Capability | Description |
| --- | --- |
| **Vulnerability assessment** | Identifies software vulnerabilities and misconfigurations on devices. |
| **[Security recommendations](/en-us/defender-vulnerability-management/tvm-security-recommendation)** | Provides actionable guidance to reduce endpoint risk. |
| **[Remediation tracking](/en-us/defender-vulnerability-management/tvm-remediation)** | Tracks remediation activities and exposure reduction. |
| **Secure Score integration** | Assesses security posture and provides actions to improve overall security. |

## Streamlined management and operations

Microsoft Defender for Endpoint on Linux provides flexible onboarding and centralized management capabilities via the Defender portal designed to simplify deployment, configuration, monitoring, and integration with other security tools in Linux server environments.

### Deployment at scale

Microsoft Defender for Endpoint on Linux supports multiple deployment methods, enabling efficient onboarding and management in large, diverse environments.

| Capability | Description |
| --- | --- |
| **Script-based deployment** | Use the Defender Deployment Tool from the Defender portal to simplify installation and onboarding via a single script. |
| **Defender for Cloud deployment** | Automatically onboard and manage Linux servers through Defender for Cloud for streamlined cloud and hybrid deployments. |
| **Third-party management tools** | Use tools such as Ansible, Chef, and Puppet for automated, at-scale deployments. |
| **Golden image deployment** | Pre-configure Defender in base images for consistent, repeatable deployment. |
| **Manual deployment** | Install Defender manually using CLI for testing or limited-scale scenarios. |

Defender supports enterprise-grade Linux distributions on both x64 and ARM64 architectures, enabling consistent protection in heterogeneous environments. For the support matrix and deployment guidance, see [Prerequisites for Defender for Endpoint on Linux](mde-linux-prerequisites).

### Management at scale

Centralized management capabilities via the Defender portal help organizations consistently configure, maintain, and monitor Linux server environments at scale while reducing operational overhead.

| Capability | Description |
| --- | --- |
| **[Security settings configuration](/en-us/defender-endpoint/linux-preferences)** | Centrally manage antivirus settings via the [Defender](linux-preferences) or [Intune](/en-us/intune/device-security/microsoft-defender/security-settings-management) portal and enforce consistent configurations in Linux environments, including [exclusions](linux-exclusions). |
| **Software updates** | **[Platform updates](linux-updates)** - Monthly updates provide security enhancements and new features. Each release expires after nine months; staying within the latest three versions is recommended. **Automatic security intelligence updates** - Keeps protection up to date with the latest threat intelligence and security definitions. **Offline security intelligence updates** - Supports updating security intelligence in environments without internet connectivity. |
| **Device health monitoring** | Provides visibility into antivirus posture, scan results, platform, engine, and intelligence versions via the portal and APIs. |

## Seamless integration and extensibility

Microsoft Defender integrates with existing security tools and workflows through cloud-level capabilities that apply to all onboarded platforms. It enables integration via [APIs](api/apis-intro), [Power BI](api/api-power-bi), and SIEM/SOAR solutions for centralized monitoring and automated response, while extending into Microsoft Defender XDR and third-party ecosystems to deliver unified visibility and coordinated security operations.

| Capability | Description |
| --- | --- |
| **[Management and automation APIs](api/management-apis)** | Automate workflows and integrate Defender for Endpoint into your existing processes. |
| **[Partner integrations](/en-us/defender-endpoint/partner-integration)** | Integrate with Microsoft and non-Microsoft security solutions. |

## What's new in the latest release

To learn about what's new in Endpoint security, see the latest updates in [What's new in Microsoft Defender for Endpoint](/en-us/defender-endpoint/whats-new-in-microsoft-defender-endpoint).

Microsoft includes security fixes in monthly releases. However, the release notes don’t always list these fixes under a separate Security patch section. For more information, see [What's new in Microsoft Defender for Endpoint on Linux](/en-us/defender-endpoint/microsoft-defender-endpoint-releases#linux-releases).