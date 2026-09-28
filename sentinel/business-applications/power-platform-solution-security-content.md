---
layout: Conceptual
title: Security content reference for Microsoft Power Platform and Microsoft Dynamics 365 Customer Engagement and Microsoft Dynamics 365 Customer Engagement | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/business-applications/power-platform-solution-security-content
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
description: Learn about the built-in security content provided by the Microsoft Sentinel solution for Power Platform.
ms.author: monaberdugo
author: mberdugo
ms.topic: article
ms.date: 2025-12-12T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: f6926a7b-24e2-6de4-c0ab-454c7561b076
document_version_independent_id: daa21cd3-c5c6-9b15-ff78-a8e0af4896f5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/business-applications/power-platform-solution-security-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/business-applications/power-platform-solution-security-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/business-applications/power-platform-solution-security-content.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0ceb3227-2ff7-4d97-8e75-3d7b9ccc937a
- https://authoring-docs-microsoft.poolparty.biz/devrel/e6f942e8-55a7-4c86-b8e3-7456508ea850
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/4d680e1a-c470-4772-a236-5c714bd09be0
- https://authoring-docs-microsoft.poolparty.biz/devrel/f1834696-48d6-470d-966b-6ee418881596
platformId: a7634d1e-3f5e-4e38-3702-03055e110b4a
---

# Security content reference for Microsoft Power Platform and Microsoft Dynamics 365 Customer Engagement and Microsoft Dynamics 365 Customer Engagement | Microsoft Learn

This article details the security content available for the Microsoft Sentinel solution for Power Platform. For more information about this solution, see [Microsoft Sentinel solution for Microsoft Power Platform and Microsoft Dynamics 365 Customer Engagement overview](power-platform-solution-overview).

## Built-in analytics rules

The following analytic rules are included when you install the solution for Power Platform. The data sources listed include the data connector name and table in Log Analytics.

### Dataverse rules

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| Dataverse - Anomalous application user activity | Identifies anomalies in activity patterns of Dataverse application (non-interactive) users, based on activity that falls outside the normal pattern of use. | Unusual S2S user activity in Dynamics 365 / Dataverse.**Data sources**:- Dataverse`DataverseActivity` | CredentialAccess, Execution, Persistence |
| Dataverse - Audit log data deletion | Identifies audit log data deletion activity in Dataverse. | Deletion of Dataverse audit logs.**Data sources**:- Dataverse`DataverseActivity` | DefenseEvasion |
| Dataverse - Audit logging disabled | Identifies a change in the system audit configuration whereby audit logging is turned off. | Global or entity level auditing disabled.**Data sources**:- Dataverse`DataverseActivity` | DefenseEvasion |
| Dataverse - Bulk record ownership re-assignment or sharing | Identifies changes in individual record ownership, including: - Record sharing with other users/teams - Ownership reassignments that exceed a predefined threshold. | Many record ownership and record sharing events generated within the detection window.**Data sources**:- Dataverse`DataverseActivity` | PrivilegeEscalation |
| Dataverse - Executable uploaded to SharePoint document management site | Identifies executable files and scripts that are uploaded to SharePoint sites used for Dynamics document management, circumventing native file extension restrictions in Dataverse. | Upload of executable files in Dataverse document management.**Data sources**:- Office365`OfficeActivity (SharePoint)` | Execution, Persistence |
| Dataverse - Export activity from terminated or notified employee | Identifies Dataverse export activity triggered by terminate employees, or employees about to leave the organization. | Data export events associated with users on the **TerminatedEmployees** watchlist template. **Data sources**:- Dataverse`DataverseActivity` | Exfiltration |
| Dataverse - Guest user exfiltration following Power Platform defense impairment | Identifies a chain of events starting with disabling Power Platform's tenant isolation and removing an environment's access security group. These events are correlated with Dataverse exfiltration alerts associated with the impacted environment and recently created Microsoft Entra guest users.Activate other Dataverse analytics rules with the **Exfiltration** MITRE tactic before enabling this rule. | As a recently created guest user, trigger Dataverse exfiltration alerts after the Power Platform security controls are disabled.**Data sources:**- PowerPlatformAdmin`PowerPlatformAdminActivity`- Dataverse`DataverseActivity` | Defense Evasion |
| Dataverse - Hierarchy security manipulation | Identifies suspicious behaviors in hierarchy security. | Changes to security properties including: - Hierarchy security disabled. - User assigns themselves as a manager. - User assigns themselves to a monitored position (set in KQL).**Data sources**:- Dataverse`DataverseActivity` | PrivilegeEscalation |
| Dataverse - Honeypot instance activity | Identifies activities in a predefined Honeypot Dataverse instance. Alerts either when either a sign-in to the Honeypot is detected or when monitored Dataverse tables in the Honeypot are accessed. | Sign-in and access data in a designated Honeypot Dataverse instance in Power Platform with auditing enabled.**Data sources**:- Dataverse`DataverseActivity` | Discovery, Exfiltration |
| Dataverse - Login by a sensitive privileged user | Identifies Dataverse and Dynamics 365 sign-ins by sensitive users. | Sign-in by users added on the **VIPUsers** watchlist based on tags set within KQL.**Data sources**:- Dataverse`DataverseActivity` | InitialAccess, CredentialAccess, PrivilegeEscalation |
| Dataverse - Login from IP in the block list | Identifies Dataverse sign-in activity from IPv4 addresses that are on a predefined block list. | Sign-in by a user with an IP address that is part of a blocked network range. Blocked network ranges are maintained in the **NetworkAddresses** watchlist template.**Data sources**:- Dataverse`DataverseActivity` | InitialAccess |
| Dataverse - Login from IP not in the allow list | Identifies sign-ins from IPv4 addresses that don't match IPv4 subnets maintained on an allow list. | Sign-in by a user with an IP address that isn't part of an allowed network range. Blocked network ranges are maintained in the **NetworkAddresses** watchlist template.**Data sources**:- Dataverse`DataverseActivity` | InitialAccess |
| Dataverse - Malware found in SharePoint document management site | Identifies malware uploaded via Dynamics 365 document management or directly in SharePoint, affecting Dataverse associated SharePoint sites. | Malicious file in SharePoint site linked to Dataverse.**Data sources**:- Dataverse`DataverseActivity`- Office365`OfficeActivity (SharePoint)` | Execution |
| Dataverse - Mass deletion of records | Identifies large scale record deletion operations based on a predefined threshold. Also detects scheduled bulk deletion jobs. | Deletion of records exceeding threshold defined in KQL.**Data sources**:- Dataverse`DataverseActivity` | Impact |
| Dataverse - Mass download from SharePoint document management | Identifies mass download in the last hour of files from SharePoint sites configured for document management in Dynamics 365. | Mass download exceeding threshold defined in KQL. This analytics rule uses the **MSBizApps-Configuration** watchlist to identify SharePoint sites used for Document Management.**Data sources**:- Office365`OfficeActivity (SharePoint)` | Exfiltration |
| Dataverse - Mass export of records to Excel | Identifies users exporting a large number of records from Dynamics 365 to Excel, where the number of records exported is significantly more than any other recent activity by that user. Large exports from users with no recent activity are identified using a predefined threshold. | Export many records from Dataverse to Excel.**Data sources:**- Dataverse`DataverseActivity` | Exfiltration |
| Dataverse - Mass record updates | Detects mass record update changes in Dataverse and Dynamics 365, exceeding a predefined threshold. | Mass update of records exceeds threshold defined in KQL.**Data sources**:- Dataverse`DataverseActivity` | Impact |
| Dataverse - New Dataverse application user activity type | Identifies new or previously unseen activity types associated with a Dataverse application (non-interactive) user. | New S2S user activity types.**Data sources**:- Dataverse`DataverseActivity` | CredentialAccess, Execution, PrivilegeEscalation |
| Dataverse - New non-interactive identity granted access | Identifies API level access grants, either via the delegated permissions of a Microsoft Entra application or by direct assignment within Dataverse as an application user. | Dataverse permissions added to non-interactive user. **Data sources**:- Dataverse`DataverseActivity`,- AzureActiveDirectory`AuditLogs` | Persistence, LateralMovement, PrivilegeEscalation |
| Dataverse - New sign-in from an unauthorized domain | Identifies Dataverse sign-in activity originating from users with UPN suffixes that haven't been seen previously in the last 14 days, and aren't present on a predefined list of authorized domains. Common internal Power Platform system users are excluded by default. | Sign-in by external user from an unauthorized domain suffix.**Data sources**:- Dataverse`DataverseActivity` | InitialAccess |
| Dataverse - New user agent type that was not used before | Identifies users accessing Dataverse from a User Agent that hasn't been seen in any Dataverse instance in the last 14 days. | Activity in Dataverse from a new user-agent.**Data sources**:- Dataverse`DataverseActivity` | InitialAccess, DefenseEvasion |
| Dataverse - New user agent type that was not used with Office 365 | Identifies users accessing Dynamics with a User Agent that hasn't been seen in any Office 365 workloads in the last 14 days. | Activity in Dataverse from a new user-agent.**Data sources**:- Dataverse`DataverseActivity` | InitialAccess |
| Dataverse - Organization settings modified | Identifies changes made at the organization level in the Dataverse environment. | Organization level property modified in Dataverse.**Data sources**:- Dataverse`DataverseActivity` | Persistence |
| Dataverse - Removal of blocked file extensions | Identifies modifications to an environment's blocked file extensions and extracts the removed extension. | Removal of blocked file extensions in Dataverse properties.**Data sources**:- Dataverse`DataverseActivity` | DefenseEvasion |
| Dataverse - SharePoint document management site added or updated | Identifies modifications of the SharePoint document management integration. Document management allows storage of data located externally to Dataverse. Combine this analytics rule with the **Dataverse: Add SharePoint sites to watchlist** playbook to automatically update the **Dataverse-SharePointSites** watchlist. This watchlist can be used to correlate events between Dataverse and SharePoint when using the Office 365 data connector. | SharePoint site mapping added in Document Management.**Data sources**:- Dataverse`DataverseActivity` | Exfiltration |
| Dataverse - Suspicious security role modifications | Identifies an unusual pattern of events whereby a new role is created, followed by the creator adding members to the role and later removing the member or deleting the role after a short time period. | Changes in security roles and role assignments.**Data sources**:- Dataverse`DataverseActivity` | PrivilegeEscalation |
| Dataverse - Suspicious use of TDS endpoint | Identifies Dataverse TDS (Tabular Data Stream) protocol-based queries, where the source user or IP address has recent security alerts and the TDS protocol hasn't been used previously in the target environment. | Sudden use of the TDS endpoint in correlation with security alerts.**Data sources**:- Dataverse`DataverseActivity`- AzureActiveDirectoryIdentityProtection`SecurityAlert` | Exfiltration, InitialAccess |
| Dataverse - Suspicious use of Web API | Identifies sign-ins across multiple Dataverse environments that breach a predefined threshold and originate from a user with an IP address that was used to sign into a well-known Microsoft Entra app registration. | Sign-in using WebAPI across multiple environments using a well known public application ID.**Data sources**:- Dataverse`DataverseActivity`- AzureActiveDirectory`SigninLogs` | Execution, Exfiltration, Reconnaissance, Discovery |
| Dataverse - TI map IP to DataverseActivity | Identifies a match in DataverseActivity from any IP IOC from Microsoft Sentinel Threat Intelligence. | Dataverse activity with IP matching IOC.**Data sources**:- Dataverse`DataverseActivity` ThreatIntelligence`ThreatIntelIndicators` | InitialAccess, LateralMovement, Discovery |
| Dataverse - TI map URL to DataverseActivity | Identifies a match in DataverseActivity from any URL IOC from Microsoft Sentinel Threat Intelligence. | Dataverse activity with URL matching IOC.**Data sources**:- Dataverse`DataverseActivity` ThreatIntelligence`ThreatIntelIndicators` | InitialAccess, Execution, Persistence |
| Dataverse - Terminated employee exfiltration over email | Identifies Dataverse exfiltration via email by terminated employees. | Emails sent to untrusted recipient domains following security alerts correlated with users on the **TerminatedEmployees** watchlist.**Data sources**:MicrosoftThreatProtection`EmailEvents``IdentityInfo`- AzureActiveDirectoryIdentityProtection, IdentityInfo`SecurityAlert` | Exfiltration |
| Dataverse - Terminated employee exfiltration to USB drive | Identifies files downloaded from Dataverse by departing or terminated employees, and are copied to USB mounted drives. | Files originating from Dataverse copied to USB by a user on the **TerminatedEmployees** watchlist.**Data sources**:- Dataverse`DataverseActivity`- MicrosoftThreatProtection`DeviceInfo``DeviceEvents``DeviceFileEvents` | Exfiltration |
| Dataverse - Unusual sign-in following disabled IP address-based cookie binding protection | Identifies previously unseen IP and user agents in a Dataverse instance following disabling of cookie binding protection. For more information, see [Safeguarding Dataverse sessions with IP cookie binding](/en-us/power-platform/admin/block-cookie-replay-attack). | New sign-in activity.**Data sources**:- Dataverse`DataverseActivity` | DefenseEvasion |
| Dataverse - User bulk retrieval outside normal activity | Identifies users retrieving significantly more records from Dataverse than they have in the past two weeks. | User retrieves many records from Dataverse and including KQL defined threshold.**Data sources:**- Dataverse`DataverseActivity` | Exfiltration |

### Power Apps rules

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| Power Apps - App activity from unauthorized geo | Identifies Power Apps activity from geographic regions in a predefined list of unauthorized geographic regions.  This detection gets the list of ISO 3166-1 alpha-2 country codes from [ISO Online Browsing Platform (OBP)](https://www.iso.org/obp/ui).This detection uses logs ingested from Microsoft Entra ID and requires that you also enable the Microsoft Entra ID data connector. | Run an activity in a Power App from a geographic region that's on the unauthorized country code list.**Data sources**: - Microsoft Power Platform Admin Activity`PowerPlatformAdminActivity`- Microsoft Entra ID`SigninLogs` | Initial access |
| Power Apps - Multiple apps deleted | Identifies mass delete activity where multiple Power Apps are deleted, matching a predefined threshold of total apps deleted or app deleted events across multiple Power Platform environments. | Delete many Power Apps from the Power Platform admin center. **Data sources**:- Microsoft Power Platform Admin Activity`PowerPlatformAdminActivity` | Impact |
| Power Apps - Multiple users accessing a malicious link after launching new app | Identifies a chain of events when a new Power App is created and is followed by these events:- Multiple users launch the app within the detection window.- Multiple users open the same malicious URL.This detection cross correlates Power Apps execution logs with malicious URL selection events from either of the following sources:- The Microsoft 365 Defender data connector or - Malicious URL indicators of compromise (IOC) in Microsoft Sentinel Threat Intelligence with the Advanced Security Information Model (ASIM) web session normalization parser.This detection gets the distinct number of users who launch or select the malicious link by creating a query. | Multiple users launch a new PowerApp and open a known malicious URL from the app.**Data sources**:- Microsoft Power Platform Admin Activity`PowerPlatformAdminActivity`- Threat Intelligence `ThreatIntelIndicators`- Microsoft Defender XDR`UrlClickEvents` | Initial access |
| Power Apps - Bulk sharing of Power Apps to newly created guest users | Identifies unusual bulk sharing of Power Apps to newly created Microsoft Entra guest users. Unusual bulk sharing is based on a predefined threshold in the query. | Share an app with multiple external users.**Data sources:**- Microsoft Power Platform Admin Activity`PowerPlatformAdminActivity`- Microsoft Entra ID`AuditLogs` | Resource Development,Initial Access,Lateral Movement |

### Power Automate rules

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| Power Automate - Departing employee flow activity | Identifies instances where an employee who has been notified or is already terminated, and is on the **Terminated Employees** watchlist, creates or modifies a Power Automate flow. | User defined in the **TerminatedEmployees** watchlist creates or updates a Power Automate flow.**Data sources**:Microsoft Power Automate`PowerAutomateActivity`**TerminatedEmployees** watchlist | Exfiltration, impact |
| Power Automate - Unusual bulk deletion of flow resources | Identifies bulk deletion of Power Automate flows that exceed a predefined threshold defined in the query, and deviate from activity patterns observed in the last 14 days. | Bulk deletion of Power Automate flows.**Data sources:**- PowerAutomate`PowerAutomateActivity` | Impact, Defense Evasion |

### Power Platform rules

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| Power Platform - Connector added to a sensitive environment | Identifies the creation of new API connectors within Power Platform, specifically targeting a predefined list of sensitive environments. | Add a new Power Platform connector in a sensitive Power Platform environment.**Data sources**:- Microsoft Power Platform Admin Activity`PowerPlatformAdminActivity` | Execution, Exfiltration |
| Power Platform - DLP policy updated or removed | Identifies changes to the data loss prevention policy, specifically policies that are updated or removed. | Update or remove a Power Platform data loss prevention policy in Power Platform environment.**Data sources**:Microsoft Power Platform Admin Activity`PowerPlatformAdminActivity` | Defense Evasion |
| Power Platform - Possibly compromised user accesses Power Platform services | Identifies user accounts flagged at risk in Microsoft Entra ID Protection and correlates these users with sign-in activity in Power Platform, including Power Apps, Power Automate, and Power Platform Admin Center. | User with risk signals accesses Power Platform portals.**Data sources:**- Microsoft Entra ID`SigninLogs` | Initial Access, Lateral Movement |
| Power Platform - Account added to privileged Microsoft Entra roles | Identifies changes to the following privileged directory roles that affect Power Platform:- Dynamics 365 Admins- Power Platform Admins- Fabric Admins | **Data sources**:AzureActiveDirectory`AuditLogs` | PrivilegeEscalation |

## Hunting queries

The solution includes hunting queries that can be used by analysts to proactively hunt malicious or suspicious activity in the Dynamics 365 and Power Platform environments.

| Rule name | Description | Data Source | Tactics |
| --- | --- | --- | --- |
| Dataverse - Activity after Microsoft Entra alerts | This hunting query looks for users conducting Dataverse/Dynamics 365 activity shortly after a Microsoft Entra ID Protection alert for that user. The query only looks for users not seen before or conducting Dynamics activity not previously seen. | - Dataverse`DataverseActivity`- AzureActiveDirectoryIdentityProtection`SecurityAlert` | InitialAccess |
| Dataverse - Activity after failed logons | This hunting query looks for users conducting Dataverse/Dynamics 365 activity shortly after many failed sign-ins. Use this query to hunt for potential post brute force activity. Adjust the threshold figure based on the false positive rate. | - Dataverse`DataverseActivity`- AzureActiveDirectory`SigninLogs` | InitialAccess |
| Dataverse - Cross-environment data export activity | Searches for data export activity across a predetermined number of Dataverse instances. Data export activity across multiple environments could indicate suspicious activity as users typically work on a few environments only. | - Dataverse`DataverseActivity` | Exfiltration, Collection |
| Dataverse - Dataverse export copied to USB devices | Uses data from Microsoft Defender XDR to detect files downloaded from a Dataverse instance and copied to USB drive. | - Dataverse`DataverseActivity`- MicrosoftThreatProtection`DeviceInfo``DeviceFileEvents``DeviceEvents` | Exfiltration |
| Dataverse - Generic client app used to access production environments | Detects the use of the built-in "Dynamics 365 Example Application" to access production environments. This generic app can’t be restricted by Microsoft Entra ID authorization controls and can be abused to gain unauthorized access via Web API. | - Dataverse`DataverseActivity`- AzureActiveDirectory`SigninLogs` | Execution |
| Dataverse - Identity management activity outside of privileged directory role membership | Detects identity administration events in Dataverse/Dynamics 365 made by accounts whthatich aren't members of the following privileged directory roles: Dynamics 365 Admins, Power Platform Admins or Global Admins | - Dataverse`DataverseActivity`- UEBA`IdentityInfo` | PrivilegeEscalation |
| Dataverse - Identity management changes without MFA | Used to show privileged identity administration operations in Dataverse made by accounts that signed in without using MFA. | - Dataverse`DataverseActivity`- AzureActiveDirectory`SigninLogs, DataverseActivity` | InitialAccess |
| Power Apps - Anomalous bulk sharing of Power App to newly created guest users | The query detects anomalous attempts to perform bulk sharing of a Power App to newly created guest users. | **Data sources**:PowerPlatformAdmin, AzureActiveDirectory`AuditLogs, PowerPlatformAdminActivity` | InitialAccess, LateralMovement, ResourceDevelopment |

## Playbooks

This solution contains playbooks which can be used to automate security response to incidents and alerts in Microsoft Sentinel.

| Playbook name | Description |
| --- | --- |
| Security workflow: alert verification with workload owners | This playbook can reduce burden on the SOC by offloading alert verification to IT admins for specific analytics rules. It is triggered when a Microsoft Sentinel alert is generated, creates a message (and associated notification email) in the workload owner's Microsoft Teams channel containing details of the alert. If the workload owner responds that the activity is not authorized, the alert will be converted to an incident in Microsoft Sentinel for the SOC to handle. |
| Dataverse: Send notification to manager | This playbook can be triggered when a Microsoft Sentinel incident is raised and will automatically send an email notification to the manager of the affected user entities. The Playbook can be configured to send either to the Dynamics 365 manager, or using the manager in Office 365. |
| Dataverse: Add user to block list (incident trigger) | This playbook can be triggered when a Microsoft Sentinel incident is raised and will automatically add affected user entities to a pre-defined Microsoft Entra group, resulting in blocked access. The Microsoft Entra group is used with Conditional Access to block sign-in to the Dataverse. |
| Dataverse: Add user to block list using Outlook approval workflow | This playbook can be triggered when a Microsoft Sentinel incident is raised and will automatically add affected user entities to a pre-defined Microsoft Entra group, using an Outlook based approval workflow, resulting in blocked access. The Microsoft Entra group is used with Conditional Access to block sign-in to the Dataverse. |
| Dataverse: Add user to block list using Teams approval workflow | This playbook can be triggered when a Microsoft Sentinel incident is raised and will automatically add affected user entities to a pre-defined Microsoft Entra group, using a Teams adaptive card approval workflow, resulting in blocked access. The Microsoft Entra group is used with Conditional Access to block sign-in to the Dataverse. |
| Dataverse: Add user to block list (alert trigger) | This playbook can be triggered on-demand when a Microsoft Sentinel alert is raised, allowing the analyst to add affected user entities to a pre-defined Microsoft Entra group, resulting in blocked access. The Microsoft Entra group is used with Conditional Access to block sign-in to the Dataverse. |
| Dataverse: Remove user from block list | This playbook can be triggered on-demand when a Microsoft Sentinel alert is raised, allowing the analyst to remove affected user entities from a pre-defined Microsoft Entra group used to block access. The Microsoft Entra group is used with Conditional Access to block sign-in to the Dataverse. |
| Dataverse: Add SharePoint sites to watchlist | This playbook is used to add new or updated SharePoint document management sites into the configuration watchlist. When combined with a scheduled analytics rule monitoring the Dataverse activity log, this Playbook will trigger when a new SharePoint document management site mapping is added. The site will be added to a watchlist to extend monitoring coverage. |

## Workbooks

Microsoft Sentinel workbooks are customizable, interactive dashboards within Microsoft Sentinel that facilitate analysts' efficient visualization, analysis, and investigation of security data. This solution includes the **Dynamics 365 Activity** workbook, which presents a visual representation of activity in Microsoft Dynamics 365 Customer Engagement / Dataverse, including record retrieval statistics and an anomaly chart.

## Watchlists

This solution includes the **MSBizApps-Configuration** watchlist, and requires users to create additional watchlists based on the following watchlist templates:

- **VIPUsers**
- **NetworkAddresses**
- **TerminatedEmployees**

For more information, see [Watchlists in Microsoft Sentinel](../watchlists) and [Create watchlists](../watchlists-create#upload-a-watchlist-created-from-a-template-preview).

## Built-in parsers

The solution includes parsers that are used to access data from the raw data tables. Parsers ensure that the correct data is returned with a consistent schema. We recommend that you use the parsers instead of directly querying the watchlists.

| Parser | Data returned | Table queried |
| --- | --- | --- |
| **MSBizAppsOrgSettings** | List of available organization wide settings available in Dynamics 365 Customer Engagement / Dataverse | n/a |
| **MSBizAppsVIPUsers** | Parser for the **VIPUsers** watchlist | `VIPUsers` from watchlist template |
| **MSBizAppsNetworkAddresses** | Parser for the **NetworkAddresses** watchlist | `NetworkAddresses` from watchlist template |
| **MSBizAppsTerminatedEmployees** | Parser for the **TerminatedEmployees** watchlist | `TerminatedEmployees` from watchlist template |
| **DataverseSharePointSites** | SharePoint sites used in Dataverse Document Management | `MSBizApps-Configuration` watchlist filtered by category 'SharePoint' |

For more information about analytic rules, see [Detect threats out-of-the-box](../detect-threats-built-in).