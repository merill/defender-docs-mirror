---
layout: Conceptual
title: Microsoft Sentinel automation rules reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation-rule-reference
breadcrumb_path: breadcrumb/toc.json
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
description: This article displays the supported properties and entities in Microsoft Sentinel automation rules.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2024-09-02T00:00:00.0000000Z
locale: en-us
document_id: 00fd5a7a-77d7-0741-1f14-a8b682399ed4
document_version_independent_id: 38f5b520-113e-fd29-d130-a8de4e8b2da8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation-rule-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/automation-rule-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation-rule-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: cb187772-7565-3ef1-78d7-690f35a326a6
---

# Microsoft Sentinel automation rules reference | Microsoft Learn

This article contains reference information about the configuration of automation rules and the supported conditions and properties.

To learn more about automation rules, see [Automate threat response in Microsoft Sentinel with automation rules](automate-incident-handling-with-automation-rules).

For instructions on creating, managing, and using automation rules, see [Create and use Microsoft Sentinel automation rules to manage response](create-manage-use-automation-rules).

## Supported entity properties

The following entities and entity properties can be used as conditions for automation rules:

# [Property descriptions](#tab/descriptions)
This table shows the entity properties supported in the automation rules API. These are the entity properties whose values you can set as conditions for triggering an automation rule.

For the full list of supported properties, which includes incident properties, see [Automation rule property condition supported properties](/en-us/rest/api/securityinsights/automation-rules/get) in the [Automation rules API documentation](/en-us/rest/api/securityinsights/automation-rules).

| Name (in API) | Type | Description |
| --- | --- | --- |
| AccountAadTenantId | string | The account Microsoft Entra ID tenant ID |
| AccountAadUserId | string | The account Microsoft Entra ID user ID |
| AccountName | string | The account name |
| AccountNTDomain | string | The account NetBIOS domain name |
| AccountPUID | string | The account Microsoft Entra ID Passport User ID |
| AccountSid | string | The account security identifier |
| AccountObjectGuid | string | The account object unique identifier |
| AccountUPNSuffix | string | The account user principal name suffix |
| AzureResourceResourceId | string | The Azure resource ID |
| AzureResourceSubscriptionId | string | The Azure resource subscription ID |
| CloudApplicationAppId | string | The cloud application identifier |
| CloudApplicationAppName | string | The cloud application name |
| DNSDomainName | string | The dns record domain name |
| FileDirectory | string | The file directory full path |
| FileName | string | The file name without path |
| FileHashValue | string | The file hash value |
| HostAzureID | string | The host Azure resource ID |
| HostName | string | The host name without domain |
| HostNetBiosName | string | The host NetBIOS name |
| HostNTDomain | string | The host NT domain |
| HostOSVersion | string | The host operating system |
| IoTDeviceId | string | The IoT device ID |
| IoTDeviceName | string | The IoT device name |
| IoTDeviceType | string | The IoT device type |
| IoTDeviceVendor | string | The IoT device vendor |
| IoTDeviceModel | string | The IoT device model |
| IoTDeviceOperatingSystem | string | The IoT device operating system |
| IPAddress | string | The IP address |
| MailboxDisplayName | string | The mailbox display name |
| MailboxPrimaryAddress | string | The mailbox primary address |
| MailboxUPN | string | The mailbox user principal name |
| MailMessageDeliveryAction | string | The mail message delivery action |
| MailMessageDeliveryLocation | string | The mail message delivery location |
| MailMessageRecipient | string | The mail message recipient |
| MailMessageSenderIP | string | The mail message sender IP address |
| MailMessageSubject | string | The mail message subject |
| MailMessageP1Sender | string | The mail message P1 sender (delegated sender) |
| MailMessageP2Sender | string | The mail message P2 sender (original sender) |
| MalwareCategory | string | The malware category |
| MalwareName | string | The malware name |
| ProcessCommandLine | string | The process execution command line |
| ProcessId | string | The process ID |
| RegistryKey | string | The registry key path |
| RegistryValueData | string | The registry key value in string formatted representation |
| Url | string | The url |

# [Mapping to entities](#tab/mapping)
This table shows how the supported entity properties in the [Automation rules API](/en-us/rest/api/securityinsights/automation-rules) are displayed in the condition drop-down in the automation rules creation wizard. It also shows how those properties map to [entities and their identifiers](entities-reference) as defined in Microsoft Sentinel security alerts.

| Name in API | Name in UI drop-down | Entity: Identifier in V3 alert schema |
| --- | --- | --- |
| AccountAadTenantId | Account tenant ID | Account: AadTenantId |
| AccountAadUserId | Account AAD user ID | Account: AadUserId |
| AccountName | Account name | Account: Name |
| AccountNTDomain | Account NT domain | Account: NTDomain |
| AccountPUID | Account PUID | Account: PUID |
| AccountSid | Account SID | Account: Sid |
| AccountObjectGuid | Account object ID | Account: ObjectGuid |
| AccountUPNSuffix | Account UPN suffix | Account: UPNSuffix |
| AzureResourceResourceId | Azure resource ID | AzureResource: ResourceId |
| AzureResourceSubscriptionId | Azure resource subscription ID | AzureResource: SubscriptionId |
| CloudApplicationAppId | Cloud application ID | CloudApplication: AppId |
| CloudApplicationAppName | Cloud application name | CloudApplication: Name |
| DNSDomainName | DNS domain name | DNS: DomainName |
| FileDirectory | File directory | File: Directory |
| FileName | File name | File: Name |
| FileHashValue | File hash | FileHash: Value |
| HostAzureID | Host Azure ID | Host: AzureID |
| HostName | Host name | Host: HostName |
| HostNetBiosName | Host NetBIOS name | Host: NetBiosName |
| HostNTDomain | Host NT domain | Host: NTDomain |
| HostOSVersion | Host operating system | Host: OSVersion |
| IoTDeviceId | IoT device ID | IoTDevice: DeviceId |
| IoTDeviceName | IoT device name | IoTDevice: DeviceName |
| IoTDeviceType | IoT device type | IoTDevice: DeviceType |
| IoTDeviceVendor | IoT device vendor | IoTDevice: Manufacturer |
| IoTDeviceModel | IoT device model | IoTDevice: Model |
| IoTDeviceOperatingSystem | IoT device operating system | IoTDevice: OperatingSystem |
| IPAddress | IP address | IP: Address |
| MailboxDisplayName | Mailbox display name | Mailbox: DisplayName |
| MailboxPrimaryAddress | Mailbox primary address | Mailbox: MailboxPrimaryAddress |
| MailboxUPN | Mailbox UPN | Mailbox: Upn |
| MailMessageDeliveryAction | Mail message delivery action | MailMessage: DeliveryAction |
| MailMessageDeliveryLocation | Mail message delivery location | MailMessage: DeliveryLocation |
| MailMessageRecipient | Mail message recipient | MailMessage: Recipient |
| MailMessageSenderIP | Mail message sender IP | MailMessage: SenderIP |
| MailMessageSubject | Mail message subject | MailMessage: Subject |
| MailMessageP1Sender | Mail message P1 sender | MailMessage: P1Sender |
| MailMessageP2Sender | Mail message P2 sender | MailMessage: P2Sender |
| MalwareCategory | Malware category | Malware: Category |
| MalwareName | Malware name | Malware: Name |
| ProcessCommandLine | Process command line | Process: CommandLine |
| ProcessId | Process ID | Process: ProcessId |
| RegistryKey | Registry key | RegistryKey: Key |
| RegistryValueData | Registry value | RegistryValue: Value |
| Url | Url | Url: Url |

---