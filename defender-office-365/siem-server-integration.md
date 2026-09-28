---
layout: Conceptual
title: SIEM server integration with Microsoft 365 services and applications - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/siem-server-integration
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
f1.keywords:
- NOCSH
ms.author: guywild
author: guywi-ms
audience: ITPro
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom: msecd-doc-authoring-1016 - Ent_Solutions - SIEM - seo-marvel-apr2020
description: Get an overview of Security Information and Event Management (SIEM) server integration with your Microsoft 365 cloud services and applications.
ms.service: defender-office-365
search.appverid: met150
ai-usage: ai-assisted
locale: en-us
document_id: 9ec646f8-2a96-ab82-8e4f-e349512fee78
document_version_independent_id: 9ec646f8-2a96-ab82-8e4f-e349512fee78
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/siem-server-integration.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: siem-server-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/siem-server-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 0690eb75-e184-eb19-4d93-eb06eb3516f4
---

# SIEM server integration with Microsoft 365 services and applications - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

This article explains how to integrate a Security Information and Event Management (SIEM) server with Microsoft 365 services and applications. It covers available integration methods, audit logging prerequisites, and step-by-step instructions for connecting Microsoft Sentinel to Microsoft 365 Defender data.

## Summary

Is your organization using or planning to get a Security Information and Event Management (SIEM) server? You might be wondering how it integrates with Microsoft 365 or Office 365. This article provides a list of resources you can use to integrate your SIEM server with Microsoft 365 services and applications.

Tip

If you don't have a SIEM server yet and are exploring your options, consider [Microsoft Sentinel](/en-us/azure/sentinel/overview).

## Do I need a SIEM server?

Whether you need a SIEM server depends on many factors, such as your organization's security requirements and where your data resides. Microsoft 365 includes a wide variety of security features that meet many organizations' security needs without additional servers, such as a SIEM server. Some organizations have special circumstances that require the use of a SIEM server. Here are some examples:

- *Fabrikam* has some content and applications on premises, and some in the cloud (they have a hybrid cloud deployment). To get security reports for all of their content and applications, Fabrikam implemented a SIEM server.
- *Contoso* is a financial services organization that has stringent security requirements. They added a SIEM server to their environment to take advantage of the extra security protections they require.

## SIEM server integration with Microsoft 365

A SIEM server can receive data from a wide variety of Microsoft 365 services and applications. The following table lists several Microsoft 365 services and applications, along with SIEM server inputs and resources to learn more.

| Microsoft 365 Service or Application | SIEM server inputs/methods | Resources to learn more |
| --- | --- | --- |
| [Microsoft Defender for Office 365](mdo-about) | Audit logs | [SIEM integration with Microsoft Defender for Office 365](siem-integration-with-office-365-ti) |
| [Microsoft Defender for Endpoint](/en-us/windows/security/threat-protection/) | HTTPS endpoint hosted in Azure <br> REST API | [Pull alerts to your SIEM tools](/en-us/defender-endpoint/configure-siem) |
| [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps) | Log integration | [SIEM integration with Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/siem) |

Tip

Take a look at [Microsoft Sentinel](/en-us/azure/sentinel/overview). Microsoft Sentinel comes with connectors for Microsoft solutions. These connectors are available "out of the box" and provide for real-time integration. You can use Microsoft Sentinel with your Microsoft Defender XDR solutions and Microsoft 365 services, including Office 365, Microsoft Entra ID, Microsoft Defender for Identity, Microsoft Defender for Cloud Apps, and more.

### Audit logging must be turned on

Make sure that audit logging is turned on before you configure SIEM server integration:

- For SharePoint, OneDrive, and Microsoft Entra ID, see [Turn auditing on or off](/en-us/purview/audit-log-enable-disable).
- For Exchange Online, see [Manage mailbox auditing](/en-us/purview/audit-mailboxes).

## Integration steps if your SIEM is Microsoft Sentinel

Verify the following requirements:

- Your current Microsoft 365 subscription (for example, Microsoft Defender for Office 365 Plan 2) allows for Microsoft Sentinel integration.
- Your account in Microsoft Defender for Office 365 or Microsoft Defender is a *Security Administrator*.
- Verify that you have *Write permissions in Microsoft Sentinel*.

### Connect Microsoft Sentinel to Microsoft Defender for Office 365 data

Use the following steps to connect the Microsoft Defender XDR connector in Microsoft Sentinel and stream email event data from Microsoft Defender for Office 365 into your SIEM.

1. Navigate to Microsoft Sentinel.
2. In the left navigation pane, select **Configuration** &gt; **Data connectors**.
3. **Search for** Microsoft Defender XDR and select the **Microsoft Defender XDR (preview) connector**.
4. On the right of your screen select **Open Connector Page**.
5. Under **Configuration** &gt; select **Connect incidents & alerts**

    Turn off all Microsoft incident creation rules for the products currently selected.
6. Scroll to **Microsoft Defender for Office 365** in the **Connect events** section of the page.

    You can also choose tables from *any other Microsoft Defender product* you find helpful and applicable before you select **Apply Changes**:
7. Select **EmailEvents**, **EmailUrlInfo**, **EmailAttachmentInfo**, and **EmailPostDeliveryEvents** &gt; and **Apply Changes**.