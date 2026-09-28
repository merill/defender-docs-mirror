---
layout: Conceptual
title: Enable Conditional Access to better protect users, devices, and data - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/conditional-access
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Microsoft Intune device compliance and Microsoft Entra Conditional Access policies to restrict access to apps and data from devices that are at risk or noncompliant.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-09-15T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e19f8102-d90a-2f45-8c83-843149d0adde
document_version_independent_id: e19f8102-d90a-2f45-8c83-843149d0adde
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/conditional-access.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: conditional-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/conditional-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: c8f7d61b-efc7-09f5-8d85-ae0b90d9fd3a
---

# Enable Conditional Access to better protect users, devices, and data - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

Conditional Access is a capability that helps you better protect your users and enterprise information by making sure that only secure devices have access to applications.

With Conditional Access, you can control access to enterprise information based on the risk level of a device. Conditional Access helps keep trusted users on trusted devices using trusted applications.

You can define security conditions under which devices and applications can run and access information from your network by enforcing policies to stop applications from running until a device returns to a compliant state.

The implementation of Conditional Access in Defender for Endpoint is based on Microsoft Intune (Intune) device compliance policies and Microsoft Entra Conditional Access policies.

This implementation requires Microsoft Intune. Intune is a separate product that isn't part of Microsoft Defender for Endpoint, and it isn't included in all subscriptions. You need licenses that support Defender for Endpoint, Intune, and Microsoft Entra Conditional Access. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses) and [Conditional Access policy license requirements](/en-us/entra/identity/conditional-access/overview#license-requirements).

A device compliance policy is used with Conditional Access to allow only devices that fulfill one or more device compliance policy rules to access applications.

## Understand the Conditional Access flow

Conditional Access is put in place so that when a threat is seen on a device, access to sensitive content is blocked until the threat is remediated.

The flow begins with devices being seen to have a low, medium, or high risk. The low, medium, or high risk determinations are then sent to Intune.

Depending on how you configure policies in Intune, Conditional Access can be set up so that when certain conditions are met, the Conditional Access policy is applied.

For example, you can configure Intune to apply Conditional Access on devices that have a high risk.

In Intune, a device compliance policy is used with Microsoft Entra Conditional Access to block access to applications. In parallel, an automated investigation and remediation process is launched.

A user can still use the device while the automated investigation and remediation is taking place, but access to enterprise data is blocked until the threat is fully remediated.

To resolve the risk found on a device, you need to return the device to a compliant state. A device returns to a compliant state when there's no risk seen on it.

There are three ways to address a risk:

1. Use Manual or automated remediation.
2. Resolve active alerts on the device. Resolving active alerts removes the risk from the device.
3. You can remove the device from the active policies and consequently, Conditional Access won't be applied on the device.

Manual remediation requires a secops admin to investigate an alert and address the risk seen on the device. For automated remediation configuration settings, see [Configure Conditional Access](configure-conditional-access).

When the risk is removed either through manual or automated remediation, the device returns to a compliant state and access to applications is granted.

The following example sequence of events explains Conditional Access in action:

1. A user opens a malicious file and Defender for Endpoint flags the device as high risk.
2. The high risk assessment is passed along to Intune. In parallel, an automated investigation is initiated to remediate the identified threat. A manual remediation can also be done to remediate the identified threat.
3. Based on the policy created in Intune, the device is marked as not compliant. The not-compliant assessment is then communicated to Microsoft Entra ID by the Intune Conditional Access policy. In Microsoft Entra ID, the corresponding policy is applied to block access to applications.
4. The manual or automated investigation and remediation is completed and the threat is removed. Defender for Endpoint sees that there's no risk on the device and Intune assesses the device to be in a compliant state. Microsoft Entra ID applies the Conditional Access policy, which allows access to applications.
5. Users can now access applications.