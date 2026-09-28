---
layout: Conceptual
title: Use Intel explorer in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/threat-intelligence-explorer
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use Intel explorer in the Microsoft Defender portal to search, create, manage, and investigate threat intelligence.
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- highpri
- tier1
ms.topic: how-to
ms.date: 2026-09-02T00:00:00.0000000Z
ms.custom: cx-ti, cx-ta
ai-usage: ai-assisted
locale: en-us
document_id: 1b69e747-f31a-c2d7-6d1c-2e1e87271506
document_version_independent_id: 1b69e747-f31a-c2d7-6d1c-2e1e87271506
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/threat-intelligence-explorer.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: threat-intelligence-explorer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/threat-intelligence-explorer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 49dfc5df-c089-cfdd-f226-3a1663553be4
---

# Use Intel explorer in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Intel explorer provides a centralized experience for searching and investigating threat intelligence in the Microsoft Defender portal. You can also use Intel explorer to create and manage Microsoft Sentinel threat intelligence.

Use Intel explorer to:

- Search and filter threat intelligence.
- Create STIX threat intelligence objects.
- Manage threat intelligence with ingestion rules.
- Manage relationships between threat intelligence objects.
- Add tags and edit threat intelligence objects.
- Investigate indicators and related infrastructure.
- Query threat intelligence with Advanced hunting.
- Export threat intelligence to supported TAXII destinations.

Note

The legacy standalone Microsoft Threat Intelligence portal and legacy Intel Explorer experience were retired on August 1, 2026. This article describes the threat intelligence experience integrated into the Microsoft Defender portal. For more information, see [Transition to the new Threat intelligence experience](threat-intelligence-transition).

## Prerequisites

Before you begin:

- Publicly available Microsoft Threat Intelligence data is available to Microsoft Defender XDR customers at no additional cost.
- To create and manage Microsoft Sentinel threat intelligence, you need the permissions of a [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) or higher role.
- To import or export threat intelligence, install the Threat Intelligence solution in Microsoft Sentinel and enable the relevant connectors. For more information, see [Use STIX/TAXII to import and export threat intelligence in Microsoft Sentinel](/en-us/azure/sentinel/connect-threat-intelligence-taxii).

Important

Microsoft Threat Intelligence can include observations of active malicious infrastructure and adversary tooling. You can safely search suspicious IP addresses, domains, and other indicators in Intel explorer. Don't browse directly to suspicious or malicious resources from a web browser.

## Search and filter threat intelligence

Use Intel explorer to search and filter threat intelligence without writing a query.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Enter a keyword or value in the search box.
4. Select a threat intelligence type.

    To narrow the results, use one or more of the available filters:

    - **Targeted industries**, **Targeted geography**, or **Source**: Filter results by common threat intelligence attributes.
    - **Add filter**: Filter by additional attributes available for the selected threat intelligence type.
5. Select a threat intelligence object to open its details.

The information available depends on the type of object you select. For example, an IP address can include:

- Reputation
- Related threat intelligence articles
- Services
- Resolutions
- Certificates

Note

Changes to threat intelligence might take a few minutes to appear in Intel explorer. If you don't see a recent change, refresh the page after a few minutes.

Tip

When working with a defanged indicator such as `contoso[.]com`, remove the brackets before entering the value in Intel explorer. Don't enter malicious indicators directly into a web browser.

## Create threat intelligence

Use Intel explorer to create STIX threat intelligence objects and define relationships between them.

### Create a STIX object

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Select the **Indicators** tab.
4. Select **New**.
5. Select an **Object type**.
6. Enter the object details.

    [![Screenshot of the New TI object pane in Intel explorer showing fields for creating an indicator.](media/threat-intelligence-explorer/intel-explorer-create-ti-object.png)](media/threat-intelligence-explorer/intel-explorer-create-ti-object.png#lightbox)
7. Specify a sensitivity value or **Traffic light protocol (TLP)** rating if needed.
8. Select **Add** to create the object.

To create another object with the same common metadata, select **Add and duplicate** instead of **Add**.

For more information about supported STIX objects, see [Threat intelligence in Microsoft Sentinel](/en-us/azure/sentinel/understand-threat-intelligence#create-and-manage-threat-intelligence).

## Manage threat intelligence with ingestion rules

Use ingestion rules to modify incoming threat intelligence based on defined conditions. For example, you can reduce noise, extend the validity of high-value indicators, or add tags to incoming objects.

To create an ingestion rule:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Select **Ingestion rules**.
4. Enter a name for the rule.
5. Select an **Object type**.
6. Select **Add condition**.
7. Configure the condition.
8. Select **Action**.
9. Select an action.
10. Select **Add action** if additional configuration is required.
11. Configure the action.
12. Add a tag if needed.
13. Select the rule **Order**.
14. Turn on **Status** if you want to enable the rule.
15. Select **Add**.

Rules run from the lowest order number to the highest. Each rule evaluates every object that's ingested.

Note

An object's **Modified** date isn't updated when the object is changed by an ingestion rule.

For more information, see [Threat intelligence ingestion rules](/en-us/azure/sentinel/understand-threat-intelligence#configure-ingestion-rules).

## Manage relationships between threat intelligence objects

Use relationships to connect threat intelligence objects and provide context about how the objects are associated.

To add or edit a relationship:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Search for and select a threat intelligence object.
4. In the entity side panel, find the relationships section.
5. Add a new relationship or edit an existing relationship.
6. Select the relationship type and related threat intelligence object.
7. Save your changes.

Common STIX relationships include:

| Relationship type | Description |
| --- | --- |
| **Duplicate of**, **Derived from**, **Related to** | Common relationships for STIX domain objects |
| **Targets** | An `Attack pattern` or `Threat actor` targets an `Identity` |
| **Uses** | A `Threat actor` uses an `Attack pattern` |
| **Attributed to** | A `Threat actor` is attributed to an `Identity` |
| **Indicates** | An `Indicator` indicates an `Attack pattern` or `Threat actor` |
| **Impersonates** | A `Threat actor` impersonates an `Identity` |

For more information, see the [STIX 2.1 relationship specification](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html).

## Tag threat intelligence

Use tags to group threat intelligence objects and make them easier to find.

If an object represents a connection to another threat intelligence object, such as a threat actor or campaign, consider creating a relationship instead of using a tag.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Search for the threat intelligence objects you want to update.
4. Select one or more objects of the same type.
5. Select **Add tags**.
6. Enter one or more tags.
7. Save the changes.

Because tags are free-form, use consistent naming conventions across your organization.

## Edit threat intelligence

You can edit threat intelligence objects one at a time.

For objects created directly in Microsoft Sentinel, all supported fields are editable. For threat intelligence ingested from partner sources such as threat intelligence platforms (TIPs) and TAXII servers, only specific fields are editable, including:

- Tags
- Expiration date
- Confidence
- Revoked

Only the latest version of a threat intelligence object appears in Intel explorer.

To edit an object:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Search for the threat intelligence object.
4. Select the object.
5. Select **Edit**.
6. Update the supported fields.
7. Save the changes.

For more information about how threat intelligence objects are updated, see [Threat intelligence lifecycle](/en-us/azure/sentinel/understand-threat-intelligence#threat-intelligence-lifecycle).

## Review enriched indicator information

IP address and domain indicators can include `GeoLocation` and `WhoIs` data to provide more context during an investigation.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Search for an IP address or domain indicator.
4. Select the indicator.
5. Review the available `GeoLocation` and `WhoIs` information.

[![Screenshot of an indicator details pane in Intel explorer showing indicator information and WHOIS data.](media/threat-intelligence-explorer/intel-explorer-indicator-details.png)](media/threat-intelligence-explorer/intel-explorer-indicator-details.png#lightbox)

Important

`GeoLocation` and `WhoIs` enrichment is currently in preview. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet generally available.

## Investigate related threat intelligence

Use related threat intelligence to move from an artifact or indicator to associated Microsoft threat research and other threat intelligence objects.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Search for an artifact or indicator.
4. Select the search result.
5. Review related threat intelligence.
6. Select a related threat intelligence object.
7. Review the object details.
8. Select a related indicator to continue the investigation.

For example, you can start with a vulnerability, review related Microsoft threat intelligence, and then investigate indicators associated with reported exploitation activity.

## Investigate related infrastructure

Use infrastructure relationships to identify connections between artifacts and expand an investigation from an initial indicator.

Infrastructure chaining uses relationships between connected data to help identify additional infrastructure associated with an adversary or campaign.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Search for an IP address or domain.
4. Select the search result.
5. Review the available infrastructure information.
6. Select a related artifact.
7. Review the intelligence for the selected artifact.
8. Select another related artifact to continue the investigation.

Depending on the artifact, infrastructure information can include:

- DNS and reverse DNS data
- Resolutions
- WHOIS information
- Subdomains
- Certificates
- Services
- Trackers
- Components
- Cookies

For a walkthrough, see [Gather threat intelligence and perform infrastructure chaining](gathering-threat-intelligence-and-infrastructure-chaining).

## Export threat intelligence

You can export Microsoft Sentinel threat intelligence from Intel explorer to supported external destinations.

For example, if you ingest threat intelligence by using the **Threat Intelligence - TAXII** data connector, you can export threat intelligence back to a TAXII server for bidirectional intelligence sharing.

Microsoft Sentinel supports exporting threat intelligence to TAXII 2.1-based platforms.

Important

Carefully consider the threat intelligence data you export and its destination, which might reside in a different geographic or regulatory region. Data export can't be undone. Make sure that you own the data or have authorization to export or share it with third parties.

To export threat intelligence:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Select one or more STIX objects.
4. Select **Export**.
5. Select a server from the **Export TI** dropdown.
6. Select **Export**.

If no server is available, configure a TAXII 2.1 server for export. For more information, see [Enable the Threat Intelligence - TAXII Export data connector](/en-us/azure/sentinel/connect-threat-intelligence-taxii#enable-the-threat-intelligence---taxii-export-data-connector).

Important

Threat intelligence export uses a bulk operation. If a bulk export operation fails, Microsoft Sentinel pauses subsequent export operations until the failed operation is removed from the bulk operations history.

### View export history

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Threat intelligence** &gt; **Intel explorer**.
3. Find the exported threat intelligence object.
4. Select **View export history** in the **Exports** column.