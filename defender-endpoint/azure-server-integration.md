---
layout: Conceptual
title: The new Defender server security experience - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/azure-server-integration
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Review cloud and endpoint information, investigate threats, and check access for servers in Microsoft Defender.
ms.service: defender-endpoint
ms.subservice: onboard
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: concept-article
ms.date: 2026-09-23T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 49663056-840a-8b6b-ab4e-826adba83c08
document_version_independent_id: 49663056-840a-8b6b-ab4e-826adba83c08
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/azure-server-integration.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: azure-server-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/azure-server-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 817db59c-37d9-fa07-ed5d-ac8bd80554bc
---

# The new Defender server security experience - Microsoft Defender for Endpoint | Microsoft Learn

The new Defender server security experience brings Defender for Endpoint and Defender for Servers together in the Microsoft Defender portal. Use it to manage server protection and investigate threats with cloud and endpoint information in one place.

This public preview covers Azure environments and on-premises servers. See [What's new](/en-us/azure/defender-for-cloud/release-notes#new-defender-server-security-experience) for the release summary.

On this page: Server asset page | Investigate an incident | Go hunt | RBAC and device groups.

## Servers already running Defender for Endpoint

Servers already running Defender for Endpoint continue operating with their existing configuration. You don't need to onboard, reinstall, or migrate them to maintain their existing protection. Review the requirements for each unified capability before changing your configuration.

## Review the server asset page

The server asset page brings together available cloud-resource and endpoint-device information for the same server, instead of requiring separate investigation pages.

1. In [Microsoft Defender](https://security.microsoft.com), open an alert involving the server and select **Open asset page** from the server's menu. From an incident graph, open the server node's menu and select **Asset details**.
2. Check the endpoint device ID and, where available, the Azure resource ID. Don't identify a server by name alone.
3. Review the server's identity, onboarding status, and available resource and operating-system details.
4. Select **Open device timeline** to inspect endpoint activity, or Go hunt to investigate related events.

If records appear duplicated or incorrectly matched, check both identifiers before taking action. Available context depends on connected data sources; manual onboarding doesn't create an Azure resource.

Response actions depend on your permissions, the platform, and the server's state. Use the [supported device-response guidance](respond-machine-alerts) before taking an action that could affect the workload.

## Investigate alerts and incidents

To investigate a server, you need access to its investigation data, and the server must have a related alert or incident.

1. Open an incident involving the server and review its attack graph.
2. Select the server node. For a server with correlated cloud and endpoint records, the graph provides one server identity and investigation menu.
3. Right-click the node or open its ellipsis menu. Choose **Asset details** for context, **Pin related alerts** to inspect related detections, or **Go hunt** to investigate activity.
4. Open a related alert and follow its server link. Confirm that it leads to the same server identity before considering a response action.

Cloud and endpoint alerts can refer to the same server without becoming a single alert. A shared asset identity doesn't guarantee that every alert is grouped into one incident.

### Use Go hunt

You need [advanced hunting access](/en-us/defender-xdr/advanced-hunting-overview#get-access) to the data being queried. Being able to open an asset page doesn't grant access to all hunting tables.

1. From the incident graph, open the server node's menu and select **Go hunt**. You can also use the action from the server's alert or asset context where available.
2. Choose **All activity**, **Related alerts**, or **See all available queries**, then select the query you need.
3. Inspect the generated query and its results in advanced hunting. Go hunt can execute the generated query automatically rather than only displaying it for review.
4. Check that the query targets the intended server. Where both identities are available, review its endpoint device and cloud-resource identifiers, selected tables, and time range.
5. To investigate another time window, adjust the query's timestamp filter and run it again. Use UTC in query expressions.
6. Open relevant results, compare their timestamps with the alert, and return to the incident to continue the investigation.

For a specific endpoint event, open **Device timeline**, select the event, and use **Hunt for related events** where available. This searches around that event rather than starting from the whole server.

**All activity** doesn't guarantee every data source is included. If results are empty or incomplete, check the query filters, available tables, retention, endpoint reporting, and your data permissions. An empty query result doesn't establish that the server is unaffected. See [Go hunt query behavior](/en-us/defender-xdr/advanced-hunting-go-hunt) for query-adjustment guidance.

## Verify RBAC and server access

Roles define **what a person can do**; scopes define **which data they can access**.

| Control | Purpose |
| --- | --- |
| Microsoft Entra user group | Identifies the people receiving access, such as a server operations team. |
| Defender RBAC role | Grants selected read, investigation, response, or administration permissions. |
| Device group | Groups endpoints and controls access to their data through assigned Entra user groups. It can also set automated-remediation behavior. |
| [Cloud scope](/en-us/azure/defender-for-cloud/cloud-scopes-unified-rbac?pivots=defender-portal) | Groups selected cloud environments, such as Azure subscriptions, for cloud-data access. It is separate from Azure RBAC. |

For a server represented in both cloud and endpoint data, configure the relevant cloud scope **and** device group. Linking a device group to a cloud scope aligns server membership; it doesn't replace role assignments or grant users access by itself. Existing endpoint-only deployments don't need a cloud connection just to continue operating.

### Assign the team's permissions

Use the permissions model active in your tenant. Don't activate a different model merely to follow this guide.

For tenants using [Microsoft Defender unified RBAC](/en-us/defender-xdr/manage-rbac), a Security Administrator or an administrator with the required delegated **Authorization** permissions can:

1. Open **Permissions** &gt; **Microsoft Defender XDR** &gt; **Roles** and create or edit the appropriate role.
2. Select the permissions the team needs. Keep investigation access separate from response and administration permissions.
3. Add an assignment for the team's Microsoft Entra security group and the required data sources. Access to Defender for Endpoint data alone doesn't grant access to Defender for Cloud data.
4. For cloud data, select the intended cloud scopes. Review and submit the assignment.

Follow [Create custom roles](/en-us/defender-xdr/create-custom-rbac-roles) for the full wizard. Tenants still using the previous endpoint model should use [Defender for Endpoint RBAC](rbac); existing roles aren't replaced by this experience.

### Define a server device group

Create a device group to manage access to servers using device conditions or existing cloud scopes. Before you begin, ensure that the Microsoft Entra user groups you want to assign have the appropriate role-based access control (RBAC) roles.

1. In the Microsoft Defender portal, go to **Settings** &gt; **Endpoints** &gt; **Permissions** &gt; **Device groups**.
2. Select **Add device group**, or edit an existing group. Enter a descriptive name and review the automated-remediation level.
3. On the **Devices** page, choose how to populate the group:

    | Option | Description |
    | --- | --- |
    | **Define using conditions** | Match servers using supported device attributes, such as device name, domain, tags, or OS platform. |
    | **Select cloud scopes to populate this group** | Select one or more existing cloud scopes. Devices from all selected scopes are included. (preview) |
4. Select **Next** and review the matching devices on the **Preview devices** page before continuing.
5. On the **User access** page, select the Microsoft Entra user groups that should have access, and then select **Submit**.
6. Review the group's membership and access assignments. For condition-based groups, review the group ranking: a device that matches multiple condition-based groups belongs to the highest-ranked group.

Note

Cloud-scope membership includes all devices from the selected scopes. Review the selected scopes to ensure that the group includes only the intended devices.

### Align a cloud scope and device group

1. If needed, create the Azure scope under **System** &gt; **Permissions** &gt; **Microsoft Defender XDR** &gt; **Scopes** &gt; **Add cloud scope**. Select the intended connected Azure subscriptions.
2. Assign the team's cloud-data permissions to that scope, then select it in the device group's **Devices** step.
3. Keep the team's endpoint role and device-group **User access** assignment in place. Verify access to both data sources.

Follow [Manage cloud scopes](/en-us/azure/defender-for-cloud/cloud-scopes-unified-rbac?pivots=defender-portal) if scope activation is required. Activation is an irreversible configuration change: review existing assignments and the activation wizard before proceeding.

The cloud-scope link updates device membership as the selected scope's contents change. Newly connected environments aren't automatically added to the cloud scope. Review scope membership when adding an Azure environment.

### Check the effective access

Test with ordinary analyst accounts, not only a Security Administrator account; broad administrator access can hide scoping mistakes. A display filter narrows a view but isn't a substitute for permissions.

| Check | Required outcome |
| --- | --- |
| Open a server within the user's assigned access | The intended server and permitted data are available. |
| Navigate from an alert or incident to the asset and hunting | The server identity remains correct and access remains appropriate. |
| Attempt to open an out-of-scope server | Restricted data and actions remain inaccessible. |
| Check a response or configuration action | The action is available only to an authorized user; don't execute disruptive actions just to test access. |

If expected access is missing, check role permissions, data-source assignments, Entra group membership, the device's effective group, and its cloud scope. If an analyst sees unintended server data, review other role assignments and broad access before expanding the rollout.

## Remove server protection

See [Offboard devices](offboard-machines) for automatic Azure offboarding and other supported offboarding methods.