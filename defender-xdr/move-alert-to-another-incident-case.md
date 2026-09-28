---
layout: Conceptual
title: Move alerts from one incident case to another in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/move-alert-to-another-incident-case
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to move an alert from one incident case to another in the Microsoft Defender portal to correct alert correlation.
ms.service: microsoft-defender
ms.subservice: unified-security-operations
author: guywi-ms
ms.author: guywild
ms.date: 2026-07-15T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 5db012da-6085-d351-d6ed-1cd6155194e9
document_version_independent_id: 5db012da-6085-d351-d6ed-1cd6155194e9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/move-alert-to-another-incident-case.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: move-alert-to-another-incident-case
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/move-alert-to-another-incident-case.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 84c337fd-c56e-7f15-97ff-ac705e625c97
---

# Move alerts from one incident case to another in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Incident cases use alert correlation to group related alerts into a single incident case. If an alert is correlated to the wrong incident case, you can move the alert to another incident case so that analysts investigate and respond with the correct context.

When you move an alert, you must add a comment that explains the change. You can also submit feedback to Microsoft about the incorrect correlation type or irrelevant entities to help improve alert correlation.

Note

Incident cases are in preview and are the recommended experience for managing incidents in the Microsoft Defender portal. The legacy incident experience remains available during this preview.

## Prerequisites

Before you begin, make sure that:

- Your tenant is onboarded to the Microsoft Defender portal.
- You have access to incident cases in the Defender portal.
- You have the **Security Data Manage** Microsoft Defender unified RBAC permission.
- You have access to the alert you want to move and both the current and destination incident cases.

Incident case permissions and scoping follow the same permissions model as the legacy incident experience. You can move alerts only between incident cases included in your assigned data sources and scopes.

For more information, see [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

## Move an alert to another incident case

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Open the incident case that contains the alert you want to move.
5. Under **Artifacts**, select **Alerts**.
6. Select the alert you want to move.
7. Select **Move alert to another incident**.

    ![Screenshot showing a selected alert and the Move alerts to another incident action in the Microsoft Defender portal.](media/move-alert-to-another-incident-case/move-alert-to-another-incident-case-select-alert.png)
8. Search for and select the incident case that you want to move the alert to.

    ![Screenshot showing the Move alert to another incident pane in the Microsoft Defender portal.](media/move-alert-to-another-incident-case/move-alert-to-another-incident-case-pane.png)
9. In **Comment**, enter a comment that explains why you're moving the alert.
10. Under **Submit feedback to Microsoft for this correlation change**, provide feedback about the correlation change.

    You can select:

    - The correlation types that are incorrect.
    - The entities that are irrelevant to the current correlation.
11. Select **Save**.

The alert is moved to the selected incident case. The alert is removed from the original incident case and becomes part of the destination incident case investigation context.