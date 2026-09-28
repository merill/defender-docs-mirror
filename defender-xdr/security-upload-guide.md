---
layout: Conceptual
title: Customize Copilot for your organization - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-upload-guide
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to upload your organization's specific guidelines to Microsoft Security Copilot to enhance guided response recommendations.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: install-set-up-deploy
ms.date: 2025-11-18T00:00:00.0000000Z
locale: en-us
document_id: 6bc2c197-21eb-9551-cf96-df4fa5328e5c
document_version_independent_id: 6bc2c197-21eb-9551-cf96-df4fa5328e5c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-upload-guide.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-upload-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-upload-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 84d5d202-9983-3807-b9db-017461a2ccaf
---

# Customize Copilot for your organization - Microsoft Defender XDR | Microsoft Learn

[Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) in the Microsoft Defender portal provides guided responses to support the response team in resolving incidents. Copilot in Defender uses AI and machine learning to contextualize an incident and learn from previous investigations to generate appropriate response actions.

This guide outlines how to upload your organization's specific guidelines to Microsoft Security Copilot to improve the guided response recommendations.

## Prerequisites

- You must be at least a security administrator to upload, approve, or delete files. Security operators can review the guidebooks but not manage them.
- Your organization-specific guidelines should be in a supported format (PDF, DOCX, TXT) and shouldn't exceed the maximum file size limit of 3 MB.

## Steps to customize Copilot's guided response using your organization's guidebook

Upload your guidebook from Copilot settings. You can get there in one of two ways:

- From the Microsoft Defender portal, select **System** &gt; **Settings** &gt; **Copilot in Defender** &gt; **Custom guidebooks**.

    ![Screenshot of adding custom guidebooks from settings.](media/security-upload-guide/add-from-settings.png)
- From the Copilot tasks pane inside an incident, go to **Create tasks from your own guidebook** and select **Open Copilot settings**.

    ![Screenshot of opening Copilot settings from the tasks pane.](media/security-upload-guide/add-from-incident.png)

Then follow these steps:

1. Select **Add new guidebook**.
2. Select **Upload file**.
3. Browse to the file location, choose the file, and then select **Generate**.
4. After the file is uploaded, go to the **Pending review** tab.

    ![Screenshot of the pending review tab for uploaded guidebooks.](media/security-upload-guide/pending-review.png)
5. The pending review tab shows the new recommendations based on the uploaded guidebook. Review the file to ensure it meets your organization's standards. Select the guidebook name and review the suggested generated tasks.
6. If the guidebook meets your standards, select **Approve and activate** to make it available for use in guided responses. If it doesn't meet your standards, select **Delete** to remove it.

    ![Screenshot of the approve and activate button for uploaded guidebooks.](media/security-upload-guide/approve-guidebook.png)
7. Make sure the guidebook appears as active in the **Guidebooks** tab. To deactivate it later, select the guidebook and choose **Deactivate**.

    ![Screenshot of the active guidebooks tab.](media/security-upload-guide/active-guidebooks.png)

Copilot will prioritize your organization's custom guidebooks over the default ones provided by Microsoft. If multiple guidebooks are relevant, Copilot will use the one that best matches the incident context.

![Screenshot of suggested responses based on the custom guidebooks.](media/security-upload-guide/custom-responses.png)

You have the opportunity to provide feedback on the effectiveness of the guided responses generated from your organization's guidebooks. This feedback helps improve future recommendations.

![Screenshot of the feedback window for guided responses.](media/security-upload-guide/feedback.png)

## Best practices for creating effective guidebooks

For examples of Microsoft's own incident response playbooks, see [Incident response playbooks](/en-us/security/operations/incident-response-playbooks).

To create a guidebook for your organization, start with the [SOP template - Compromised identity](sop-documentation-template).

When creating your organization's guidebooks, keep in mind that the guidebook can only read text. Avoid using images, graphs, or complex formatting that may hinder text extraction.