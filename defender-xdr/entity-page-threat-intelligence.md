---
layout: Conceptual
title: View threat intelligence in entity pages in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/entity-page-threat-intelligence
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to view threat intelligence from Microsoft Threat Intelligence on IP, domain, URL, and file entity pages in the Microsoft Defender portal.
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- highpri
- tier1
- usx-security
ms.custom:
- cx-ti
ms.topic: concept-article
ms.date: 2026-07-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: ac63d89a-c19d-a90a-fae3-da62a782a67c
document_version_independent_id: ac63d89a-c19d-a90a-fae3-da62a782a67c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/entity-page-threat-intelligence.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: entity-page-threat-intelligence
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/entity-page-threat-intelligence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: b566abc2-a3c1-e6c8-c828-84e2b833925a
---

# View threat intelligence in entity pages in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product that may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Microsoft Defender enriches entity pages with threat intelligence data from Microsoft Threat Intelligence, so analysts get in-context intelligence during investigations. Instead of switching between separate tools, you can access reputation data, threat actor attribution, infrastructure relationships, and other intelligence directly on entity pages in the Microsoft Defender portal.

Entity enrichments bring globally observed threat intelligence into the investigation workflow. When you investigate an IP address, domain, URL, or file in an incident, the entity page surfaces relevant intelligence that helps you assess risk and make faster, more informed decisions.

## Prerequisites

All Microsoft Defender XDR customers can access entity enrichments with publicly available Microsoft Threat Intelligence data at no extra cost.

## Supported entity types

You can get entity enrichments for the following entity types. Each entity type surfaces different intelligence data depending on what's relevant:

| Entity type | Enrichment data available |
| --- | --- |
| [IP address](entity-page-ip) | Reputation, attributed threat reports, infrastructure relationships (DNS, WHOIS, host pairs, subdomains), services, TLS/SSL certificates, components, trackers, cookies |
| Domain | Reputation, attributed threat reports, infrastructure relationships (DNS, WHOIS, host pairs, subdomains), services, TLS/SSL certificates, components, trackers, cookies |
| URL | Reputation, attributed threat reports, sandbox analysis |
| File | Reputation, attributed threat reports, sandbox analysis |

Note

IP addresses and domains provide a broader set of enrichment data because of the additional infrastructure relationship data available for these entity types.

## How to access entity enrichments

You can access enriched entity pages through several entry points in the Microsoft Defender portal:

- **Incident investigation** - Select an entity (IP, domain, URL, or file) from an incident's evidence or alert details to open its enriched entity page.
- **Global search** - Search for an IP address, domain, URL, or file hash in the Defender portal search bar to navigate directly to the entity page.
- **Advanced hunting** - Select an entity value in advanced hunting query results to open the entity page.
- **Direct navigation** - Navigate to an entity page directly from any link in the portal.

## Threat Intelligence Insights tab

The **Threat Intelligence Insights** tab on entity pages is the primary surface for enrichment data. This tab consolidates threat intelligence from Microsoft Threat Intelligence into a single view, organized into the following sections depending on the entity type:

[![Screenshot of Defender portal entity page with Threat Intelligence Insights tab and Reputation section highlighted.](media/entity-page-threat-intelligence/threat-intel-insights-tab.png)](media/entity-page-threat-intelligence/threat-intel-insights-tab.png#lightbox)

### Reputation

The reputation section provides a risk assessment for the entity based on Microsoft's detection rules and intelligence. Reputation scores help analysts quickly determine whether an entity is categorized as malicious, suspicious, neutral, or unknown and surface any prior malicious or suspicious activity tied to the entity.

Reputation appears as a numerical score from 0 to 100. Microsoft derives the score from proprietary data and machine learning rules—each assigned a High, Medium, or Low severity—that assess factors such as the top-level domain, hosting provider, name server, registrar, and TLS certificate characteristics. Assess these factors holistically: the combination of indicators, rather than any single one, predicts whether an entity is likely malicious. Hosts, domains, and IP addresses fall into the following categories based on their score:

| Score | Category | Description |
| --- | --- | --- |
| 75–100 | Malicious | Confirmed associations to known malicious infrastructure on Microsoft's blocklist, with matches to machine learning rules that detect suspicious activity. |
| 50–74 | Suspicious | Likely associated with suspicious infrastructure based on matches to three or more machine learning rules. |
| 25–49 | Neutral | Matches at least two machine learning rules. |
| 0–24 | Unknown | Returned one or zero rule matches. |

### Attributed threat reports

When Microsoft links an entity to a known threat actor or campaign, the attributed threat reports section shows related threat analytics reports. These reports provide context about the threat actor's tactics, techniques, and procedures (TTPs) and help analysts understand the broader threat landscape.

### Infrastructure relationships (IP addresses and domains)

For IP address and domain entities, the infrastructure relationships section draws on Microsoft's internet data—collected through passive DNS (PDNS), port scans, and web-crawling infrastructure—to reveal connected infrastructure and support infrastructure analysis. This section includes:

- **DNS records** - Historical and current DNS resolution data, including reverse DNS, that shows which domains resolved to an IP address and the reverse over time.
- **WHOIS information** - Domain registration details including registrant, dates, and registrar.
- **Host pairs** - Relationships between hosts based on observed connections in web content.
- **Subdomains** - Known subdomains associated with a domain.
- **TLS/SSL certificates** - Certificate details including issuer, validity, and subject alternative names.
- **Services** - Detected network services running on the infrastructure.
- **Components** - Web technologies and frameworks identified on the infrastructure.
- **Trackers** - Web analytics and tracking codes observed on the infrastructure.
- **Cookies** - Cookie names observed in responses from the infrastructure.

### Sandbox analysis (URLs and files)

For URL and file entities, sandbox analysis provides detonation results showing behavioral indicators observed when the entity was executed in a controlled environment.

## Investigation workflow

Entity enrichments integrate directly into the incident investigation workflow in Microsoft Defender. A typical investigation flow includes:

- Open an incident in the Microsoft Defender portal and review the incident's evidence.
- Select an entity (IP address, domain, URL, or file) to open its entity page.
- Review the **Overview** tab for key details about the entity.
- Select the **Threat Intelligence Insights** tab to view enrichment data from Microsoft Threat Intelligence.
- Use the intelligence to assess risk, identify threat actor attribution, and understand infrastructure relationships.
- Pivot to related entities and reports to continue your investigation.