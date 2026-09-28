---
layout: Conceptual
title: Advanced technologies at the core of Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/adv-tech-of-mdav
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender Antivirus engines and advanced technologies
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: overview
ms.date: 2025-01-24T00:00:00.0000000Z
ms.subservice: ngp
ms.localizationpriority: medium
ms.custom: partner-contribution
locale: en-us
document_id: 26355eec-77f2-0c26-2b09-755bfd37aac9
document_version_independent_id: 26355eec-77f2-0c26-2b09-755bfd37aac9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/adv-tech-of-mdav.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: adv-tech-of-mdav
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/adv-tech-of-mdav.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/d6f38669-3d05-40f2-afd8-e49f7dd20884
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/55265cca-de9b-48dc-a77a-9047cc39a575
platformId: 34e83cd2-d71d-b8cb-de57-b7fe35c27546
---

# Advanced technologies at the core of Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender Antivirus and the multiple engines that lead to the advanced detection and prevention technologies under the hood to detect and stop a wide range of threats and attacker techniques at multiple points, as depicted in the following diagram:

![Diagram depicting next generation protection engines and how they work between the cloud and the client device.](media/next-gen-protection-engines.png)

Many of these engines are built into the client and provide advanced protection against most threats in real time.

These next-generation protection engines provide [industry-best](/en-us/defender-xdr/top-scoring-industry-tests) detection and blocking capabilities and ensure that protection is:

- **Accurate**: Threats both common and sophisticated, many which are designed to try to slip through protections, are detected and blocked.
- **Real-time**: Threats are prevented from getting on to devices, stopped in real-time at first sight, or detected and remediated in the least possible time (typically within a few milliseconds).
- **Intelligent**: Through the power of the cloud, machine learning (ML), and Microsoft's industry-leading optics, protection is enriched and made even more effective against new and unknown threats.

## Hybrid detection and protection

Microsoft Defender Antivirus does hybrid detection and protection. What this means is, detection and protection occur on the client device first, and works with the cloud for newly developing threats, which results in faster, more effective detection and protection.

When the client encounters unknown threats, it sends metadata or the file itself to the cloud protection service, where more advanced protections examine new threats on the fly and integrate signals from multiple sources.

| On the client | In the cloud |
| --- | --- |
| **Machine learning (ML) engine** A set of light-weight machine learning models make a verdict within milliseconds. These models include specialized models and features that are built for specific file types commonly abused by attackers. Examples include models built for portable executable (PE) files, PowerShell, Office macros, JavaScript, PDF files, and more. | **Metadata-based ML engine** Specialized ML models, which include file type-specific models, feature-specific models, and adversary-hardened [monotonic models](https://www.microsoft.com/security/blog/2019/07/25/new-machine-learning-model-sifts-through-the-good-to-unearth-the-bad-in-evasive-malware/), analyze a featurized description of suspicious files sent by the client. Stacked ensemble classifiers combine results from these models to make a real-time verdict to allow or block files pre-execution. |
| **Behavior monitoring engine** The behavior monitoring engine monitors for potential attacks post-execution. It observes process behaviors, including behavior sequence at runtime, to identify and block certain types of activities based on predetermined rules. | **Behavior-based ML engine** Suspicious behavior sequences and advanced attack techniques are monitored on the client as triggers to analyze the process tree behavior using real-time cloud ML models. Monitored attack techniques span the attack chain, from exploits, elevation, and persistence all the way through to lateral movement and exfiltration. |
| **Memory scanning engine** This engine scans the memory space used by a running process to expose malicious behavior that could be hiding through code obfuscation. | **Antimalware Scan Interface (AMSI)-paired ML engine** Pairs of client-side and cloud-side models perform advanced analysis of scripting behavior pre- and post-execution to catch advanced threats like fileless and in-memory attacks. These models include a pair of models for each of the scripting engines covered, including PowerShell, JavaScript, VBScript, and Office VBA macros. Integrations include both dynamic content calls and/or behavior instrumentation on the scripting engines. |
| **AMSI integration engine** Deep in-app integration engine enables detection of fileless and in-memory attacks through [AMSI](/en-us/windows/desktop/AMSI/antimalware-scan-interface-portal), defeating code obfuscation. This integration blocks malicious behavior of scripts client-side. | **File classification ML engine** Multi-class, deep neural network classifiers examine full file contents, provides an extra layer of defense against attacks that require more analysis. Suspicious files are held from running and submitted to the cloud protection service for classification. Within seconds, full-content deep learning models produce a classification and reply to the client to allow or block the file. |
| **Heuristics engine** Heuristic rules identify file characteristics that have similarities with known malicious characteristics to catch new threats or modified versions of known threats. | **Detonation-based ML engine** Suspicious files are detonated in a sandbox. Deep learning classifiers analyze the observed behaviors to block attacks. |
| **Emulation engine** The emulation engine dynamically unpacks malware and examines how they would behave at runtime. The dynamic emulation of the content and scanning both the behavior during emulation and the memory content at the end of emulation defeat malware packers and expose the behavior of polymorphic malware. | **Reputation ML engine** Domain-expert reputation sources and models from across Microsoft are queried to block threats that are linked to malicious or suspicious URLs, domains, emails, and files. Sources include Windows Defender SmartScreen for URL reputation models and Defender for Office 365 for email attachment expert knowledge, among other Microsoft services through the Microsoft Intelligent Security Graph. |
| **Network engine** Network activities are inspected to identify and stop malicious activities from threats. | **Smart rules engine** Expert-written smart rules identify threats based on researcher expertise and collective knowledge of threats. |
| **CommandLine scanning engine** This engine scans the commandlines of all processes before they execute. If the commandline for a process is found to be malicious it is blocked from execution. | **CommandLine ML engine** Multiple advanced ML models scan the suspicious commandlines in the cloud. If a commandline is found to be malicious, cloud sends a signal to the client to block the corresponding process from starting. |

For more information, see [Microsoft 365 Defender demonstrates 100 percent protection coverage in the 2023 MITRE Engenuity ATT&CK® Evaluations: Enterprise](https://www.microsoft.com/security/blog/2023/09/20/microsoft-365-defender-demonstrates-100-percent-protection-coverage-in-the-2023-mitre-engenuity-attck-evaluations-enterprise/).

## How next-generation protection works with other Defender for Endpoint capabilities

Together with [attack surface reduction](attack-surface-reduction-overview), which includes advanced capabilities like hardware-based isolation, application control, exploit protection, network protection, controlled folder access, [attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview), and network firewall, [next-generation protection](microsoft-defender-antivirus-windows) engines deliver Microsoft Defender for Endpoint's prebreach capabilities, stopping attacks before they can infiltrate devices and compromise networks.

As part of Microsoft's defense-in-depth solution, the superior performance of these engines accrues to the [Microsoft Defender for Endpoint](https://www.microsoft.com/security/business/endpoint-security/microsoft-defender-endpoint) unified endpoint protection, where antivirus detections and other next-generation protection capabilities enrich endpoint detection and response, automated investigation and remediation, advanced hunting, threat and vulnerability management, managed threat hunting service, and other capabilities.

These protections are further amplified through [Microsoft Defender XDR](https://www.microsoft.com/security/business/siem-and-xdr/microsoft-defender-xdr), Microsoft's comprehensive, end-to-end security solution for the modern workplace. Through [signal-sharing and orchestration of remediation across Microsoft's security technologies](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-Microsoft-Threat-Protection/ba-p/262783), Microsoft Defender XDR secures identities, endpoints, email and data, apps, and infrastructure.

## Memory protection and memory scanning

Microsoft Defender Antivirus (MDAV) provides memory protection with different engines:

| Client | Cloud |
| --- | --- |
| Behavior Monitoring | Behavior-based Machine Learning |
| Antimalware Scan Interface(AMSI) integration | AMSI-paired Machine Learning |
| Emulation | Detonation-based Machine Learning |
| Memory scanning | N/A |

An additional layer to help prevent memory-based attacks is to use the ASR rule [Block Office applications from injecting code into other processes](attack-surface-reduction-rules-reference#block-office-applications-from-injecting-code-into-other-processes).

## Frequently asked questions

### How many malware threats does Microsoft Defender Antivirus block per month?

[Five billion threats on devices every month](https://www.microsoft.com/security/blog/2019/05/14/executing-vision-microsoft-threat-protection/).

### How does Microsoft Defender Antivirus memory protection help?

See [Detecting reflective DLL loading with Windows Defender for Endpoint](https://www.microsoft.com/security/blog/2017/11/13/detecting-reflective-dll-loading-with-windows-defender-atp/) to learn about one way Microsoft Defender Antivirus memory attack protection helps.

### Do you all focus your detections/preventions in one specific geographic area?

No, we are in all the geographical regions (Americas, EMEA, and APAC).

### Do you all focus on specific industries?

We focus on every industry.

### Do your detection/protection require a human analyst?

When you're pen-testing, you should demand where no human analysts are engaged on detect/protect, to see how the actual antivirus engine (prebreach) efficacy truly is, and a separate one where human analysts are engaged. You can add [Microsoft Defender Experts for XDR](/en-us/defender-xdr/dex-xdr-overview) a managed extended detection and response service to augment your SOC.

The ***continuous iterative enhancement*** each of these engines to be increasingly effective at catching the latest strains of malware and attack methods. These enhancements show up in consistent [top scores in industry tests](/en-us/defender-xdr/top-scoring-industry-tests), but more importantly, translate to [threats and malware outbreaks](https://www.microsoft.com/security/blog/2018/03/07/behavior-monitoring-combined-with-machine-learning-spoils-a-massive-dofoil-coin-mining-campaign/) stopped and [more customers protected](https://www.microsoft.com/security/blog/2018/03/22/why-windows-defender-antivirus-is-the-most-deployed-in-the-enterprise/).