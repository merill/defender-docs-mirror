---
layout: Conceptual
title: Protect your Workplace environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-workplace
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Connect Workplace by Meta to Microsoft Defender for Cloud Apps with the API connector to monitor user activity and detect suspicious behavior.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 98811c55-7c15-ec35-b703-9196065999ed
document_version_independent_id: 98811c55-7c15-ec35-b703-9196065999ed
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-workplace.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-workplace
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-workplace.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: bdf87f40-774a-5dfc-6dd0-240c850bec15
---

# Protect your Workplace environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Workplace by Meta is a collaboration tool built by Meta. It brings group work, instant messaging, video calls, and news sharing into one place. Cloud collaboration has many benefits, but it can also expose critical assets to threats. These assets include messages, posts, and files that might contain sensitive data or partnership details. You need continuous monitoring to stop malicious actors or careless insiders from leaking this data.

Connect Workplace by Meta to Defender for Cloud Apps to get better insights into user activity and detect unusual behavior.

## Main threats to Workplace by Meta

The main threats to Workplace by Meta include the following:

- Compromised accounts and insider threats
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps protect your Workplace by Meta environment in the following ways:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Workplace by Meta with policies

The following table lists the policy types available for controlling Workplace by Meta:

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country/region](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as the identity provider (IdP)) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual impersonated activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy | Built a customized policy by the Workplace by Meta activities |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

Beyond monitoring for threats, you can also automate Workplace governance actions to fix detected issues:

| Type | Action |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID) Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Workplace by Meta in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## SaaS security posture management for Workplace by Meta (Preview)

When you connect Workplace by Meta to Defender for Cloud Apps using the API connector, you automatically get security posture recommendations for Workplace in Microsoft Secure Score. In Secure Score, select **Recommended actions** and filter by **Product** = **Workplace**. Workplace supports security recommendations to *Adopt SSO (Single sign on) in Workplace by Meta*.

For more information, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Connect Workplace by Meta to Microsoft Defender for Cloud Apps

The following information describes the current support status for connecting Workplace by Meta to Defender for Cloud Apps using the API connector.

Note

Due to the [Workplace from Meta planned deprecation notice](https://www.workplace.com/help/work/1167689491269151) by Meta of Workplace from Meta, we no longer support new connections to the Workplace from Meta API connector. If you have an existing Workplace from Meta connection, it will continue to work as expected.