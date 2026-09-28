---
layout: Conceptual
title: Directory Service Accounts for Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/directory-service-accounts
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn about how Microsoft Defender for Identity uses Directory Service accounts (DSAs).
ms.date: 2024-01-16T00:00:00.0000000Z
ms.topic: article
ms.reviewer: rlitinsky
locale: en-us
document_id: 0583491b-eeb3-568d-0984-55e9c4c7ee32
document_version_independent_id: 0583491b-eeb3-568d-0984-55e9c4c7ee32
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/directory-service-accounts.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/directory-service-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/directory-service-accounts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 114c57b4-cbb8-b80d-5121-9d48f99bc424
---

# Directory Service Accounts for Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

Defender for Identity uses Directory Service Accounts (DSAs) to read data from Active Directory, such as querying objects, tracking changes, and resolving entities. This is separate from the [action account](manage-action-accounts), which performs remediation actions like disabling users or resetting passwords.

Note

Directory Service Accounts apply to the Defender for Identity sensor v2.x only. The sensor v3.x doesn't use DSA or gMSA configuration and uses LocalSystem exclusively. For more information, see [Defender for Identity sensor v3.x service account requirements](deploy-sensor-v3#service-account-requirements).

Note

Regardless of the Directory Service Accounts configured, the sensor service operates under the LocalSystem identity, and the updater service operates under the LocalSystem identity.

While a DSA is optional in some scenarios, we recommend that you configure a DSA for Defender for Identity for full security coverage.

For example, when you have a DSA configured, the DSA is used to connect to the domain controller at startup. A DSA can also be used to query the domain controller for data on entities seen in network traffic, monitored events, and monitored ETW activities

A DSA is required for the following features and functionality:

- When working with a sensor installed on an [AD FS, AD CS, or Microsoft Entra Connect server](active-directory-federation-services).
- Requesting member lists for local administrator groups from devices seen in network traffic, events and ETW activities via a [SAM-R call](remote-calls-sam) made to the device.
- Accessing the *DeletedObjects* container to collect information about deleted users and computers.
- Domain and trust mapping, which occurs at sensor startup, and again every 10 minutes.
- Querying another domain via LDAP for details, when detecting activities from entities in those other domains.

When you're using a single DSA, the DSA must have *Read* permissions to all the domains in the forests. In an untrusted, multi-forest environment, a DSA account is required for each forest.

One sensor in each domain is defined as the *domain synchronizer*, and is responsible for tracking changes to the entities in the domain. For examples, changes might include objects created, entity attributes tracked by Defender for Identity, and so on.

Note

By default, Defender for Identity supports up to 30 credentials. To add more credentials, contact Defender for Identity support.

## Supported DSA account options

Defender for Identity supports the following DSA options:

| Option | Description | Configuration |
| --- | --- | --- |
| **Group Managed Service Account gMSA** (Recommended) | Provides a more secure deployment and password management. Active Directory manages the creation and rotation of the account's password, just like a computer account's password, and you can control how often the account's password is changed. | For more information, see [Configure a Directory Service Account for Defender for Identity with a gMSA](create-directory-service-account-gmsa). |
| **Regular user account** | Easy to use when getting started, and simpler to configure *Read* permissions between trusted forests, but requires extra overhead for password management. A regular user account is less secure, as it requires you to create and manage passwords, and can lead to downtime if the password expires and isn't updated for both the user and the DSA. | Create a new account in Active Directory to use as the DSA with *Read* permissions to all the objects, including permissions to the *DeletedObjects* container. For more information, see Grant required DSA permissions. |
| **Local service account** | The Local service account is used out of the box and used by default when there is no DSA configured. Note: - SAM-R queries for potential lateral movement paths not supported in this scenario.<br>- LDAP queries only within the domain the sensor is installed. Queries to other domains in the same forest or cross forest will fail. | None |

Note

While the local service account is used with the sensor by default, and a DSA is optional in some scenarios, we recommend that you configure a DSA for Defender for Identity for full security coverage.

## DSA entry usage

This section describes how DSA entries are used, and how the sensor selects a DSA entry in any given scenario. Sensor attempts differ, depending on the type of DSA entry:

| Type | Description |
| --- | --- |
| **gMSA account** | The sensor attempts to retrieve the gMSA account password from Active Directory, and then signs into the domain. |
| **Regular user account** | The sensor attempts to sign into the domain using the configured username and password. |

The following logic is applied:

1. The sensor looks for an entry with an exact match of the domain name for the target domain. If an exact match is found, the sensor attempts to authenticate using the credentials in that entry.
2. If there isn't an exact match, or if the authentication failed, the sensor searches the list for an entry to the parent domain using DNS FQDN, and attempts to authenticate using the credentials in the parent entry instead.
3. If there isn't an entry for the parent domain, or if the authentication failed, the sensor searches the list for a sibling domain entry, using the DNS FQDN, and attempts to authenticate using the credentials in the sibling entry instead.
4. If there isn't an entry for the sibling domain, or if the authentication failed, the sensor reviews the list again and tries to authenticate again with each entry until it succeeds. DSA gMSA entries have higher priority than regular DSA entries.

### Sample logic with a DSA

This section provides an example of how the sensor tries the DSA entires when you have multiple accounts, including both a gMSA account and a regular account.

The following logic is applied:

1. The sensor looks for a match between the DNS domain name of the target domain, such as `emea.contoso.com` and the DSA gMSA entry, such as `emea.contoso.com`.
2. The sensor looks for a match between the DNS domain name of the target domain, such as `emea.contoso.com` and the DSA regular entry DSA, such as `emea.contoso.com`
3. The sensor looks for a match in the root DNS name of the target domain, such as `emea.contoso.com` and the DSA gMSA entry domain name, such as `contoso.com`.
4. The sensor looks for a match in the root DNS name of the target domain, such as `emea.contoso.com` and the DSA regular entry domain name, such as `contoso.com`.
5. The sensor looks for the target domain name for a sibling domain, such as `emea.contoso.com` and the DSA gMSA entry domain name, such as `apac.contoso.com`.
6. The sensor looks for the target domain name for a sibling domain, such as `emea.contoso.com` and the DSA regular entry domain name, such as `apac.contoso.com`.
7. The sensor runs a round robin of all DSA gMSA entries.
8. The sensor runs a round robin of all DSA regular entries.

The logic shown in this example is implemented with the following configuration:

- **DSA entries**:

    - `DSA1.emea.contoso.com`
    - `DSA2.fabrikam.com`
- **Sensors and the DSA entry that's used first**:

    | Domain controller FQDN | DSA entry used |
    | --- | --- |
    | `DC01.emea.contoso.com` | `DSA1.emea.contoso.com` |
    | `DC02.contoso.com` | `DSA1.emea.contoso.com` |
    | `DC03.fabrikam.com` | `DSA2.fabrikam.com` |
    | `DC04.contoso.local` | Round robin |

Important

If a sensor isn't able to successfully authenticate via LDAP to the Active Directory domain at startup, the sensor won't enter a running state and a health issue is generated. For more information, see [Defender for Identity health issues](../health-alerts).

## Grant required DSA permissions

The DSA requires read only permissions on **all** the objects in Active Directory, including the **Deleted Objects Container**.

The read-only permissions on the **Deleted Objects** container allows Defender for Identity to detect user deletions from your Active Directory.

Use the following code sample to help you grant the required read permissions on the **Deleted Objects** container, whether or not you're using a gMSA account.

Tip

If the DSA you want to grant the permissions to is a Group Managed Service Account (gMSA), you must first create a security group, add the gMSA as a member, and add the permissions to that group. For more information, see [Configure a Directory Service Account for Defender for Identity with a gMSA](create-directory-service-account-gmsa).

```powershell
# Declare the identity that you want to add read access to the deleted objects container:
$Identity = 'mdiSvc01'

# If the identity is a gMSA, first to create a group and add the gMSA to it:
$groupName = 'mdiUsr01Group'
$groupDescription = 'Members of this group are allowed to read the objects in the Deleted Objects container in AD'
if(Get-ADServiceAccount -Identity $Identity -ErrorAction SilentlyContinue) {
    $groupParams = @{
        Name           = $groupName
        SamAccountName = $groupName
        DisplayName    = $groupName
        GroupCategory  = 'Security'
        GroupScope     = 'Universal'
        Description    = $groupDescription
    }
    $group = New-ADGroup @groupParams -PassThru
    Add-ADGroupMember -Identity $group -Members ('{0}$' -f $Identity)
    $Identity = $group.Name
}

# Get the deleted objects container's distinguished name:
$distinguishedName = ([adsi]'').distinguishedName.Value
$deletedObjectsDN = 'CN=Deleted Objects,{0}' -f $distinguishedName

# Take ownership on the deleted objects container:
$params = @("$deletedObjectsDN", '/takeOwnership')
C:\Windows\System32\dsacls.exe $params

# Grant the 'List Contents' and 'Read Property' permissions to the user or group:
$params = @("$deletedObjectsDN", '/G', ('{0}\{1}:LCRP' -f ([adsi]'').name.Value, $Identity))
C:\Windows\System32\dsacls.exe $params
  
# To remove the permissions, uncomment the next 2 lines and run them instead of the two prior ones:
# $params = @("$deletedObjectsDN", '/R', ('{0}\{1}' -f ([adsi]'').name.Value, $Identity))
# C:\Windows\System32\dsacls.exe $params
```

For more information, see [Changing permissions on a deleted object container](/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824%28v=ws.10%29).

## Test your DSA permissions and delegations via PowerShell

Use the following PowerShell command to verify that your DSA doesn't have too many permissions, such as powerful admin permissions:

```powershell
Test-MDIDSA [-Identity] <String> [-Detailed] [<CommonParameters>]
```

For example, to check permissions for the **mdiSvc01** account and provide full details, run:

```powershell
Test-MDIDSA -Identity "mdiSvc01" -Detailed
```

For more information, see the [DefenderForIdentity PowerShell reference](/en-us/powershell/module/defenderforidentity/test-mdidsa).