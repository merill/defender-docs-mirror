---
layout: Conceptual
title: Security content reference for Dynamics 365 Finance and Operations | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/dynamics-365/dynamics-365-finance-operations-security-content
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: mapankra
description: Learn about the built-in security content provided by the Microsoft Sentinel solution for Dynamics 365 Finance and Operations.
ms.author: monaberdugo
author: mberdugo
ms.topic: reference
ms.date: 2024-11-14T00:00:00.0000000Z
locale: en-us
document_id: 5e627128-fc30-87be-dd0d-bb4044183f0c
document_version_independent_id: 2bbc0182-e037-bc3e-93bf-e0a47207fdd5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/dynamics-365/dynamics-365-finance-operations-security-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/dynamics-365/dynamics-365-finance-operations-security-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/dynamics-365/dynamics-365-finance-operations-security-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/410e33a0-5420-48ba-a8e2-7fb3dc6a9163
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/437f62ae-23a5-4ffc-9ff2-ac42acc41d76
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 25c44d68-4abb-f489-8690-cc4ace4b8e2f
---

# Security content reference for Dynamics 365 Finance and Operations | Microsoft Learn

This article details the security content available for the Microsoft Sentinel solution for Dynamics 365 Finance and Operations.

[Learn more about the solution](dynamics-365-finance-operations-solution-overview).

## Built-in analytics rules

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| **F&O – Non-interactive account mapped to self or sensitive privileged user** | Identifies changes to Microsoft Entra Client Apps registered for Finance & Operations, specifically when: - A new client is mapped to a predefined list of sensitive privileged user accounts, or - When a user associates a client app with their own account. | Mapping modifications in Finance and Operations portal, under **Modules &gt; System Administration &gt; Microsoft Entra Applications**. Data source: `FinanceOperationsActivity_CL` | Credential Access, Persistence, Privilege Escalation |
| **F&O – Mass update or deletion of user account records** | Identifies large delete or update operations on Finance and Operations user records based on predefined thresholds. Default update threshold: **50**Default delete threshold: **10** | Deletions or modifications in Finance and Operations portal, under **Modules &gt; System Administration &gt; Users**Data source: `FinanceOperationsActivity_CL` | Impact |
| **F&O – Bank account change following network alias reassignment** | Identifies updates to bank account number by a user account which his alias was recently modified to a new value. | Changes in bank account number, in Finance and Operations portal, under **Workspaces &gt; Bank management &gt; All bank accounts** correlated with a relevant change in the user account to alias mapping.Data source: `FinanceOperationsActivity_CL` | Credential Access, Lateral Movement, Privilege Escalation |
| **F&O – Reverted bank account number modifications** | Identifies changes to bank account numbers in Finance & Operations, whereby a bank account number is modified but then subsequently reverted a short time later. | Changes in bank account number, in Finance and Operations portal, under **Workspaces &gt; Bank management &gt; All bank accounts**.Data source: `FinanceOperationsActivity_CL` | Impact |
| **F&O – Unusual sign-in activity using single factor authentication** | Identifies successful sign-in events to Finance & Operations and Lifecycle Services using single factor/password authentication. Sign-in events from tenants that aren't using MFA, coming from a Microsoft Entra ID trusted network location, or from geographic locations seen in the last 14 days are excluded.This detection uses logs ingested from Microsoft Entra ID and you must enable the [Microsoft Entra data connector](../data-connectors-reference#microsoft-entra-id). | Sign-ins to the monitored Finance and Operations environment.Data source: `Signinlogs` | Credential Access, Initial Access |