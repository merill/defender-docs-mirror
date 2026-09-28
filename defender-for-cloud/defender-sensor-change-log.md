---
layout: Conceptual
title: Defender Sensor for Defender for Containers Changelog - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-sensor-change-log
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
description: Learn about the version history and updates for the Defender sensor in Microsoft Defender for Containers.
ms.topic: reference
ms.date: 2026-04-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 35a3a39d-1072-837b-be70-8349d88b285e
document_version_independent_id: 0ad25d86-ee58-1e52-93ce-abe06866d91e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-sensor-change-log.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-sensor-change-log
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-sensor-change-log.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 98e82ee6-a65f-0e14-34ab-06fc584820cd
---

# Defender Sensor for Defender for Containers Changelog - Microsoft Defender for Cloud | Microsoft Learn

The Sensor for Microsoft Defender for Containers release notes provides a detailed version history of sensor updates. Each version includes new features, improvements, and fixes to enhance functionality. Use this changelog to stay informed about the latest updates and plan your deployments accordingly.

For more information about deploying the sensor in Defender for Containers, see [Configure Microsoft Defender for Containers components](defender-for-containers-enable-plan).

To see the version of the sensor run:

`kubectl get -n kube-system daemonsets/microsoft-defender-collector-ds -o jsonpath='{.metadata.labels.app\.kubernetes\.io/version}'`

## Defender for Containers – Sensor Support Policy

The support policy here applies to all Helm-based and multicloud installations. For scenarios where the sensor is deployed as part of AKS, please refer to: [Supported Kubernetes versions in Azure Kubernetes Service (AKS) - Azure Kubernetes Service | Microsoft Learn](/en-us/azure/aks/supported-kubernetes-versions?tabs=azure-cli)

| Version | Preview Date | GA Date | End of support |
| --- | --- | --- | --- |
| 0.8 |  | Feb 2025 | Feb 2027 |
| 0.9 | July 2025 | Apr 2026 | Apr 2027 |
| 0.10 | Feb 2026 | Apr 2026 | Apr 2027 |
| 0.11 | Apr 2026 | Jul 2026 | Jul 2027 |

Each stable (GA) version is supported for 12 months from its GA release date. After the 12-month window ends, the version is no longer supported. Customers should upgrade to the latest stable or Public release to maintain support and access new capabilities.

## Sensor versions available per release

### Sensor v0.11 (deployed by Helm or Arc for K8s)

**Sensor v0.11.6 — GA**

- **Released:** August 2026
- **What's included:**

    - Security vulnerability fixes and dependency updates.

**Sensor v0.11.5 — GA**

- **Released:** August 2026
- **What's included:**

    - Improved pod inventory reliability by preventing failures when processing Kubernetes pod deletion events.
    - Updated runtime and telemetry dependencies to address security vulnerabilities.

**Sensor v0.11.4 — GA**

- **Released:** July 2026
- **What's included:**

    - General Availability of EKS/GKE Private clusters support. For the private clusters documentation page [Private clusters](defender-for-containers-private-clusters)

### Sensor v0.10 (deployed by Helm or Arc for K8s)

**Sensor v0.10.9 — GA**

- **Released:** August 2026
- **What's included:**

    - Security vulnerability fixes and dependency updates.

**Sensor v0.10.8 — GA**

- **Released:** August 2026
- **What's included:**

    - Improved pod inventory reliability by preventing failures when processing Kubernetes pod deletion events.
    - Updated runtime and networking dependencies to address security vulnerabilities.

**Sensor v0.10.6 — GA**

- **Released:** July 2026
- **What's included:**

    - Security fixes: including patching vulnerabilities in authentication, runtime components, and dependencies to address credential exposure risks
    - Performance improvement - Reduced process event filtering CPU usage
    - Improved authentication stability by using projected service account tokens (PSAT) with the correct audience for cloud token exchange

**Sensor v0.10.5 — GA**

- **Released:** May 2026
- **What's included:**

    - General Availability of runtime antimalware detection and blocking
    - General Availability of Bottlerocket OS support
    - Improved compatibility with Nexus Baremetal clusters
    - Upgraded Go and related dependencies to address security vulnerabilities and improve runtime stability

**Sensor v0.10.4 — Preview**

- **Released:** April 2026
- **What's included:**

    - Upgraded Go and related dependencies and libraries to address security vulnerabilities and improve runtime stability

**Sensor v0.10.3 — Preview**

- **Released:** March 2026
- **What's included:**

    - Added privileged security context for collectors on Nexus Baremetal
    - Security fix: sanitized secrets from storage client retry logs
    - Moved SELinux options to pod-level for improved collector compatibility
    - Updated antimalware collector
    - Security vulnerability fixes

**Sensor v0.10.2 – Preview**

- **Released:** February 2026
- **What's included:**

    - Defender for containers runtime antimalware. Learn more about [antimalware detection and blocking](anti-malware).
    - Binary drift blocking

### Sensor v0.9 (AKS 1.35 or by Helm)

**Sensor v0.9.66 — GA**

- **Released:** August 2026
- **What's included:**

    - Security vulnerability fixes and dependency updates.

**Sensor v0.9.65— GA**

- **Released:** August 2026
- **What's included:**

    - Improved pod inventory reliability by preventing failures when processing Kubernetes pod deletion events.
    - Updated runtime and networking dependencies to address security vulnerabilities.

**Sensor v0.9.62— GA**

- **Released:** July 2026
- **What's included:**

    - Security fixes: including patching vulnerabilities in authentication, runtime components, and dependencies to address credential exposure risks
    - Performance improvement - Reduced process event filtering CPU usage
    - Improved authentication stability by using projected service account tokens (PSAT) with the correct audience for cloud token exchange

**Sensor v0.9.58 — GA**

- **Released:** May 2026
- **What's included:**

    - General Availability of Bottlerocket OS support
    - Improved compatibility with Nexus Baremetal clusters
    - Upgraded Go and related dependencies to address security vulnerabilities and improve runtime stability

**Sensor v0.9.53 — Preview**

- **Released:** April 2026
- **What's included:**

    - Upgraded Go and related dependencies and libraries to address security vulnerabilities and improve runtime stability

**Sensor v0.9.52— Preview**

- **Released:** March 2026
- **What's included:**

    - Added privileged security context for collectors on Nexus Baremetal
    - Security fix: sanitized secrets from storage client retry logs
    - Moved SELinux options to pod-level for improved collector compatibility
    - Security vulnerability fixes

**Sensor v0.9.51 – Preview**

- **Released:** March 2026
- **What's included:**

    - Improvements

        - Security and platform updates

            - Upgraded Go and related dependencies and libraries to address security vulnerabilities and improve runtime stability.
            - Fluent Bit updated to a newer version to improve log processing and security.
            - FIPS support enabled for the publisher and file-cleaner components for customers requiring FIPS-compliant operation.
        - Reduced load and resource usage

            - Reduced aggregation size and narrowed aggregated data types to lower memory and CPU usage.
            - Chart and publisher updates to reduce query load on the authentication service, improving overall reliability.
    - Fixes

        - Authentication stability and concurrency

            - Token provider now caches negative (false) responses from the auth service to avoid repeated failing calls.
            - Improved thread-safety in the token provider by adding read-locking around token map checks to prevent race conditions.
        - Miscellaneous fixes

            - Various configuration and path fixes to ensure reliable log collection and prevent duplicate data.

**Sensor v0.9.50 – Preview**

- **Released:** February 2026
- **What's included:**

    - Performance improvements

**Sensor v0.9.49 – Preview**

- **Released:** December 2025
- **What's included:**

    - Bug fixes
    - Gating support for auto AKS

**Sensor v0.9.46 – Preview**

- **Released:** December 2025
- **What's included:**
    - Bug fixes and security enhancements
    - Convert log analytics keys in Defender helm chart to optional

**Sensor v0.9.44 – Preview**

- **Released:** November 2025
- **What's included:**
    - Bug fixes and security enhancements
    - Added support for new Defender endpoints (requires outbound access to `*.cloud-defender.microsoft.com`). Learn more in the [Defender for Containers setup guide](defender-for-containers-enable-plan).

**Sensor v0.9.17 – Preview**

- **Released:** June 2025
- **What's included:**
    - **Helm-based deployment support** Introduces a new method for deploying and managing the sensor using Helm. See: [Install Defender for Containers sensor using Helm](deploy-helm).
    - **DNS threat detections** Adds DNS-based detection capabilities using threat intelligence feeds.
    - Improved memory efficiency and reduced CPU consumption
    - Bug fixes and security enhancements

### Sensor v0.8 (AKS versions 1.34 and below)

**Sensor v0.8.59 — GA**

- **Released:** August 2026
- **What's included:**

    - Security vulnerability fixes and dependency updates.

**Sensor v0.8.55 — GA**

- **Released:** July 2026
- **What's included:**

    - Security fixes: including patching vulnerabilities in authentication, runtime components, and dependencies to address credential exposure risks
    - Performance improvement - Reduced process event filtering CPU usage
    - Improved authentication stability by using projected service account tokens (PSAT) with the correct audience for cloud token exchange

**Sensor v0.8.51 — GA**

- **Released:** May 2026
- **What's included:**

    - Improved compatibility with Nexus Baremetal clusters
    - Upgraded Go and related dependencies to address security vulnerabilities and improve runtime stability

**Sensor v0.8.50 — GA**

- **Released:** April 2026
- **What's included:**

    - Upgraded Go and related dependencies and libraries to address security vulnerabilities and improve runtime stability

**Sensor v0.8.49 — GA**

- **Released:** March 2026
- **What's included:**

    - Added privileged security context for collectors on Nexus Baremetal
    - Security fix: sanitized secrets from storage client retry logs
    - Security vulnerability fixes

**Sensor v0.8.48 – GA**

- **Released:** March 2026
- **What's included:**

    - Security

        - Dependency and image updates: Multiple components have updated binaries and container images to address known vulnerabilities.
        - Go runtime and component upgrades: The Go runtime and an internal IG component were upgraded to remediate security issues.
        - FIPS and image hardening for publisher components: Publisher and file-cleaner components now support FIPS configurations and use smaller, hardened base images; Fluent Bit was upgraded as part of this hardening.

**Sensor v0.8.47 – GA**

- **Released:** February 2026
- **What's included:**

    - Performance Improvements

**Sensor v0.8.42 – GA**

- **Released:** December 2025
- **What's included:**

    - Security enhancements
    - Gating support for auto AKS

**Sensor v0.8.40 – GA**

- **Released:** December 2025
- **What's included:**
    - Bug fixes and security enhancements
    - Improve latency for webhook calls in the API gating validation.

**Sensor v0.8.39 – GA**

- **Released:** November 2025
- **What's included:**
    - Bug fixes and security enhancements
    - Gated deployment: Now globally available
    - Added support for new Defender endpoints (requires outbound access to `*.cloud-defender.microsoft.com`). Learn more about network requirements in the [Defender for Containers setup guide](defender-for-containers-enable-plan).

**Sensor v0.8.30 – GA**

- **Released:** August 2025
- **What's included:**

    - Better memory efficiency and reduced CPU consumption
    - Bug fixes and security enhancements