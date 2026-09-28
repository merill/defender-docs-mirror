---
layout: Conceptual
title: Partner applications in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/partner-applications
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: View supported partner applications to enhance the detection, investigation, and threat intelligence capabilities of the platform
ms.service: defender-endpoint
ms.subservice: reference
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: article
ms.date: 2026-06-08T00:00:00.0000000Z
locale: en-us
document_id: e2307049-88c8-7b80-453f-cb8f7e45ef4f
document_version_independent_id: e2307049-88c8-7b80-453f-cb8f7e45ef4f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/partner-applications.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: partner-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/partner-applications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 37600383-2ce6-3384-d083-27399f0bcd7f
---

# Partner applications in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Defender for Endpoint supports third-party applications to help enhance the detection, investigation, and threat intelligence capabilities of the platform.

The support for third-party solutions helps to further streamline, integrate, and orchestrate defenses from other vendors with Microsoft Defender for Endpoint; enabling security teams to effectively respond better to modern threats.

Microsoft Defender for Endpoint seamlessly integrates with existing security solutions. The integration provides integration with the following solutions such as:

- SIEM
- Ticketing and IT service management solutions
- IoC indicators ingestions and matching
- Automated device investigation and remediation based on external alerts
- Integration with Security orchestration and automation response (SOAR) systems
- Support for non-Windows platforms

To find the complete list of supported partner applications and integrations, see the [Microsoft Marketplace](https://marketplace.microsoft.com).

## SIEM integration

Defender for Endpoint supports SIEM integration through various of methods. This can include specialized SIEM system interface with out of the box connectors, a generic alert API enabling custom implementations, and an action API enabling alert status management.

## Ticketing and IT service management

Ticketing solution integration helps to implement manual and automatic response processes. Defender for Endpoint can help to create tickets automatically when an alert is generated and resolve the alerts when tickets are closed using the alerts API.

## Indicators matching

You can use threat-intelligence from providers and aggregators to maintain and use indicators of compromise (IOCs).

Defender for Endpoint allows you to integrate with these solutions and act on IoCs by correlating rich telemetry to create alerts. You can also use prevention and automated response capabilities to block execution and take remediation actions when there's a match.

Defender for Endpoint supports IOC matching and remediation for file and network indicators. Blocking is supported for file indicators.

## External alert correlation and Automated investigation and remediation

Defender for Endpoint offers unique automated investigation and remediation capabilities to drive incident response at scale.

Integrating the automated investigation and response capability with other solutions such as IDS and firewalls help to address alerts and minimize the complexities surrounding network and device signal correlation, effectively streamlining the investigation and threat remediation actions on devices.

External alerts can be pushed to Defender for Endpoint. These alerts are shown side by side with additional device-based alerts from Defender for Endpoint. This view provides a full context of the alert and can reveal the full story of an attack.

## Security orchestration and automation response (SOAR) integration

Orchestration solutions can help build playbooks and integrate the rich data model and actions that Defender for Endpoint APIs exposes to orchestrate responses, such as query for device data, trigger device isolation, block/allow, resolve alert and others.

## Support for non-Windows platforms

Defender for Endpoint provides a centralized security operations experience for Windows and non-Windows platforms, including mobile devices. You'll be able to see alerts from various supported operating systems (OS) in the portal and better protect your organization's network.