---
layout: Conceptual
title: Daily Operational Guide - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/ops-guide/ops-guide-daily
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn about the Microsoft Defender for Identity activities that we recommend for your team on a daily basis.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: martin77s
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 88a27fbe-dbc3-bcf8-dae4-40ca76cd38d7
document_version_independent_id: 88a27fbe-dbc3-bcf8-dae4-40ca76cd38d7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/ops-guide/ops-guide-daily.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide-daily
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/ops-guide/ops-guide-daily.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 7ed5925a-4c67-a4a4-3abb-af68acbc8925
---

# Daily Operational Guide - Microsoft Defender for Identity | Microsoft Learn

This article reviews the Microsoft Defender for Identity activities we recommend for your team on a daily basis. It covers key tasks such as reviewing identity security dashboards, triaging incidents, tuning alerts, proactive threat hunting, and monitoring deployment health. These daily activities are intended for SOC analysts, security administrators, and identity management teams to help maintain a strong security posture and quickly detect identity-based threats.

## Review the Identity Security dashboard

**Where**: In Microsoft Defender, under select **Identities** &gt; **Dashboard**.

**Persona**: SOC analysts, security administrators, identity, and access management administrators

Use Defender for Identity's **Dashboard** page to view critical insights and real-time data about identity security. On a daily basis, we recommend that you focus on the **Top insights**, **Identity related incidents**, and **Entra ID users at risk** widgets.

For more information, see [Work with Defender for Identity's Identity Security dashboard (Preview)](../dashboard).

## Triage incidents by priority

**Where**: In Microsoft Defender, select **Incidents & alerts**

**Persona**: SOC analysts

When triaging incidents:

1. In the incident dashboard, filter for the following items:

    | Filter | Values |
    | --- | --- |
    | **Status** | New, In progress |
    | **Severity** | High, Medium, Low |
    | **Service source** | Keep all service sources checked. This selection should list alerts with the most fidelity, with correlation across other Microsoft XDR workloads. Select **Defender for Identity** to view items that come specifically from Defender for Identity. |
2. Select each incident to review all details. Review all tabs in the incident, the activity log, and advanced hunting.
3. In the incident's **Evidence and response** tab, select each evidence item. Select the options menu &gt; **Investigate** and then select **Activity log** or **Go hunt** as needed.
4. Triage your incidents. For each incident, select **Manage incident** and then select one of the following options:

    - True positive
    - False positive
    - Informational, expected activity

    For true alerts, specify the threat type to help your security team see threat patterns and defend your organization from risk.
5. When you're ready to start your active investigation, assign the incident to a user and update the incident status to **In progress**.
6. When the incident is remediated, resolve it to resolve all linked and related active alerts and set a classification.

## Configure tuning rules for benign true positives / false positive alerts

**Where**: In Microsoft Defender, select **Hunting &gt; Advanced hunting**

**Persona**: Security and compliance administrators, SOC analysts

If you find either benign true positives or outright false positives, we recommend that you tune your alerts to reduce the number of alerts you need to triage to match your risk appetite. Tuning alerts resolves alerts automatically based on your configurations and rule conditions.

We recommend creating new rules as needed as your network grows to make sure that your alert tuning remains relevant and effective.

For more information, see [Tune an alert](/en-us/microsoft-365/security/defender/investigate-alerts#tune-an-alert).

## Proactively hunt

**Where**: In Microsoft Defender, select **Hunting &gt; Advanced hunting**.

**Persona**: SOC analysts

You might want to proactively hunt on a daily or weekly basis, depending on your level as a SOC analyst.

Use Microsoft Defender advanced hunting to proactively explore through the last 30 days of raw data, including Defender for Identity data correlated with data streaming from other Microsoft Defender services.

Inspect events in your network to locate threat indicators and entities, including both known and potential threats.

We recommend that beginners use guided advanced hunting, which provides a query builder. If you're comfortable using Kusto Query Language (KQL), build queries from scratch as needed for your investigations.

For more information, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](/en-us/microsoft-365/security/defender/advanced-hunting-overview).

## Review Defender for Identity health issues

**Where**: In Microsoft Defender, select **Identities &gt; Health issues**.

**Persona**: Security administrators, Active Directory administrators

Check the **Health Issues** page regularly for problems in your Defender for Identity deployment, such as connectivity or sensor issues. Review both the **Global** and **Sensor** tabs.

We also recommend setting up email notifications for service issues. Notifications help you catch problems as they happen.

For more information, see [Microsoft Defender for Identity health issues](../health-alerts) and [Configure email notifications](../notifications#configure-email-notifications).