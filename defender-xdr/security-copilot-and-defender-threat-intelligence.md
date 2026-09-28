---
layout: Conceptual
title: Use Microsoft Security Copilot for threat intelligence - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-copilot-and-defender-threat-intelligence
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about Microsoft Threat Intelligence capabilities embedded in Microsoft Security Copilot, including prompts, promptbooks, and the Microsoft Threat Intelligence plugin.
keywords: security copilot, threat intelligence, microsoft threat intelligence, Security Copilot, embedded experience, vulnerability impact assessment, threat actor profile, plugins, Microsoft plugins
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.custom:
- cx-ti
ms.topic: how-to
ms.update-cycle: 180-days
ms.date: 2026-07-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5d787902-0bee-ac33-a408-2513a64b8b0c
document_version_independent_id: 5d787902-0bee-ac33-a408-2513a64b8b0c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-copilot-and-defender-threat-intelligence.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot-and-defender-threat-intelligence
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-copilot-and-defender-threat-intelligence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: a60657b9-5923-08c5-67ba-f4334c835969
---

# Use Microsoft Security Copilot for threat intelligence - Microsoft Defender XDR | Microsoft Learn

Microsoft Security Copilot is a cloud-based AI platform that provides a natural language copilot experience. It can help support security professionals in different scenarios, like incident response, threat hunting, and intelligence gathering. For more information about what it can do, read [What is Microsoft Security Copilot?](/en-us/copilot/security/microsoft-security-copilot).

Security Copilot customers receive access to Microsoft Threat Intelligence for each authenticated Copilot user. To ensure that you have access to Copilot, see the [Security Copilot purchase and licensing information](/en-us/copilot/security/faq-security-copilot).

Once you have access to Security Copilot, the key features discussed in this article become accessible in either the Security Copilot portal or the [Microsoft Defender portal](defender-threat-intelligence#use-microsoft-copilot-in-defender-for-threat-intelligence).

## Know before you begin

If you're new to Security Copilot, you should familiarize yourself with it by reading these articles:

- [What is Microsoft Security Copilot?](/en-us/copilot/security/microsoft-security-copilot)
- [Microsoft Security Copilot experiences](/en-us/copilot/security/experiences-security-copilot)
- [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot)
- [Understand authentication in Microsoft Security Copilot](/en-us/copilot/security/authentication)
- [Prompting in Microsoft Security Copilot](/en-us/copilot/security/prompting-security-copilot)

## Security Copilot integration with Microsoft Threat Intelligence

Security Copilot delivers information about threat actors, indicators of compromise (IOCs), tools, and vulnerabilities, as well as contextual threat intelligence from Microsoft Threat Intelligence. You can use the prompts and promptbooks to investigate incidents, enrich your hunting flows with threat intelligence information, or gain more knowledge about your organization's or the global threat landscape.

- Be clear and specific with your prompts. You might get better results if you include specific threat actor names or IOCs in your prompts. It might also help if you add **threat intelligence** to your prompt, like:

    - Show me threat intelligence data for Aqua Blizzard.
    - Summarize threat intelligence data for "malicious.com."
- Be specific when referencing an incident (for example, "incident ID 15324").
- Experiment with different prompts and variations to see what works best for your use case. Chat AI models vary, so iterate and refine your prompts based on the results you receive.
- Copilot saves your prompt sessions. To see the previous sessions, from the Security Copilot [Home menu](/en-us/copilot/security/navigating-security-copilot#home-menu), go to **My sessions**.

    ![Screenshot that shows the Microsoft Security Copilot Home menu with My sessions highlighted.](media/security-copilot-and-defender-threat-intelligence/copilot-my-sessions.png)

    Note

    For a walkthrough on Copilot, including the pin and share feature, read [Navigate Microsoft Security Copilot](/en-us/copilot/security/navigating-security-copilot).

[Learn more about creating effective prompts](/en-us/copilot/security/prompting-tips)

## Key features

Security Copilot lets security teams understand, prioritize, and take action on threat intelligence information immediately.

You can ask about a threat actor, attack campaign, or any other threat intelligence that you want to know more about, and Copilot generates responses based on threat analytics reports, intel profiles and articles, and other Microsoft Threat Intelligence content.

You can also select any of the built-in prompts that are available in the Defender portal to do the following actions:

- **Summarize** the latest threats related to your organization.
- **Prioritize** which threats to focus on based on your environment's highest exposure level.
- **Ask** about the threat actors targeting a specific industry.

[Learn more about using Copilot in Defender for threat intelligence](defender-threat-intelligence#use-microsoft-copilot-in-defender-for-threat-intelligence)

## Turn on the Security Copilot integration

1. Go to [Microsoft Security Copilot](https://go.microsoft.com/fwlink/?linkid=2247989) and sign in with your credentials.
2. Make sure that the Microsoft Threat Intelligence plugin is turned on. In the prompt bar, select the **Sources** icon.

    ![Screenshot of the prompt bar in Microsoft Security Copilot with the Sources icon highlighted.](media/security-copilot-and-defender-threat-intelligence/copilot-prompts-bar-sources.png)

    In the **Manage sources** pop-up window that appears, under **Plugins**, confirm that the **Microsoft Threat Intelligence** toggle is turned on, then close the window.

    ![Screenshot of the Manage plugins pop-up window with the Microsoft Threat Intelligence plugin highlighted.](media/security-copilot-and-defender-threat-intelligence/copilot-manage-plugins.png)

    Note

    Some roles can turn the toggle on or off for plugins like Microsoft Threat Intelligence. For more information, read [Manage plugins in Microsoft Security Copilot](/en-us/copilot/security/manage-plugins).
3. Enter your prompt in the prompt bar.

### Built-in system features

Security Copilot has built-in system features that can get data from the different plugins that are turned on.

To view the list of built-in system capabilities for Microsoft Threat Intelligence:

1. In the prompt bar, select the **Prompts** icon.

    ![Screenshot of the prompt bar in Microsoft Security Copilot with the Prompts icon highlighted.](media/security-copilot-and-defender-threat-intelligence/copilot-prompts-bar-prompts.png)
2. Select **See all system capabilities**. The *Microsoft Threat Intelligence* section lists all the available capabilities that you can use.

Copilot also has the following promptbooks that also deliver information from Microsoft Threat Intelligence:

- [**Check impact of an external threat article**](/en-us/copilot/security/using-promptbooks#check-impact-of-an-external-threat-article) – Analyzes an external or third-party article to extract related IOCs, summarize the intelligence, and generate hunting queries so you can assess the potential impact of the threat reported in the article to your organization.
- [**Threat actor profile**](/en-us/copilot/security/using-promptbooks#threat-actor-profile) – Generates a report profiling a known threat actor, including suggestions to defend against their common tools and tactics.
- [**Threat Intelligence 360 report based on MDTI article**](/en-us/copilot/security/using-promptbooks#threat-intelligence-360-report-based-on-mdti-article) – Analyzes a Microsoft Threat Intelligence article to extract related IOCs, summarize the intelligence, and generate hunting queries so you can assess the potential impact of the threat reported in the article to your organization.
- [**Vulnerability impact assessment**](/en-us/copilot/security/using-promptbooks#vulnerability-impact-assessment) – Generates a report summarizing the intelligence for a known vulnerability, including steps on how to address it.

To view these promptbooks, in the prompt bar, select the **Prompts** icon then select **See all promptbooks**.

## Sample Microsoft Threat Intelligence prompts

You can use many prompts to get information from Microsoft Threat Intelligence. This section lists some ideas and examples.

### General information about threat intelligence trends

Get threat intelligence from threat articles and threat actors.

**Sample prompts** :

- Summarize the recent threat intelligence.
- Show me the latest threat articles.
- Get threat articles related to ransomware in the last six months.

### Threat actor mapping and infrastructure

Get information on threat actors and the tactics, techniques, and procedures (TTPs), sponsored states, industries, and IOCs associated with them.

**Sample prompts**:

- Tell me more about Silk Typhoon.
- Share the IOCs associated with Silk Typhoon.
- Share the TTPs associated with Silk Typhoon.
- Share threat actors associated with Russia.

### Vulnerability data by CVE

Get contextual information and threat intelligence on Common Vulnerabilities and Exposures (CVEs), which are derived from Microsoft Threat Intelligence articles, [threat analytics reports](threat-analytics), and data from [Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management) and [Microsoft Defender External Attack Surface Management](/en-us/azure/external-attack-surface-management/overview).

**Sample prompts**:

- Share the technologies that are susceptible to the vulnerability CVE-2021-44228.
- Summarize the vulnerability CVE-2021-44228.
- Show me the latest CVEs.
- Show me threat actors associated with CVE-2021-44228.
- Show me the threat articles associated with CVE-2021-44228.

### Indicator data in relation to threat intelligence

Get detailed information about an indicator (for example, IP addresses, domains, and file hashes) based on the numerous [data sets](entity-page-threat-intelligence) available in Microsoft Threat Intelligence, including reputation scores, WHOIS information, domain name system (DNS), host pairs, and certificates.

**Sample prompts**:

- What can you tell me about the domain *&lt;domain name&gt;*?
- Show me indicators related to *&lt;domain name&gt;*.
- Show me all resolutions for *&lt;domain name&gt;*.
- Show me host pairs related to *&lt;domain name&gt;*.
- Show me the reputation of the host *&lt;host name&gt;*.
- Show me all resolutions for IP address *&lt;IP address&gt;*.
- Show me the open services in *&lt;IP address&gt;*.

### Malware information

Get detailed information about a specific malware detection, which is derived from the [Microsoft Security Intelligence threat encyclopedia](https://www.microsoft.com/en-us/wdsi/threats/threat-search).

**Sample prompt**:

- What can you tell me about Ransom:Win32/WannaCrypt?

## Provide feedback

Your feedback on the Microsoft Threat Intelligence integration in Security Copilot helps with development. To provide feedback, in Copilot, select **How's this response?** at the bottom of each completed prompt and choose any of the following options:

- **Looks right** - Select this button if the results are accurate, based on your assessment.
- **Needs improvement** - Select this button if any detail in the results is incorrect or incomplete, based on your assessment.
- **Inappropriate** - Select this button if the results contain questionable, ambiguous, or potentially harmful information.

For each feedback button, you can provide more information in the next dialog box that appears. Whenever possible, and when the result is **Needs improvement**, write a few words explaining what can be done to improve the outcome. If you entered prompts specific to threat intelligence and the results aren't related, then include that information.

## Privacy and data security in Security Copilot

When you interact with Security Copilot to get Microsoft Threat Intelligence data, Copilot pulls that data from Microsoft Threat Intelligence. The prompts, the data retrieved, and the output shown in the prompt results are processed and stored within the Copilot service. [Learn more about privacy and data security in Microsoft Security Copilot](/en-us/copilot/security/privacy-data-security)