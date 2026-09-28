---
layout: Conceptual
title: Configure sensors for AD FS, AD CS, and Microsoft Entra Connect - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/active-directory-federation-services
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
description: Learn how to configure Microsoft Defender for Identity on Active Directory Federation Services (AD FS), Active Directory Certificate Services (AD CS), and Microsoft Entra Connect servers.
ms.date: 2026-08-31T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 49de276e-c6a2-46a3-2385-861dd47af16c
document_version_independent_id: 49de276e-c6a2-46a3-2385-861dd47af16c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/active-directory-federation-services.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/active-directory-federation-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/active-directory-federation-services.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2436d91c-852c-5e67-0682-7e57e07838f4
---

# Configure sensors for AD FS, AD CS, and Microsoft Entra Connect - Microsoft Defender for Identity | Microsoft Learn

## Install and configure sensors on non-domain-controller servers

Install and configure the Defender for Identity sensor v2.x on Active Directory Federation Services (AD FS), Active Directory Certificate Services (AD CS), and Microsoft Entra Connect servers that aren't domain controllers. Before you begin, make sure you've completed the [sensor installation prerequisites](prerequisites-sensor-version-2).

Tip

Deploying the Defender for Identity sensor v3.x on AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers is in preview. Use [sensor v3.x](deploy-sensor-v3) on eligible servers running Windows Server 2019 or later. Use the sensor v2.x procedures in this article only for supported servers running Windows Server 2016 or earlier.

These considerations apply:

- For AD FS environments, Defender for Identity sensors are supported only on the federation servers. They're not required on Web Application Proxy (WAP) servers.
- For AD CS environments, you don't need to install sensors on any AD CS servers that are offline.
- For Microsoft Entra Connect servers, you need to install the sensors on both active and staging servers.

## Prerequisites

For general sensor prerequisites, see the [Microsoft Defender for Identity prerequisites](prerequisites-sensor-version-2) article. The following additional requirements apply to AD FS, AD CS, and Microsoft Entra Connect servers.

A sensor installed on an AD FS, AD CS, or Microsoft Entra Connect server can't use the local service account to connect to the domain. Instead, you need to configure a [Directory Service Account](directory-service-accounts).

In addition, the Defender for Identity sensor for AD CS supports only AD CS servers with Certification Authority Role Service.

## Configure event collection

If you're working with AD FS, AD CS, or Microsoft Entra Connect servers, make sure that you configured auditing as needed. For more information, see:

- AD FS:

    - [Required AD FS events](configure-windows-event-collection#required-ad-fs-events)
    - [Configure auditing on an AD FS server](configure-windows-event-collection#configure-auditing-on-an-ad-fs-server)
- AD CS:

    - [Required AD CS events](configure-windows-event-collection#required-ad-cs-events)
    - [Configure auditing on an AD CS server](configure-windows-event-collection#configure-auditing-on-an-ad-cs-server)
- Microsoft Entra Connect:

    - [Required Microsoft Entra Connect events](configure-windows-event-collection#required-microsoft-entra-connect-events)
    - [Configure auditing on Microsoft Entra Connect](configure-windows-event-collection#configure-auditing-on-microsoft-entra-connect)

## Configure read permissions for the AD FS database

For sensors running on AD FS servers to have access to the AD FS database, you need to grant read (*db\_datareader*) permissions for the relevant [Directory Service Account](directory-service-accounts).

If you have more than one AD FS server, make sure to grant db\_datareader read access for the Directory Service Account across all of them. Database permissions aren't replicated across servers.

Configure the SQL server to allow the Directory Service Account with the following permissions to the *AdfsConfiguration* database:

- *connect*
- *log in*
- *read*
- *select*

### Grant access to the AD FS database

Grant access to the AD FS database by using SQL Server Management Studio, Transact-SQL (T-SQL), or PowerShell.

For example, the following commands might be helpful if you're using the Windows Internal Database (WID) or an external SQL server.

In these sample codes:

- `[DOMAIN1\mdiSvc01]` is the directory services user of the workspace. If you're working with a gMSA, append `$` to the end of the username. For example: `[DOMAIN1\mdiSvc01$]`.
- `AdfsConfigurationV4` is an example of an AD FS database name and might vary.
- `server=\.\pipe\MICROSOFT##WID\tsql\query` is the connection string to the database if you're using WID.

Tip

If you don't know your connection string, follow the steps in the [Windows Server documentation](/en-us/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-sql#to-acquire-the-sql-connection-string).

The following T-SQL script creates a SQL login for the Directory Service Account and grants it the required db\_datareader, connect, and select permissions on the AD FS configuration database:

```tsql
USE [master]
CREATE LOGIN [DOMAIN1\mdiSvc01] FROM WINDOWS WITH DEFAULT_DATABASE=[master]
USE [AdfsConfigurationV4]
CREATE USER [DOMAIN1\mdiSvc01] FOR LOGIN [DOMAIN1\mdiSvc01]
ALTER ROLE [db_datareader] ADD MEMBER [DOMAIN1\mdiSvc01]
GRANT CONNECT TO [DOMAIN1\mdiSvc01]
GRANT SELECT TO [DOMAIN1\mdiSvc01]
GO
```

The following PowerShell script connects to the Windows Internal Database (WID) or external SQL server instance and creates the required SQL login, db\_datareader role membership, and select permissions for the Directory Service Account on the AD FS configuration database:

```powershell
$ConnectionString = 'server=\\.\pipe\MICROSOFT##WID\tsql\query;database=AdfsConfigurationV4;trusted_connection=true;'
$SQLConnection= New-Object System.Data.SQLClient.SQLConnection($ConnectionString)
$SQLConnection.Open()
$SQLCommand = $SQLConnection.CreateCommand()
$SQLCommand.CommandText = @"
USE [master]; 
CREATE LOGIN [DOMAIN1\mdiSvc01] FROM WINDOWS WITH DEFAULT_DATABASE=[master];
USE [AdfsConfigurationV4]; 
CREATE USER [DOMAIN1\mdiSvc01] FOR LOGIN [DOMAIN1\mdiSvc01]; 
ALTER ROLE [db_datareader] ADD MEMBER [DOMAIN1\mdiSvc01]; 
GRANT CONNECT TO [DOMAIN1\mdiSvc01]; 
GRANT SELECT TO [DOMAIN1\mdiSvc01];
"@
$SqlDataReader = $SQLCommand.ExecuteReader()
$SQLConnection.Close()
```

## Configure permissions for the Microsoft Entra Connect (ADSync) database

Note

This section is applicable only if the Microsoft Entra Connect database is hosted on an external SQL server instance.

Microsoft recommends that you use the most secure authentication flow available. The authentication flow described in this procedure requires a very high degree of trust in the application, and carries risks that aren't present in other flows. You should only use this flow when other more secure flows, such as managed identities, aren't viable.

Sensors running on Microsoft Entra Connect servers need to have access to the ADSync database, and have execute permissions for the relevant stored procedures. If you have more than one Microsoft Entra Connect server, make sure to run the following PowerShell script on each server to grant ADSync database access and stored procedure permissions.

To grant the sensor permissions to the Microsoft Entra Connect ADSync database by using PowerShell:

```powershell
$entraConnectServerDomain = $env:USERDOMAIN
$entraConnectServerComputerAccount = $env:COMPUTERNAME
$entraConnectDBName = (Get-ItemProperty 'registry::HKLM\SYSTEM\CurrentControlSet\Services\ADSync\Parameters' -Name 'DBName').DBName
$entraConnectSqlServer = (Get-ItemProperty 'registry::HKLM\SYSTEM\CurrentControlSet\Services\ADSync\Parameters' -Name 'Server').Server
$entraConnectSqlInstance = (Get-ItemProperty 'registry::HKLM\SYSTEM\CurrentControlSet\Services\ADSync\Parameters' -Name 'SQLInstance').SQLInstance

$ConnectionString = 'server={0}\{1};database={2};trusted_connection=true;' -f $entraConnectSqlServer, $entraConnectSqlInstance, $entraConnectDBName
$SQLConnection= New-Object System.Data.SQLClient.SQLConnection($ConnectionString)
$SQLConnection.Open()
$SQLCommand = $SQLConnection.CreateCommand()
$SQLCommand.CommandText = @"
USE [master]; 
CREATE LOGIN [{0}\{1}$] FROM WINDOWS WITH DEFAULT_DATABASE=[master];
USE [{2}];
CREATE USER [{0}\{1}$] FOR LOGIN [{0}\{1}$];
GRANT CONNECT TO [{0}\{1}$];
GRANT SELECT TO [{0}\{1}$];
GRANT EXECUTE ON OBJECT::{2}.dbo.mms_get_globalsettings TO [{0}\{1}$];
GRANT EXECUTE ON OBJECT::{2}.dbo.mms_get_connectors TO [{0}\{1}$];
"@ -f $entraConnectServerDomain, $entraConnectServerComputerAccount, $entraConnectDBName
$SqlDataReader = $SQLCommand.ExecuteReader()
$SQLConnection.Close()
```

## Post-installation steps (optional)

During the sensor installation on an AD FS, AD CS, or Microsoft Entra Connect server, the closest domain controller is automatically selected. Use the following steps to check or modify the selected domain controller:

1. In [Microsoft Defender XDR](https://security.microsoft.com), go to **Settings** &gt; **Identities** &gt; **Sensors** to view all of your Defender for Identity sensors.
2. Locate and select the sensor that you installed on the server.
3. On the pane that opens, in the **Domain controller (FQDN)** box, enter the fully qualified domain name (FQDN) of the resolver domain controllers. Select **+ Add** to add the FQDN, and then select **Save**.

    ![Screenshot of Defender for Identity sensor settings pane showing the Domain controller (FQDN) field where you enter the resolver domain controller for an AD FS sensor.](../media/sensor-config-adfs-resolver.png)

Initializing the sensor might take a couple of minutes. When it finishes, the service status of the AD FS, AD CS, or Microsoft Entra Connect sensor changes from **stopped** to **running**.

## Validate successful deployment

To validate that you successfully deployed a Defender for Identity sensor on an AD FS or AD CS server:

1. Check that the **Azure Advanced Threat Protection sensor** service is running. After you save the Defender for Identity sensor settings, it might take a few seconds for the service to start.
2. If the service doesn't start, review the `Microsoft.Tri.sensor-Errors.log` file, located by default at `%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs`.
3. Use AD FS or AD CS to authenticate a user to any application, and then verify that Defender for Identity observed the authentication.

    For example, select **Hunting** &gt; **Advanced Hunting**. On the **Query** pane, enter and run one of the following queries:

    - For AD FS:

        ```query
        IdentityLogonEvents | where Protocol contains 'Adfs'
        ```

        The results pane should include a list of events with a **LogonType** value of **Logon with ADFS authentication**.
    - For AD CS:

        ```query
        IdentityDirectoryEvents | where Protocol == "Adcs"
        ```

        The results pane shows a list of events of failed and successful certificate issuance. Select a specific row to see additional details on the **Inspect record** pane.

        [![Screenshot of the results of an Active Directory Certificate Services logon advanced hunting query.](../media/adfs-logon-advanced-hunting.png)](../media/adfs-logon-advanced-hunting.png#lightbox)