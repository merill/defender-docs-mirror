---
layout: Conceptual
title: Configure Windows event auditing - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/configure-windows-event-collection
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
description: Configure Windows event auditing for Defender for Identity sensors. Learn automatic, manual, and PowerShell methods to enable required audit policies.
ms.date: 2026-08-10T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1015
- sfi-image-nochange
ms.reviewer: rlitinsky
ai-usage: ai-assisted
locale: en-us
document_id: 01ae5b99-6873-1583-9722-3bdbd8dd2309
document_version_independent_id: 01ae5b99-6873-1583-9722-3bdbd8dd2309
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/configure-windows-event-collection.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/configure-windows-event-collection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/configure-windows-event-collection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 05ed5b0c-f510-a947-1ae0-22c5af2fdf44
---

# Configure Windows event auditing - Microsoft Defender for Identity | Microsoft Learn

Configure Windows event auditing to enable Defender for Identity detections. The sensor parses specific Windows event logs from your domain controllers, AD FS servers, AD CS servers, and Microsoft Entra Connect servers. For the correct events to be audited and included in the Windows event log, these servers need the correct advanced audit policy settings.

Configure auditing using one of these methods:

- Automatic configuration for sensor v3.x on domain controllers, AD FS, AD CS, and Microsoft Entra Connect servers (recommended)
- Manual configuration for sensor v2.x or if you opted out of automatic auditing
- PowerShell configuration
- Required Windows events for all server types

Defender for Identity generates health alerts when it detects incorrect Windows event auditing configurations. For more information, see [Microsoft Defender for Identity health alerts](../health-alerts).

If you configure auditing properly, Windows event auditing has minimal effect on server performance.

## Configure Defender for Identity to collect Windows events automatically

If you're deploying the Defender for Identity sensor v3.x, use automatic Windows auditing. This approach requires no manual configuration and handles all auditing settings for you.

### Turn on automatic Windows auditing

To enable automatic Windows auditing in the Defender portal, complete the following steps:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings**, and then **Identities**.
2. In the **General** section, select **Advanced features**.
3. Turn on **Automatic Windows auditing configuration**.

### What automatic auditing configures

When enabled, the sensor automatically:

- Checks current Windows event auditing configuration.
- Identifies any gaps in the configuration.
- Applies any necessary changes, including all of the steps in the manual configuration:
    - **Directory services advanced auditing**: Adds audit entries to the domain root object's System Access Control List (SACL) to enable required directory service auditing.
    - **NTLM auditing**: Uses standard Windows Registry APIs to configure the required NTLM auditing registry values.
    - **Domain object auditing**: Modifies the SACL on the Configuration partition to capture changes to directory service configuration objects.
    - **AD FS auditing**: Automatically configures the following settings:
        - **Object-level auditing on the AD FS configuration container**: Adds audit entries to the object's System Access Control List (SACL) of the AD FS configuration container, to enable auditing of AD FS-related directory objects.
        - **Group Policy for event auditing**: Configures the **Audit Application Generated** advanced audit policy (Success and Failure) on the local system by using the Windows Local Security Authority (LSA) audit policy APIs under the sensor's local system account.
        - Other AD FS auditing settings aren't included in automatic auditing and remain manual, such as AD FS event auditing in AD FS Management and verbose logging for AD FS events.
    - **AD CS auditing**: Writes the required value to the certificate authority (CA) audit filter in the CA's registry configuration. Automatic auditing modifies an existing audit filter but doesn't create one, so the CA must already have an audit filter configured. The new value takes effect after the Certificate Services (`certsvc`) service restarts. Until the service restarts, Defender for Identity raises a health alert that prompts you to restart it.
    - **Microsoft Entra Connect auditing**: Configures the **Audit Logon** advanced audit policy (Success and Failure) on Microsoft Entra Connect servers by using the Windows LSA audit policy APIs.
    - **Windows audit policy**: Configures the local Windows audit policies using the Windows LSA audit policy APIs.
- Applies auditing settings directly to the local system policy of the server.
- Runs once every 24 hours.

Note

- Automatic Windows event auditing is supported only for domain controllers and AD FS, AD CS, and Microsoft Entra Connect servers that use Defender for Identity sensor v3.x. For servers that use sensor v2.x, configure Windows event auditing manually.
- If you don't turn on automatic Windows auditing, you **must**configure Windows event auditing manually or by configuring Windows event collection using PowerShell.
- GPO settings can conflict with local settings set by the sensor.

## Required Windows events

This section lists the Windows events that the Defender for Identity sensor requires. The specific events depend on the server type where the sensor is installed.

### Required AD FS events

The following events are required for AD FS servers:

- 1202: The Federation Service validated a new credential
- 1203: The Federation Service failed to validate a new credential
- 4624: An account was successfully logged on
- 4625: An account failed to log on

For more information, see Configure auditing on an AD FS server.

### Required AD CS events

The following events are required for AD CS servers:

- 4870: Certificate Services revoked a certificate
- 4882: The security permissions for Certificate Services changed
- 4885: The audit filter for Certificate Services changed
- 4887: Certificate Services approved a certificate request and issued a certificate
- 4888: Certificate Services denied a certificate request
- 4890: The certificate manager settings for Certificate Services changed
- 4896: One or more rows have been deleted from the certificate database

For more information, see Configure auditing on an AD CS server.

### Required Microsoft Entra Connect events

The following event is required for Microsoft Entra Connect servers:

- 4624: An account was successfully logged on

For more information, see Configure auditing on Microsoft Entra Connect.

### Other required Windows events

The following general Windows events are required for all Defender for Identity sensors on domain controllers:

- 4662: An operation was performed on an object
- 4726: User Account Deleted
- 4728: Member Added to Global Security Group
- 4729: Member Removed from Global Security Group
- 4730: Global Security Group Deleted
- 4732: Member Added to Local Security Group
- 4733: Member Removed from Local Security Group
- 4741: Computer Account Added
- 4743: Computer Account Deleted
- 4753: Global Distribution Group Deleted
- 4756: Member Added to Universal Security Group
- 4757: Member Removed from Universal Security Group
- 4758: Universal Security Group Deleted
- 4763: Universal Distribution Group Deleted
- 4776: Domain Controller Attempted to Validate Credentials for an Account (NTLM)
- 5136: A directory service object was modified
- 7045: New Service Installed
- 8004: NTLM Authentication

For more information, see Configure NTLM auditing and Configure domain object auditing.

### Event collection for standalone sensors

If you're working with a standalone Defender for Identity sensor, configure event collection manually by using one of the following methods:

- [Listen for security information and event management (SIEM) events on your Defender for Identity standalone sensor](configure-event-collection). Defender for Identity supports User Datagram Protocol (UDP) traffic from your SIEM system or your syslog server.
- [Configure Windows event forwarding to your Defender for Identity standalone sensor](configure-event-forwarding). When you're forwarding syslog data to a standalone sensor, make sure not to forward *all* syslog data to your sensor.

Important

Defender for Identity standalone sensors don't support the collection of Event Tracing for Windows (ETW) log entries that provide the data for multiple detections. For full coverage of your environment, deploy the Defender for Identity sensor.

For more information, see the product documentation for your SIEM system or your syslog server.

## Check your current configuration

Before configuring Windows event collection manually, you can run a PowerShell script to check your current configuration and generate a report of any adjustments you need to make:

1. Download the [Defender for Identity PowerShell module](https://www.powershellgallery.com/packages/DefenderForIdentity/).
2. Run the Defender for Identity `New-MDIConfigurationReport` PowerShell module to generate a report of your current Windows event auditing configuration.

    ```powershell
        New-MDIConfigurationReport -Path "C:\Reports" -Mode Domain -Identity "DOMAIN\ServiceAccountName" -OpenHtmlReport
    ```

    Where:

    - `Path` is the directory where the report is saved.
    - `Mode`indicates where the settings are collected from.
        - In `Domain` mode, the settings are collected from the Group Policy objects (GPOs). When using `-Mode Domain`, include the `-Identity` parameter to avoid an interactive prompt.
        - In `LocalMachine` mode, the settings are collected from the local machine.
    - `OpenHtmlReport` opens the HTML report after the report is generated. For example, to generate a report and open it in your default browser, run the following command:

    ```powershell
    New-MDIConfigurationReport -Path "C:\Reports" -Mode Domain -OpenHtmlReport
    ```

    For more information, see [New-MDIConfigurationReport](/en-us/powershell/module/defenderforidentity/new-mdiconfigurationreport?view=defenderforidentity-latest&amp;preserve-view=true).
3. Review the report and make any necessary adjustments before configuring Windows event collection.

## Configure Windows event collection manually

This section includes instructions for manually configuring Windows event collection. Use these steps if you're deploying sensor v2.x or if you opted out of automatic auditing for sensor v3.x.

Note

**Known issue:** In some sensor v3.x environments, health alerts about Windows event auditing might persist even when auditing is correctly configured. This primarily occurs with manual auditing configuration, such as using Group Policy or PowerShell. The sensor remains healthy and detections aren't affected. To resolve, enable **Automatic Windows auditing configuration** in the Defender for Identity portal under **Settings** &gt; **Advanced features**.

The following sections describe configuration for each server type:

- Configure auditing on a domain controller
- Configure auditing on an AD FS server
- Configure auditing on an AD CS server
- Configure auditing on Microsoft Entra Connect
- Configure auditing on the Configuration container

### Configure auditing on a domain controller

To configure auditing on a domain controller, complete the following steps:

- Configure Directory Services Advanced Auditing
- Configure NTLM auditing
- Configure Domain object auditing
- Configure object-level auditing on the AD FS configuration folder

#### Configure Directory Services Advanced Auditing

The following procedure describes how to modify your domain controller's Audit (Premium) Policy settings for Defender for Identity.

1. Sign in to the server as **Domain Administrator**.
2. Open the Group Policy Management Editor from **Server Manager** &gt; **Tools** &gt; **Group Policy Management**.
3. Expand **Domain Controllers Organizational Units**, right-click **Default Domain Controllers Policy**, and then select **Edit**.

    ![Screenshot of the pane for editing the default policy for domain controllers.](../media/configure-windows-event-collection/advanced-audit-policy-check-step-1.png)

    Note

    Use the Default Domain Controllers policy or a dedicated GPO to set these policies.
4. Go to **Computer Configuration** &gt; **Policies** &gt; **Windows Settings** &gt; **Security Settings**. Depending on the policy you want to enable, do the following:

    1. Go to **Advanced Audit Policy Configuration** &gt; **Audit Policies**.

        ![Screenshot of selections for opening an audit policy.](../media/configure-windows-event-collection/advanced-audit-policy-check-step-2.png)
    2. Under **Audit Policies**, edit each of the following policies and select **Configure the following audit events** for both **Success** and **Failure** events.

        | Audit policy | Subcategory | Triggers event IDs |
        | --- | --- | --- |
        | **Account Logon** | **Audit Credential Validation** | 4776 |
        | **Account Management** | **Audit Computer Account Management**^Failure auditing note^ | 4741, 4743 |
        | **Account Management** | **Audit Distribution Group Management**^Failure auditing note^ | 4753, 4763 |
        | **Account Management** | **Audit Security Group Management**^Failure auditing note^ | 4728, 4729, 4730, 4732, 4733, 4756, 4757, 4758 |
        | **Account Management** | **Audit User Account Management** | 4726 |
        | **DS Access** | **Audit Directory Service Changes**^See note^ | 5136 |
        | **System** | **Audit Security System Extension**^See note^ | 7045 |
        | **DS Access** | **Audit Directory Service Access** | 4662 - For this event, you must also configure domain object auditing. |

        Note

        * These subcategories don't support failure events. Add them for auditing purposes in case they're implemented in the future. For more information, see [Audit Computer Account Management](/en-us/windows/security/threat-protection/auditing/audit-computer-account-management), [Audit Security Group Management](/en-us/windows/security/threat-protection/auditing/audit-security-group-management), and [Audit Security System Extension](/en-us/windows/security/threat-protection/auditing/audit-security-system-extension).
    3. To configure **Audit Security Group Management**, under **Account Management**, select **Audit Security Group Management**, and then select **Configure the following audit events** for both **Success** and **Failure** events.

        ![Screenshot of the audit security group management properties log.](../media/configure-windows-event-collection/advanced-audit-policy-check-step-4.png)
5. From an elevated command prompt, enter `gpupdate`.
6. After you apply the policy via GPO, confirm that the new events appear in the Event Viewer, under **Windows Logs** &gt; **Security**.

    To test your audit policies from the command line, run the following command:

    ```cmd
    auditpol.exe /get /category:*
    ```

For more information, see the [auditpol reference documentation](/en-us/windows-server/administration/windows-commands/auditpol).

#### Configure NTLM auditing

When a Defender for Identity sensor parses Windows event 8004, it enriches Defender for Identity NTLM authentication activities with the server-accessed data. This section describes the configuration steps for auditing Windows event 8004.

Note

Apply domain group policies to collect Windows event 8004 *only* to domain controllers.

To configure NTLM auditing:

1. Open **Group Policy Management** and Expand **Domain Controllers Organizational Units**, right-click **Default Domain Controllers Policy**, and then select **Edit**.
2. Go to **Default Domain Controllers Policy** &gt; **Local Policies** &gt; **Security Options**.
3. Configure the specified security policies as follows:

    | Security policy setting | Value |
    | --- | --- |
    | **Network security: Restrict NTLM: Outgoing NTLM traffic to remote servers** | Audit all |
    | **Network security: Restrict NTLM: Audit NTLM authentication in this domain** | Enable all |
    | **Network security: Restrict NTLM: Audit Incoming NTLM Traffic** | Enable auditing for all accounts |
4. To configure **Outgoing NTLM traffic to remote servers**, under **Security Options**, double-click **Network security: Restrict NTLM: Outgoing NTLM traffic to remote servers**, and then select **Audit all**.

![Screenshot of the audit configuration for outgoing NTLM traffic to remote servers.](../media/advanced-audit-policy-check-step-3.png)

#### Configure domain object auditing

To collect events for object changes, such as for event 4662, you must also configure object auditing on the user, group, computer, and other objects. The following procedure describes how to enable auditing in the Active Directory domain.

To configure domain object auditing:

1. Go to the **Active Directory Users and Computers** console.
2. Select the domain that you want to audit.
3. Select the **View** menu, and then select **Advanced Features**.
4. Right-click the domain and select **Properties**.

    ![Screenshot of selections for opening container properties.](../media/configure-windows-event-collection/container-properties.png)
5. Go to the **Security** tab, and then select **Advanced**.

    ![Screenshot of the dialog for opening advanced security properties.](../media/configure-windows-event-collection/security-advanced.png)
6. In **Advanced Security Settings**, select the **Auditing** tab, and then select **Add**.

    ![Screenshot of the Auditing tab in the Advanced Security Settings dialog.](../media/configure-windows-event-collection/auditing-tab.png)
7. Choose **Select a principal**.

    ![Screenshot of the button for selecting a principal.](../media/configure-windows-event-collection/select-a-principal.png)
8. Under **Enter the object name to select**, enter **Everyone**. Then select **Check Names** &gt; **OK**.

    ![Screenshot of entering an object name of Everyone.](../media/configure-windows-event-collection/select-everyone.png)
9. Go back to **Auditing Entry**. You need to create a separate auditing entry for **each** of the following object types:

    - **Descendant User Objects**
    - **Descendant Group Objects**
    - **Descendant Computer Objects**
    - **Descendant msDS-GroupManagedServiceAccount Objects**
    - **Descendant msDS-ManagedServiceAccount Objects**
    - **Descendant msDS-DelegatedManagedServiceAccount Objects**^1^

    Important

    Auditing must be configured for **all** of the listed object types, not just user objects. Configuring auditing for only one object type results in incomplete detection coverage.

    For each object type, make the following selections:

    1. For **Type**, select **Success**.
    2. For **Applies to**, select the object type from the list.
    3. Under **Permissions**, scroll down and select the **Clear all** button.

        ![Screenshot of the button for clearing all permissions.](../media/clear-all.png)
    4. Scroll back up and select **Full Control**. All the permissions are selected.
    5. Clear the selection for the **List contents**, **Read all properties**, and **Read permissions** permissions, and then select **OK**. This step sets all the **Properties** settings to **Write**.

        ![Screenshot of selecting permissions.](../media/configure-windows-event-collection/select-permissions.png)

        Now, all relevant changes to directory services appear as 4,662 events when they're triggered.

Note

- You can assign auditing permissions to **All descendant objects**, using only the object types detailed in the previous step.
- The **msDS-DelegatedManagedServiceAccount** class is relevant only for domains running at least one Windows Server 2025 domain controller.

#### Configure Object-level auditing on the AD FS configuration folder

To configure object-level auditing on the AD FS configuration folder, complete the following steps:

1. Go to the **Active Directory Users and Computers** console, and select the domain where you want to enable the logs.
2. Go to **Program Data** &gt; **Microsoft** &gt; **ADFS**.

    ![Screenshot of a container for Active Directory Federation Services.](../media/configure-windows-event-collection/adfs-container.png)
3. Right-click **ADFS** and select **Properties**.
4. Go to the **Security** tab and select **Advanced** &gt; **Advanced Security Settings**. Then go to the **Auditing** tab and select **Add** &gt; **Select a principal**.
5. Under **Enter the object name to select**, enter **Everyone**. Then select **Check Names** &gt; **OK**.
6. Return to **Auditing Entry**. Make the following selections:

    - For **Type**, select **All**.
    - For **Applies to**, select **This object and all descendant objects**.
    - Under **Permissions**, scroll down and select **Clear all**. Scroll up and select **Read all properties** and **Write all properties**.

    ![Screenshot of the auditing settings for Active Directory Federation Services.](../media/configure-windows-event-collection/audit-adfs.png)
7. Select **OK**.

### Configure auditing on an AD FS server

The following procedure describes how to modify your Active Directory Federation Services (AD FS) audit configurations for Defender for Identity.

#### Configure a Group Policy for event auditing

To configure Group Policy-based event auditing for AD FS, complete the following steps:

1. Create a group policy to apply to your Active Directory Federation Services (AD FS).
2. Configure the following auditing settings:

    1. Go to **Computer Configuration\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policies\Object Access\Audit Application Generated**.
    2. Select the checkboxes to configure audit events for **Success** and **Failure**.

    ![Screenshot of the advanced auditing audit policy configuration.](media/configure-windows-event-collection/group-policy-management-editor.png)

#### Configure AD FS event auditing in AD FS Management

To enable AD FS event auditing in AD FS Management, complete the following steps:

1. Select **Start** &gt; **Programs** &gt; **Administrative Tools** &gt; **AD FS Management**.
2. Go to **Actions** &gt; **Edit Federation Service Properties**.
3. Select the **Events** tab.
4. Select the **Success audits** and **Failure audits** check boxes.
5. Select **OK**.

    [![Screenshot that shows the Federation service properties page.](media/configure-windows-event-collection/federation-services-dialog.png)](media/configure-windows-event-collection/federation-services-dialog.png#lightbox)

#### Configure Verbose logging for AD FS events

Sensors running on AD FS servers must have the auditing level set to **Verbose** for relevant events.

Use the following PowerShell command to configure the auditing level to **Verbose**:

```powershell
Set-AdfsProperties -AuditLevel Verbose
```

### Configure auditing on an AD CS server

If you're working with a dedicated server that has Active Directory Certificate Services (AD CS) configured, configure auditing as follows to view dedicated alerts and Secure Score reports:

1. Create a group policy to apply to your AD CS server. Edit it and configure the following auditing settings:

    1. Go to **Computer Configuration\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policies\Object Access\Audit Certification Services**.
    2. Select the checkboxes to configure audit events for **Success** and **Failure**.

    ![Screenshot of configuring audit events for Active Directory Certificate Services in the Group Policy Management Editor.](../media/configure-windows-event-collection/group-policy-management-editor.png)
2. Configure auditing on the certificate authority (CA) using one of the following methods:

    - **To configure CA auditing using PowerShell**, set the CA audit filter to enable full auditing and then restart the Certificate Services service for the change to take effect:

```powershell
certutil -setreg CA\AuditFilter 127 
Restart-Service certsvc
```

- **To configure CA auditing in the Defender portal:**

    1. Select **Start** &gt; **Certification Authority (MMC Desktop application)**. Right-click your CA's name and select **Properties**.

        ![Screenshot of the Certification Authority dialog.](../media/configure-windows-event-collection/certification-authority.png)
    2. Select the **Auditing** tab, select all the events that you want to audit, and then select **Apply**.

        ![Screenshot of the Auditing tab for certificate authority properties.](../media/configure-windows-event-collection/auditing.png)

Note

Configuring **Start and Stop Active Directory Certificate Services** event auditing might cause restart delays when you're dealing with a large AD CS database. Consider removing irrelevant entries from the database. Alternatively, don't enable this specific type of event.

### Configure auditing on Microsoft Entra Connect

To configure auditing on Microsoft Entra Connect servers:

1. Create a group policy to apply to your Microsoft Entra Connect servers.
2. Edit the group policy and configure the following auditing settings:

    1. Go to **Computer Configuration\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policies\Logon/Logoff\Audit Logon**.
    2. Select the checkboxes to configure audit events for **Success** and **Failure**.

    ![Screenshot of the Group Policy Management Editor.](media/configure-windows-event-collection/success-and-failure.png)

### Configure auditing on the configuration container

You need the configuration container audit only for environments that currently have or previously had Microsoft Exchange. These environments have an Exchange container located within the domain's Configuration section.

Active Directory replicates the configuration container throughout the forest, so configure auditing once for the entire forest. The health alert might appear for multiple domains because sensors in each domain report the state of the shared configuration container.

1. Open the ADSI Edit tool.
2. Select **Start** &gt; **Run**, enter `ADSIEdit.msc`, and then select **OK**.
3. In the **Action** menu, select **Connect to**.
4. Go to **Connection Settings** &gt; **Select a well known Naming Context**, &gt; **Configuration** and select **OK**.
5. Expand the **Configuration** container to show the **Configuration** node, which begins with **"CN=Configuration,DC=..."**.

    ![Screenshot of selections for opening properties for the CN Configuration node.](../media/cn-configuration.png)
6. Right-click the **Configuration** node and select **Properties**.

    ![Screenshot of selections for opening properties for the Configuration node.](../media/configure-windows-event-collection/configuration-properties.png)
7. Select the **Security** tab, and then select **Advanced**.
8. In **Advanced Security Settings**, select the **Auditing** tab, and then select **Add**.
9. Choose **Select a principal**.
10. Under **Enter the object name to select**, enter **Everyone**. Then select **Check Names** &gt; **OK**.
11. Return to **Auditing Entry**. Make the following selections:

    - For **Type**, select **All**.
    - For **Applies to**, select **This object and all descendant objects**.
    - Under **Permissions**, scroll down and select **Clear all**. Scroll up and select **Write all properties**.

    ![Screenshot of the auditing settings for the Configuration container.](../media/configure-windows-event-collection/audit-configuration.png)
12. Select **OK**.

## Configure Windows event collection using PowerShell

For more information, see the [Defender for Identity PowerShell reference](/en-us/powershell/module/defenderforidentity/new-mdiconfigurationreport):

- [Set-MDIConfiguration](/en-us/powershell/module/defenderforidentity/set-mdiconfiguration)
- [Get-MDIConfiguration](/en-us/powershell/module/defenderforidentity/get-mdiconfiguration)

The following commands show how to modify your domain controller's Audit (Premium) Policy settings for Defender for Identity by using PowerShell.

**To view your audit policies:**

Use the `Get-MDIConfiguration` cmdlet to retrieve the current Defender for Identity configuration values in domain or local machine mode. Use the following syntax to view the current configuration for a specific mode and configuration set:

```powershell
Get-MDIConfiguration [-Mode] <String> [-Configuration] <String[]>
```

Where:

- `Mode` specifies whether to use `Domain` or `LocalMachine` mode. In `Domain` mode, the settings come from the Group Policy objects. In `LocalMachine` mode, the settings come from the local machine.
- `Configuration` specifies which configuration to get. Use `All` to get all configurations.

**To configure your settings:**

Use the following syntax to apply Defender for Identity configuration settings and optionally control GPO creation and linking behavior:

```powershell
Set-MDIConfiguration [-Mode] <String> [-Configuration] <String[]> [-CreateGpoDisabled] [-SkipGpoLink] [-Force]
```

Where:

- `Mode` specifies whether to use `Domain` or `LocalMachine` mode. In `Domain` mode, the settings come from the Group Policy objects. In `LocalMachine` mode, the settings come from the local machine.
- `Configuration` specifies which configuration to set. Use `All` to set all configurations.
- `CreateGpoDisabled` specifies if the GPOs are created and kept as disabled.
- `SkipGpoLink` specifies that GPO links aren't created.
- `Force` specifies that the configuration is set or GPOs are created without validating the current state.

The following example applies all supported Defender for Identity domain configuration settings in one operation, creating the group policy objects and linking them:

```powershell
Set-MDIConfiguration -Mode Domain -Configuration All
```

## Update legacy configurations

Defender for Identity no longer requires logging 1,644 events. If you enabled either of the following settings, remove them from the registry. These registry values configured NTDS diagnostic logging levels and search thresholds that were previously required for event 1644 collection but are no longer needed.

```reg
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics]
"15 Field Engineering"=dword:00000005

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]
"Expensive Search Results Threshold"=dword:00000001
"Inefficient Search Results Threshold"=dword:00000001
"Search Time Threshold (msecs)"=dword:00000001
```