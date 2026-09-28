---
layout: Conceptual
title: 'Custom detection rules with advanced hunting: Protecting SAP external OS commands (SAPXPG) - Microsoft Defender for Endpoint | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mde-sap-custom-detection-rules
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use advanced hunting with Defender for Endpoint to safeguard the SAPXPG mechanism with SAP systems.
author: chrisda
ms.author: chrisda
ms.date: 2025-05-20T00:00:00.0000000Z
ms.topic: overview
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
ms.collection: 
ms.custom:
- partner-contribution
ms.reviewer: cgardin
locale: en-us
document_id: e9402b80-4d32-2d69-12c5-625d81b4284c
document_version_independent_id: e9402b80-4d32-2d69-12c5-625d81b4284c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mde-sap-custom-detection-rules.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-sap-custom-detection-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mde-sap-custom-detection-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 9f2fb0e5-efa4-81cb-2e85-a8174781bb96
---

# Custom detection rules with advanced hunting: Protecting SAP external OS commands (SAPXPG) - Microsoft Defender for Endpoint | Microsoft Learn

SAP Systems can execute OS level commands by using `SAPXPG – Transaction Code SM49/SM69`. This article describes how to use advanced hunting with Microsoft Defender for Endpoint to help safeguard the SAPXPG mechanism to protect it from being exploited. The example illustrated in this article features SAP running on Linux; however, the procedure for SAP running on Windows Server is similar.

## Before you begin

Make sure to read the following articles before you begin:

- [Create custom detection rules](/en-us/defender-xdr/custom-detection-rules)
- [SAP Documentation: Starting External Commands and Programs](https://help.sap.com/doc/saphelp_nw73ehp1/7.31.19/en-US/4b/2b2bed365474fee10000000a421937/frameset.htm)

The SAP BASIS Team and the security team should codevelop the solution. The SAP BASIS team doesn't have access to the [Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-security-center-mde), and the security team doesn't know the specifics of the SAP Batch Jobs and External Commands. Both teams should work together.

## Recommended implementation sequence

1. The SAP BASIS team identifies and categorizes the external commands and scripts running on all SAP Environments (Dev, QA, PRD).
2. The security team and the SAP BASIS team ensure that Defender for Endpoint is correctly deployed and configured on all SAP servers. For deployment guidance, see the following articles:

    - [Deployment guidance for Microsoft Defender for Endpoint on Linux for SAP](https://aka.ms/mde4sap-linux)
    - [Microsoft Defender for Endpoint on Windows Server with SAP](https://aka.ms/mde4sap-windows)
3. The security team identifies all the SAP servers and runs a query for `"InitiatingProcessName" == "sapxpg"`, noting which servers are starting SAPXPG.

    We recommended limiting the number of servers running SAPXPG to a minimum, and disallowing SAPXPG on most SAP servers. And, the SAP BASIS team and security team should limit access to the authorization objects and transaction codes for SAPXPG.
4. The SAP BASIS team briefs the security team on any "allowed" utilities, such as `BRTOOLS` (for Oracle customers), `AzCopy` (if used) or other specific utilities for printing or archiving.
5. The security team works with the SAP BASIS team to query SAPXPG commands and parameters. An example query to detect `wget` (which can be used to download malicious payloads) is as follows:

    ```kusto
    
    DeviceProcessEvents
     | where Timestamp >= ago (1d)
     | where (InitiatingProcessFileName == "sapxpg" or  InitiatingProcessFileName =="sapxpg.exe")  and FileName == "wget"
    
    // Query shows SAPXPG commands that execute "wget"
    
    ```

    This query is designed to work on Linux (`sapxpg`) and Windows (`sapxpg.exe`).

    Another query/rule design logic is to block SAPXPG from executing any command other than specified allowed commands. In the following query, any command that is not in the set ("cp", "ls", "mkdir") can be alerted or blocked.

    ```kusto
    
    DeviceProcessEvents
     | where Timestamp >= ago (1d)
     | where (InitiatingProcessFileName == "sapxpg" or  InitiatingProcessFileName =="sapxpg.exe")  and FileName !in ("cp", "ls", "mkdir")
    
    //Query shows SAPXPG commands that execute any command other than "cp" or "mv" or mkdir
    
    ```
6. The security team [creates a custom detection rule](/en-us/defender-xdr/custom-detection-rules#2-create-new-rule-and-provide-alert-details) to detect suspicious commands. Suspicious commands could include:

    - `ncat`
    - `netcat`
    - `socat`
    - `azcopy`
    - `wget`
    - `curl`
    - `echo`
    - `base64`
    - `/dev/tcp`
    - `pwd`
    - `whoami`
    - `chmod +x`
7. The security team deploys the rule to non-production environments. The security team monitors detections, and the SAP BASIS team monitors jobs/interfaces for errors.
8. The security team deploys the rule to production environments. The SAP BASIS team should monitor jobs and interfaces, and the security team should monitor any alerts that are generated.

## Additional information

- To trace SAPXPG using `sapxpg_trace`, see [SAP documentation: Analyzing Problems with External Commands and Programs](https://help.sap.com/doc/saphelp_snc700_ehp01/7.0.1/en-US/4b/272d0ed1341780e10000000a42189c/content.htm?no_cache=true).
- To learn more about advanced hunting, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](/en-us/defender-xdr/advanced-hunting-overview).
- To learn more about custom rules, see [Create custom detection rules](/en-us/defender-xdr/custom-detection-rules#2-create-new-rule-and-provide-alert-details).