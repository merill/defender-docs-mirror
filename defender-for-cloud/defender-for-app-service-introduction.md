---
layout: Conceptual
title: Microsoft Defender for App Service - Benefits and Features - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-app-service-introduction
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
description: Learn about the capabilities of Microsoft Defender for App Service and how to enable it on your subscription.
ms.date: 2026-05-14T00:00:00.0000000Z
ms.topic: overview
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: e5b1396b-0d4e-e597-31f5-4a4dcf8e1c9e
document_version_independent_id: d3fdd770-d88d-b0b5-cc4e-f05ba971188f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-app-service-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-app-service-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-app-service-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 382afdea-1c8c-15c1-dd2c-b0db2f2b674d
---

# Microsoft Defender for App Service - Benefits and Features - Microsoft Defender for Cloud | Microsoft Learn

## Prerequisites

Defender for Cloud is natively integrated with App Service, eliminating the need for deployment and onboarding - the integration is transparent.

To protect your Azure App Service plan with Microsoft Defender for App Service, you need:

- An App Service plan on any App Service tier.
- Defender for Cloud's enhanced protections enabled on your subscription as described in [Enable enhanced security features](connect-azure-subscription).

    Tip

    You can optionally enable individual Microsoft Defender plans, like Microsoft Defender for App Service.
- Microsoft Defender for App Service is billed as shown on the [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator). Billing is calculated according to the total compute instances across all App Service plan tiers.
- Check out Defender for App Service's [cloud availability](support-matrix-defender-for-cloud).

### App Service diagnostics for alert investigation

To investigate security alerts triggered by Microsoft Defender for App Service, enable diagnostic settings on your App Service resource. Diagnostic logs capture HTTP traffic, application events, and platform-level activity that provide critical evidence when analyzing suspicious behavior. Without these logs, the data available for incident investigation might be limited.

Important

Enabling diagnostic settings can incur additional storage costs based on log volume and the destination you choose, such as a Log Analytics workspace or a Storage Account.

## Benefits of Microsoft Defender for App Service?

Azure App Service is a fully managed platform for building and hosting your web apps and APIs. Since the platform is fully managed, you don't have to worry about the infrastructure. It provides management, monitoring, and operational insights to meet enterprise-grade performance, security, and compliance requirements. For more information, see [Azure App Service](https://azure.microsoft.com/services/app-service/).

**Microsoft Defender for App Service** uses the scale of the cloud to identify attacks targeting applications running over App Service. Attackers probe web applications to find and exploit weaknesses. Before being routed to specific environments, requests to applications running in Azure go through several gateways, where they're inspected and logged. This data is then used to identify exploits and attackers, and to learn new patterns that can be used later.

When you enable Microsoft Defender for App Service, you immediately benefit from the following services offered by this Defender plan:

- **Secure** - Defender for App Service assesses the resources covered by your App Service plan and generates security recommendations based on its findings. To harden your App Service resources, use the detailed instructions in these recommendations.
- **Detect** - Defender for App Service detects a multitude of threats to your App Service resources by monitoring:

    - the Virtual Machine (VM) instance in which your App Service is running, and its management interface
    - the requests and responses sent to and from your App Service apps
    - the underlying sandboxes and VMs
    - App Service internal logs - available thanks to the visibility that Azure has as a cloud provider

As a cloud-native solution, Defender for App Service can identify attack methodologies applying to multiple targets. For example, from a single host it would be difficult to identify a distributed attack from a small subset of IPs, crawling to similar endpoints on multiple hosts.

The log data and the infrastructure together can tell the story: from a new attack circulating in the wild to compromises in customer machines. Therefore, even if Microsoft Defender for App Service is deployed after a web app has been exploited, it might be able to detect ongoing attacks.

## What threats can Defender for App Service detect?

### Threats by MITRE ATT&CK tactics

Defender for Cloud monitors for many threats to your App Service resources. The alerts cover almost the complete list of MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) tactics from preattack to command and control.

- **Pre-attack threats** - Defender for Cloud can detect the execution of multiple types of vulnerability scanners that attackers frequently use to probe applications for weaknesses.
- **Initial access threats** - [Microsoft Defender Threat Intelligence](https://www.microsoft.com/security/business/siem-and-xdr/microsoft-defender-threat-intelligence/) powers these alerts that include triggering an alert when a known malicious IP address connects to your Azure App Service FTP interface.
- **Execution threats** - Defender for Cloud can detect attempts to run high privilege commands, Linux commands on a Windows App Service, fileless attack behavior, digital currency mining tools, and many other suspicious and malicious code execution activities.

### Dangling DNS detection

Defender for App Service also identifies any DNS entries remaining in your DNS registrar when an App Service website is decommissioned - these are known as dangling DNS entries. When you remove a website and don't remove its custom domain from your DNS registrar, the DNS entry is pointing to a nonexistent resource, and your subdomain is vulnerable to a takeover. Defender for Cloud doesn't scan your DNS registrar for *existing* dangling DNS entries; it alerts you when an App Service website is decommissioned and its custom domain (DNS entry) isn't deleted.

Subdomain takeovers are a common, high-severity threat for organizations. When a threat actor detects a dangling DNS entry, they create their own site at the destination address. The traffic intended for the organization’s domain is then directed to the threat actor's site, and they can use that traffic for a wide range of malicious activity.

Dangling DNS protection is available whether your domains are managed with Azure DNS or an external domain registrar and applies to App Service on both Windows and Linux.

[![An example of an alert about a discovered dangling DNS entry. Enable Microsoft Defender for App Service to receive this and other alerts for your environment.](media/defender-for-app-service-introduction/dangling-dns-alert.png)](media/defender-for-app-service-introduction/dangling-dns-alert.png#lightbox)

Learn more about dangling DNS and the threat of subdomain takeover, in [Prevent dangling DNS entries and avoid subdomain takeover](/en-us/azure/security/fundamentals/subdomain-takeover).

For a full list of the App Service alerts, see the [Reference table of alerts](alerts-azure-app-service).

Note

Defender for Cloud might not trigger dangling DNS alerts if your custom domain doesn't point directly to an App Service resource, or if Defender for Cloud hasn't monitored traffic to your website since the dangling DNS protection was enabled (because there won't be logs to help identify the custom domain).