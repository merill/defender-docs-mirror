---
layout: Conceptual
title: Built-in & custom alerts list - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-security-alerts
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
ms.subservice: device-builders
description: Learn about security alerts and recommended remediation using Defender for IoT Hub's features and service.
ms.topic: reference
ms.date: 2023-01-01T00:00:00.0000000Z
locale: en-us
document_id: ea9f317b-a00a-34fe-9d93-e9fd6b8b46a6
document_version_independent_id: 8fa0309e-08b0-a660-791d-9beb14c891cf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-security-alerts.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-security-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-security-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 872b96a3-a1ea-ebcc-ad97-b8840abada18
---

# Built-in & custom alerts list - Microsoft Defender for IoT | Microsoft Learn

Defender for IoT continuously analyzes your IoT solution using advanced analytics and threat intelligence to alert you to malicious activity. In addition, you can create custom alerts based on your knowledge of expected device behavior. An alert acts as an indicator of potential compromise, and should be investigated and remediated.

In this article, you will find a list of built-in alerts, which can be triggered on your IoT Hub. In addition to built-in alerts, Defender for IoT allows you to define custom alerts based on expected IoT Hub and/or device behavior. For more information, see [customizable alerts](concept-customizable-security-alerts).

## Built-in alerts for IoT Hub

### Medium severity

| Name | Severity | Data Source | Description | Suggested remediation | AlertType |
| --- | --- | --- | --- | --- | --- |
| New certificate added to an IoT Hub | Medium | IoT Hub | A certificate was added to an IoT Hub. If this action was made by an unauthorized party, it may indicate malicious activity. | 1. Make sure the certificate was added by an authorized party.  2. If it was not added by an authorized party, remove the certificate and escalate the alert to the organizational security team. | IoT\_CertificateSuccessfullyAddedToHub |
| Certificate deleted from an IoT Hub | Medium | IoT Hub | A certificate was deleted from an IoT Hub. If this action was made by an unauthorized party, it may indicate a malicious activity. | 1. Make sure the certificate was removed by an authorized party.  2. If the certificate was not removed by an authorized party, add the certificate back, and escalate the alert to the organizational security team. | IoT\_CertificateSuccessfullyDeletedFromHub |
| Unsuccessful attempt detected to add a certificate to an IoT Hub | Medium | IoT Hub | There was an unsuccessful attempt to add a certificate to an IoT Hub. If this action was made by an unauthorized party, it may indicate malicious activity. | Make sure permissions to change certificates are only granted to authorized parties. | Hub\_CertificateFailedToBeAddedToHub |
| Unsuccessful attempt detected to delete a certificate from an IoT Hub | Medium | IoT Hub | There was an unsuccessful attempt to delete a certificate from an IoT Hub. If this action was made by an unauthorized party, it may indicate malicious activity. | Make sure permissions to change certificates are only granted to an authorized party. | IoT.Hub\_CertificateFailedToBeDeletedFromHub |
| x.509 device certificate thumbprint mismatch | Medium | IoT Hub | x.509 device certificate thumbprint did not match configuration. | Review alerts on the devices. No further action required. | IoT\_Cert\_Print\_Mismatch |
| x.509 certificate expired | Medium | IoT Hub | X.509 device certificate has expired. | This could be a legitimate device with an expired certificate or an attempt to impersonate a legitimate device. If the legitimate device is currently communicating correctly this is likely an impersonation attempt. | IoT\_Cert\_Expired |

### Low severity

| Name | Severity | Data Source | Description | Suggested remediation | AlertType |
| --- | --- | --- | --- | --- | --- |
| Attempt to add or edit a diagnostic setting of an IoT Hub detected | Low | IoT Hub | Attempt to add or edit the diagnostic settings of an IoT Hub has been detected. Diagnostic settings enable you to recreate activity trails for investigation purposes when a security incident occurs or your network is compromised. If this action was not made by an authorized party, it may indicate malicious activity. | 1. Make sure the certificate was removed by an authorized party.  2. If the certificate was not removed by an authorized party, add the certificate back and escalate the alert to your information security team. | IoT\_DiagnosticSettingAddedOrEditedOnHub |
| Attempt to delete a diagnostic setting from an IoT Hub detected | Low | IoT Hub | Attempt to add or edit the diagnostic settings of an IoT Hub has been detected. Diagnostic settings enable you to recreate activity trails for investigation purposes when a security incident occurs or your network is compromised. If this action was not made by an authorized party, it may indicate malicious activity. | Make sure permissions to change diagnostics settings are granted only to an authorized party. | IoT\_DiagnosticSettingDeletedFromHub |
| Expired SAS Token | Low | IoT Hub | Expired SAS token used by a device | May be a legitimate device with an expired token, or an attempt to impersonate a legitimate device. If the legitimate device is currently communicating correctly, this is likely an impersonation attempt. | IoT\_Expired\_SAS\_Token |
| Invalid SAS token signature | Low | IoT Hub | A SAS token used by a device has an invalid signature. The signature does not match either the primary or secondary key. | Review the alerts on the devices. No further action required. | IoT\_Invalid\_SAS\_Token |