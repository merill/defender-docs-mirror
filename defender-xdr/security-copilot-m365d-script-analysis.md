---
layout: Conceptual
title: Script analysis with Microsoft Copilot in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-copilot-m365d-script-analysis
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Use Microsoft Copilot script analysis in Microsoft Defender to investigate scripts and command lines.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.update-cycle: 180-days
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: da896928-024c-f12d-ffab-bd65f5d916bc
document_version_independent_id: da896928-024c-f12d-ffab-bd65f5d916bc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-copilot-m365d-script-analysis.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot-m365d-script-analysis
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-copilot-m365d-script-analysis.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a3de7266-362e-38cc-85a7-4668956f5ba9
---

# Script analysis with Microsoft Copilot in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Through AI-powered investigation capabilities from [Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) in the Microsoft Defender portal, security teams can speed up their analysis of malicious or suspicious scripts and command lines.

This guide describes what the script analysis capability is and how it works, including how you can provide feedback on the results generated.

## Before you begin

If you're new to Security Copilot, you should familiarize yourself with it by reading the following articles:

- [What is Security Copilot?](/en-us/security-copilot/microsoft-security-copilot)
- [Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Get started with Security Copilot](/en-us/security-copilot/get-started-security-copilot)
- [Understand authentication in Security Copilot](/en-us/security-copilot/authentication)
- [Prompting in Security Copilot](/en-us/security-copilot/prompting-security-copilot)

Most complex and sophisticated attacks like [Microsoft ransomware guidance](/en-us/security/ransomware) evade detection through numerous ways, including the use of scripts and PowerShell command lines. Moreover, these scripts are often obfuscated, which adds to the complexity of detection and analysis. Security operations teams need to quickly analyze scripts to understand capabilities and apply appropriate mitigation, immediately stopping attacks from progressing further within a network.

The script analysis capability provides security teams added capacity to inspect scripts without using external tools. The script analysis capability also reduces the complexity of analysis, minimizing challenges and allowing security teams to quickly assess and identify a script as malicious or benign.

## Security Copilot integration in Microsoft Defender

The script analysis capability is available in the Microsoft Defender portal for customers who have provisioned access to Security Copilot.

Script analysis is also available in the Security Copilot standalone experience through the Microsoft Defender XDR plugin. For information about the Microsoft Defender XDR plugin, see [Preinstalled plugins in Security Copilot](/en-us/security-copilot/manage-plugins#preinstalled-plugins).

## Key script analysis features

You can access the script analysis capability within the attack story below the incident graph on an incident page and in the device timeline view. For more information, see [Investigate the device timeline](/en-us/defender-endpoint/investigate-machines#investigate-device-timeline).

To begin analysis, perform the following steps:

1. Open an incident page then select an item on the left pane to open the attack story below the incident graph. Within the attack story, select an event with a script or command line that you want to analyze. Click **Analyze** to start the analysis.

    [![Screenshot that shows the script analysis button in the attack story view.](media/copilot-in-defender/script-analyzer/copilot-defender-script-analysis-incident-small.png)](media/copilot-in-defender/script-analyzer/copilot-defender-script-analysis-incident.png#lightbox)

    Alternately, you can select an event to inspect in the device timeline view. On the file details pane, select **Analyze** to run the script analysis capability.

    [![Screenshot that shows the Analyze button in the device timeline.](media/security-copilot-m365d-script-analysis/copilot-defender-script-device-timeline-small.png)](media/security-copilot-m365d-script-analysis/copilot-defender-script-device-timeline.png#lightbox)
2. Copilot runs script analysis and displays the results in the Copilot pane. Select **Show code** to expand the script, or **Hide code** to close the expansion.

    [![Screenshot highlighting the show or hide code option within the script analysis results.](media/security-copilot-m365d-script-analysis/show-code-script-small.png)](media/security-copilot-m365d-script-analysis/show-code-script.png#lightbox)
3. Select **Show MITRE techniques** to view the MITRE ATT&CK techniques associated with the script. This information helps you understand the techniques used by the script and how it can impact your environment. Select **Hide MITRE techniques** to close the expansion.

    [![Screenshot highlighting the show or hide MITRE techniques option within the script analysis results.](media/security-copilot-m365d-script-analysis/hide-mitre-script-small.png)](media/security-copilot-m365d-script-analysis/hide-mitre-script.png#lightbox)
4. Select the **More actions** ellipsis (...) on the upper right of the script analysis card to copy or regenerate the results, or view the results in the Security Copilot standalone experience. Selecting **Open in Security Copilot** opens a new tab to the Copilot standalone portal where you can input prompts and access other plugins.

    ![Screenshot that shows the More actions option in the Copilot script analysis card.](media/security-copilot-m365d-script-analysis/script-analysis-options.png)
5. Review the results and use the information to guide your investigation and response to the incident.

## Sample script analysis prompt

In the Security Copilot standalone portal, you can use the following prompt identify and analyze scripts:

- *Identify the scripts in Defender incident {incident ID}. Are these malicious scripts?*

Tip

When analyzing scripts in the Security Copilot portal, Microsoft recommends including the word ***Defender*** in your prompts to ensure that the script analysis capability delivers the results.

## Provide feedback on script analysis

Microsoft highly encourages you to provide feedback to Copilot, as it's crucial for a capability's continuous improvement. You can provide feedback on the results by selecting the feedback icon ![Screenshot of the feedback control used to submit feedback for Copilot responses in Defender cards.](media/copilot-in-defender/copilot-defender-feedback.png) found at the end of the script analysis card.