---
layout: Conceptual
title: Behavioral blocking and containment - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/behavioral-blocking-containment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Explore behavioral blocking and containment capabilities in Microsoft Defender for Endpoint that identify and stop threats based on behaviors and process trees.
author: limwainstein
ms.author: lwainstein
ms.reviewer: shwetaj
ms.topic: concept-article
ms.service: defender-endpoint
ms.subservice: edr
ms.localizationpriority: medium
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1012
ms.collection:
- m365-security
- tier2
ms.date: 2026-05-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5447816f-bab1-75cc-5669-ca3edc04806a
document_version_independent_id: 5447816f-bab1-75cc-5669-ca3edc04806a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/behavioral-blocking-containment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: behavioral-blocking-containment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/behavioral-blocking-containment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b4fe7e0c-7f84-eada-db5b-eec0055931da
---

# Behavioral blocking and containment - Microsoft Defender for Endpoint | Microsoft Learn

## What is behavioral blocking and containment?

Today's threat landscape is overrun by [fileless malware](malware/fileless-threats) that lives off the land, highly polymorphic threats that mutate faster than traditional solutions can keep up with, and human-operated attacks that adapt to what adversaries find on compromised devices. Traditional security solutions aren't sufficient to stop such attacks; you need artificial intelligence (AI) and machine learning (ML) backed capabilities, such as behavioral blocking and containment, included in [Defender for Endpoint](/en-us/windows/security).

Behavioral blocking and containment capabilities can help identify and stop threats based on their behaviors and process trees, even when the threat has already started. Next-generation protection, EDR, and Defender for Endpoint components and features work together in behavioral blocking and containment capabilities.

Behavioral blocking and containment capabilities work with multiple components and features of Defender for Endpoint to stop attacks immediately and prevent attacks from progressing.

- [Next-generation protection](microsoft-defender-antivirus-windows) (which includes Microsoft Defender Antivirus) can detect threats by analyzing behaviors, and stop running threats.
- [Endpoint detection and response](overview-endpoint-detection-response) (EDR) receives security signals across your network, devices, and kernel behavior. As threats are detected, alerts are created. Multiple alerts of the same type are aggregated into incidents, which makes it easier for your security operations team to investigate and respond.
- [Defender for Endpoint](overview-endpoint-detection-response) has a wide range of optics across identities, email, data, and apps, in addition to the network, endpoint, and kernel behavior signals received through EDR. A component of [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender), Defender for Endpoint processes and correlates these signals, raises detection alerts, and connects related alerts in incidents.

With these capabilities, more threats can be prevented or blocked, even if they start running. Whenever suspicious behavior is detected, the threat is contained, alerts are created, and threats are stopped in their tracks.

The following image shows an example of behavioral blocking and containment capabilities triggering an alert:

[![Screenshot of the Alerts page showing an alert triggered by behavioral blocking and containment.](media/blocked-behav-alert.png)](media/blocked-behav-alert.png#lightbox)

## Prerequisites

### Supported operating systems

- Windows

## Components of behavioral blocking and containment

- **On-client, policy-driven [attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview)** Prevent predefined, common attack behavior from apps. To monitor ASR rule detections, see [Monitor attack surface reduction (ASR) rule activity](attack-surface-reduction-rules-monitor).
- **[Client behavioral blocking](client-behavioral-blocking)** Threats on endpoints are detected through machine learning, and then are blocked and remediated automatically. (Client behavioral blocking is enabled by default.)
- **[Feedback-loop blocking](feedback-loop-blocking)** (also referred to as rapid protection) Threat detections are observed through behavioral intelligence. Threats are stopped and prevented from running on other endpoints. (Feedback-loop blocking is enabled by default.)
- **[Endpoint detection and response (EDR) in block mode](edr-in-block-mode)** Malicious artifacts or behaviors that are observed through post-breach protection are blocked and contained. EDR in block mode works even if Microsoft Defender Antivirus isn't the primary antivirus solution. (EDR in block mode isn't enabled by default; you turn it on in the Defender portal.)

Expect more to come in the area of behavioral blocking and containment, as Microsoft continues to improve threat protection features and capabilities. To see what's planned and rolling out now, visit the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?filters=Microsoft%20365).

## Examples of behavioral blocking and containment in action

Behavioral blocking and containment capabilities have blocked the following attacker techniques:

- Credential dumping from LSASS
- Cross-process injection
- Process hollowing
- User Account Control bypass
- Tampering with antivirus (such as disabling it or adding the malware as exclusion)
- Contacting Command and Control (C&C) to download payloads
- Coin mining
- Boot record modification
- Pass-the-hash attacks
- Installation of root certificate
- Exploitation attempt for various vulnerabilities

The following are two real-life examples of behavioral blocking and containment in action.

### Example 1: Credential theft attack against 100 organizations

As described in [In hot pursuit of elusive threats: AI-driven behavior-based blocking stops attacks in their tracks](https://www.microsoft.com/security/blog/2019/10/08/in-hot-pursuit-of-elusive-threats-ai-driven-behavior-based-blocking-stops-attacks-in-their-tracks), behavioral blocking and containment capabilities stopped a credential theft attack against 100 organizations around the world. Spear-phishing email messages that contained a lure document were sent to the targeted organizations. If a recipient opened the attachment, a related remote document was able to execute code on the user's device and load Lokibot malware, which stole credentials, exfiltrated stolen data, and waited for further instructions from a command-and-control server.

Behavior-based machine-learning models in Defender for Endpoint caught and stopped the attacker's techniques at two points in the attack chain:

- The first protection layer detected the exploit behavior. Machine-learning classifiers in the cloud correctly identified the threat and immediately instructed the client device to block the attack.
- The second protection layer, which helped stop cases where the attack got past the first layer, detected process hollowing, stopped that process, and removed the corresponding files (such as Lokibot).

While the attack was detected and stopped, alerts, such as an "initial access alert," were triggered and appeared in the [Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender).

[![Screenshot of the initial access alert in the Microsoft Defender portal.](media/behavblockcontain-initialaccessalert.png)](media/behavblockcontain-initialaccessalert.png#lightbox)

This example shows how behavior-based machine-learning models in the cloud add new layers of protection against attacks, even after they're already running.

### Example 2: NTLM relay - Juicy Potato malware variant

As described in the recent blog post, [Behavioral blocking, and containment: Transforming optics into protection](https://www.microsoft.com/security/blog/2020/03/09/behavioral-blocking-and-containment-transforming-optics-into-protection), in January 2020, Defender for Endpoint detected a privilege escalation activity on a device in an organization. An alert called "Possible privilege escalation using NTLM relay" was triggered.

[![An NTLM alert for Juicy Potato malware](media/ntlmalertjuicypotato.png)](media/ntlmalertjuicypotato.png#lightbox)

The threat turned out to be malware; it was a new, not-seen-before variant of a notorious hacking tool called Juicy Potato, which is used by attackers to get privilege escalation on a device.

Minutes after the alert was triggered, the file was analyzed, and confirmed to be malicious. Its process was stopped and blocked, as shown in the following image:

[![Screenshot of a blocked artifact notification showing the malicious process was stopped.](media/artifactblockedjuicypotato.png)](media/artifactblockedjuicypotato.png#lightbox)

A few minutes after the artifact was blocked, multiple instances of the same file were blocked on the same device, preventing more attackers or other malware from deploying on the device.

This example shows that with behavioral blocking and containment capabilities, threats are detected, contained, and blocked automatically.

Tip

If you're looking for Antivirus related information for other platforms, see the following articles:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)