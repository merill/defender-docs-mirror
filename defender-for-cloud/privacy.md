---
layout: Conceptual
title: Manage user data - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/privacy
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to manage the user data in Microsoft Defender for Cloud. Managing user data includes the ability to access, delete, or export data.
ms.topic: concept-article
ms.date: 2025-05-18T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a9f6624b-7766-e70c-e6b0-fb5381a143ef
document_version_independent_id: 1c4611e5-358a-1a48-89f8-6a44e173ad71
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/privacy.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/privacy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: cf1ea1e0-d34c-09a5-bbca-2f41c949131c
---

# Manage user data - Microsoft Defender for Cloud | Microsoft Learn

This article provides information about how you can manage the user data in Microsoft Defender for Cloud. Managing user data includes the ability to access, delete, or export data.

Note

This article provides steps about how to delete personal data from the device or service and can be used to support your obligations under the GDPR. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

A Defender for Cloud user assigned the role of Reader, Owner, Contributor, or Account Administrator can access customer data within the tool. To learn more about the Account Administrator role, see [Built-in roles for Azure role-based access control](/en-us/azure/role-based-access-control/built-in-roles) to learn more about the Reader, Owner, and Contributor roles. See [Azure subscription administrators](/en-us/azure/cost-management-billing/manage/add-change-subscription-administrator).

## Search for and identify personal data

A Defender for Cloud user can view their personal data through the Azure portal. Defender for Cloud only stores security contact details such as email addresses and phone numbers. For more information, see [Provide security contact details in Microsoft Defender for Cloud](configure-email-notifications).

In the Azure portal, a user can view allowed IP configurations using Defender for Cloud's just-in-time VM access feature. For more information, see [Manage virtual machine access using just-in-time](just-in-time-access-usage).

In the Azure portal, a user can view security alerts provided by Defender for Cloud including IP addresses and attacker details. For more information, see [Managing and responding to security alerts in Microsoft Defender for Cloud](manage-respond-alerts).

## Classify personal data

You don't need to classify personal data found in Defender for Cloud's security contact feature. The data saved is an email address (or multiple email addresses) and a phone number. [Contact data](configure-email-notifications) is validated by Defender for Cloud.

You don't need to classify the IP addresses and port numbers saved by Defender for Cloud's [just-in-time](just-in-time-access-usage) feature.

Only a user assigned the role of Administrator can classify personal data by [viewing alerts](manage-respond-alerts) in Defender for Cloud.

## Secure and control access to personal data

A Defender for Cloud user assigned the role of Reader, Owner, Contributor, or Account Administrator can access [security contact data](configure-email-notifications).

A Defender for Cloud user assigned the role of Reader, Owner, Contributor, or Account Administrator can access their [just-in-time](just-in-time-access-usage) policies.

A Defender for Cloud user assigned the role of Reader, Owner, Contributor, or Account Administrator can view their [alerts](manage-respond-alerts).

## Update personal data

A Defender for Cloud user assigned the role of Owner, Contributor, or Account Administrator can update [security contact data](configure-email-notifications) via the Azure portal.

A Defender for Cloud user assigned the role of Owner, Contributor, or Account Administrator can update their [just-in-time policies](just-in-time-access-usage).

An Account Administrator can't edit alert incidents. An [alert incident](manage-respond-alerts) is considered security data and is read only.

## Delete personal data

A Defender for Cloud user assigned the role of Owner, Contributor, or Account Administrator can delete [security contact data](configure-email-notifications) via the Azure portal.

A Defender for Cloud user assigned the role of Owner, Contributor, or Account Administrator can delete the [just-in-time policies](just-in-time-access-usage) via the Azure portal.

A Defender for Cloud user can't delete alert incidents. For security reasons, an [alert incident](manage-respond-alerts) is considered read-only data.

## Export personal data

A Defender for Cloud user assigned the role of Reader, Owner, Contributor, or Account Administrator can export [security contact data](configure-email-notifications) by:

- Copying from the Azure portal
- Executing the Azure REST API call, GET HTTP:

    ```HTTP
    GET https://<endpoint>/subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts?api-version={api-version}
    ```

A Defender for Cloud user assigned the role of Account Administrator can export the [just-in-time policies](just-in-time-access-usage) containing the IP addresses by:

- Copying from the Azure portal
- Executing the Azure REST API call, GET HTTP:

    ```HTTP
    GET https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Security/locations/{location}/jitNetworkAccessPolicies/default?api-version={api-version}
    ```

An Account Administrator can export the alert details by:

- Copying from the Azure portal
- Executing the Azure REST API call, GET HTTP:

    ```HTTP
    GET https://<endpoint>/subscriptions/{subscriptionId}/providers/microsoft.Security/alerts?api-version={api-version}
    ```

For more information, see [Get Security Alerts (GET Collection)](/en-us/previous-versions/azure/reference/mt704050%28v=azure.100%29).

## Restrict the use of personal data for profiling or marketing without consent

A Defender for Cloud user can choose to opt out by deleting their [security contact data](configure-email-notifications).

[Just-in-time data](just-in-time-access-usage) is considered non-identifiable data and is retained for 30 days.

[Alert data](manage-respond-alerts) is considered security data and is retained for two years.

## Auditing and reporting

Audit logs of security contact, just-in-time, and alert updates are maintained in [Azure Activity Logs](/en-us/azure/azure-monitor/essentials/platform-logs-overview).

## Respond to data subject export requests for Defender for APIs

The right of data portability allows data subjects to request a copy of their personal data in a structured, common, electronic format that can be transmitted to another data controller.

### Manage export and view requests

You can manage requests to export customer or user data.

#### Export customer data (Tenant administrator only)

As a tenant administrator, you have the ability to export customer data.

**To export customer data**:

1. Send an email to `D4APIS_DSRRequests@microsoft.com` that specifies the customer’s email address in the request.
2. The Defender for APIs team will respond with an email to the registered tenant's administrator email address that will ask for confirmation to export the data.
3. Acknowledge the confirmation to export the data for the requested customer. The exported data will be sent to the tenant administrator's email address.