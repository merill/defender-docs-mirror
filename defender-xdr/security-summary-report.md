---
layout: Conceptual
title: Visualize security impact with the unified security summary - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-summary-report
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the unified security summary in the Microsoft Defender portal to visualize your security impact and achievements.
ms.service: defender-xdr
ms.localizationpriority: medium
author: guywi-ms
ms.author: guywild
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.collection:
- m365-security
- tier2
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 435b245e-187b-9bcd-2925-6bfe9f8da03f
document_version_independent_id: 435b245e-187b-9bcd-2925-6bfe9f8da03f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-summary-report.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-summary-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-summary-report.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: da29cfb9-4282-1570-b209-23a22e6e8b98
---

# Visualize security impact with the unified security summary - Microsoft Defender XDR | Microsoft Learn

Security operations center (SOC) teams can easily showcase their security achievements and the impact of Microsoft Defender using the unified security summary. Having the summary readily available in the Microsoft Defender portal streamlines the process for SOC teams to generate security reports, saving time usually spent on collecting data from various sources and creating reports tailored to their audiences. SOC teams can readily communicate performance and achievements to their stakeholders with the unified security summary.

The unified security summary highlights the following information:

- **Posture**: Your organization’s posture includes data from [Microsoft Secure Score](microsoft-secure-score), threat protection information related to ransomware and phishing prevention, [exposure score](/en-us/defender-vulnerability-management/tvm-exposure-score) based on Microsoft Defender Vulnerability Management, and the number of onboarded devices to Microsoft Defender for Endpoint [![Screenshot of the Posture section in the security summary report](media/security-summary-report/summary-posture-small.png)](media/security-summary-report/summary-posture.png#lightbox)
- **Detection**: This section contains the number of [incidents and alerts overview](incidents-overview), including how many alerts were consolidated into incidents, the number of alerts grouped into incidents, and information on active detection rules and the corresponding response actions produced by those rules [![Screenshot of the Detection section in the security summary report](media/security-summary-report/summary-detection-small.png)](media/security-summary-report/summary-detection.png#lightbox)
- **Protection**: Cards under this section include data from Microsoft’s automatic investigation and response features like the total number of [automatic attack disruptions](automatic-attack-disruption), a list of the disruption incidents, the number of malicious activities blocked by Microsoft Defender Antivirus, and the number of malicious emails and URLs blocked [![Screenshot of the Protection section in the security summary report](media/security-summary-report/summary-protection-small.png)](media/security-summary-report/summary-protection.png#lightbox)
- **Investigation and response**: This section contains the number of active and resolved alerts and incidents, top 10 critical incidents with each incident’s status and affected number of assets, the number of [automated investigation and response in Microsoft Defender](m365d-autoir) actions taken on impacted assets, and the number of email messages where malicious files were automatically identified and extracted through [Microsoft Defender for Office 365 Zero-hour auto purge (ZAP)](/en-us/defender-office-365/zero-hour-auto-purge)[![Screenshot of the Investigation and Response section in the security summary report](media/security-summary-report/summary-investigation-small.png)](media/security-summary-report/summary-investigation.png#lightbox)
- **Copilot-powered investigation and response**: This section contains the number of [file analysis in Copilot in Defender](copilot-in-defender-file-analysis) and [script analysis in Copilot in Defender](security-copilot-m365d-script-analysis) operations where Microsoft Copilot in Defender was used. [![Screenshot of the Copilot section in the security summary report](media/security-summary-report/summary-copilot-small.png)](media/security-summary-report/summary-copilot.png#lightbox)

SOC teams can use the unified security summary to highlight the impact of their day-to-day operations. They can also emphasize how Microsoft’s automated actions impact the efficient protection of their organization with features like automatic attack disruption, which stops attacks before they become widespread.

## Prerequisites

Important

Data for the unified security summary is based on the Microsoft security products and services present in the organization. Data is limited only to the Microsoft products which the user has provisioned access to. For example, if the organization has Microsoft Defender for Endpoint and Microsoft Defender for Office 365, the summary will only show data from these two products.

Users must have the following permissions to view the unified security summary:

- Security data basics (read)
- Vulnerability management (read)

Additionally, users must have permissions to view all devices in the organization.

## View the unified security summary

To access and share the unified security summary, follow these steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. In the navigation, select **Reports**. Under General, select **Unified security summary**.
3. The report page automatically generates data from the last 90 days by default. You can adjust the data to show the last 30 days if needed. ![Screenshot highlighting the report data duration options in the security summary report](media/security-summary-report/duration-picker.png)
4. Once the summary is generated, you can check the details of each card under each section. 
    Tip

    Select a card's title to learn more about that card. Selecting the title opens the Microsoft documentation page for that card's feature or metric.
5. You can export the summary as a PDF or CSV file. To export, select the dropdown menu on the upper right corner of the page and choose the format. ![Screenshot highlighting the export options in the security summary report](media/security-summary-report/export-picker.png)
6. If you choose to export the summary as a PDF, an option to customize by adding a logo of your choice is available. Select **Upload logo** to add a logo to the PDF. Otherwise, you can select **Generate PDF** to proceed exporting the summary to a PDF file. ![Screenshot of the export to PDF dialog box](media/security-summary-report/pdf-dialog.png)
7. When exporting the summary as a CSV file, the file is automatically saved to your device as *Unified security summary\_{date and time exported}.csv*. The file contains three columns for the card name, the field name in the card, and the value of the field. Here’s an example. ![Screenshot of the CSV output of the security summary report](media/security-summary-report/csv-sample-values.png)