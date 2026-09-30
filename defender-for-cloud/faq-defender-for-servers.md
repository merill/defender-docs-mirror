---
layout: FAQ
title: Common questions - Defender for Servers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-defender-for-servers
summary: >
  <p>Get answers to common questions about Microsoft Defender for Servers.</p>
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
description: Get answers to frequently asked questions about Microsoft Defender for Servers.
ms.topic: faq
ms.date: 2026-06-09T00:00:00.0000000Z
locale: en-us
document_id: 27311548-4fee-6cf7-791e-8b3b07749108
document_version_independent_id: b484d8ec-ad01-0c58-0609-2a0d559b3ff5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-defender-for-servers.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-defender-for-servers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-defender-for-servers.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 7bd1b969-08e0-e36d-008e-97170cf2c136
---

# Common questions - Defender for Servers - Microsoft Defender for Cloud | Microsoft Learn

Get answers to common questions about Microsoft Defender for Servers.

## Pricing

### What servers do I pay for in a subscription?

When you enable Defender for Servers on a subscription, you're charged for all machines based on their power states. For more information, see [Upcoming billing updates for Defender for Servers](https://aka.ms/D4ServersUpcomingBillingPolicyChange).

| State | Details | Billing |
| --- | --- | --- |
| **Azure VMs** |  |  |
| Starting | VM starting up. | Billed |
| Running | Normal working state. | Billed |
| Stopping | Transitional. Moves to Stopped state when finished. | Billed |
| Stopped | VM shut down from within guest OS or by using PowerOff APIs. Hardware is still allocated, and the machine remains on the host. | Billed |
| Deallocating | Transitional. Moves to Deallocated state when finished. | Not billed |
| Deallocated | VM stopped and removed from the host. | Not billed |
| **Azure Arc machines** |  |  |
| Connecting | Servers connected, but heartbeat not yet received. | Not billed |
| Connected | Receiving regular heartbeat from Connected Machine agent. | Billed |
| Offline/Disconnected | No heartbeat received in 15-30 minutes. | Not billed |
| Expired | If disconnected for 45 days, status might change to Expired. | Not billed |
| **Direct onboarding (Defender for Endpoint only)** |  |  |
| Sensor connected | Server is directly onboarded to Defender for Cloud through the Defender for Endpoint sensor connection model. | Billed per hour |

If you already have standalone Microsoft Defender for Endpoint for Servers licenses, submit a support request to apply the billing adjustment and avoid double billing. For steps, see Can I get a discount if I already have a Microsoft Defender for Endpoint license?.

### What are the licensing requirements for Microsoft Defender for Endpoint?

Licenses for Defender for Endpoint for Servers are included with Defender for Servers.

### Can I get a discount if I already have a Microsoft Defender for Endpoint license?

If you already have a license for **Microsoft Defender for Endpoint for Servers**, you don't pay for that part of your Microsoft Defender for Servers Plan 1 (P1) or 2 (P2) license.

1. To request your discount, in the Azure portal, select **Support and Troubleshooting** &gt; **Help + support**. Select **Create a support request** and fill in the fields.

    ![Screenshot that shows the support ticket description with the information filled out.](media/faq-defender-for-servers/support-ticket-description.png)
2. In *Additional details*, enter details, tenant ID, the number of Defender for Endpoint licenses that were purchased, the expiration date, and all other required fields.
3. Complete the process and select **Create**.

The discount becomes effective starting on the approval date. It isn't retroactive.

### What's the free data ingestion allowance?

When Defender for Servers Plan 2 is enabled you get a free data ingestion allowance for specific data types. [Learn more](data-ingestion-benefit)

## Deployment

### Can I enable Defender for Servers on a subset of machines in a subscription?

Yes you can enable Defender for Servers on specific resources in a subscription. Learn more about [planning deployment scope](plan-defender-for-servers-select-plan).

### How does Defender for Servers collect data?

Learn about [data collection methods in Defender for Servers](plan-defender-for-servers-agents).

### Where does Defender for Servers store my data?

Learn about [data residency for Defender for Cloud](plan-defender-for-servers-data-workspace).

### Does Defender for Servers need a Log Analytics workspace?

Defender for Servers Plan 1 doesn't depend on Log Analytics. In Defender for Servers Plan 2, you need a Log Analytics workspace to take advantage of the [free data ingestion benefit](data-ingestion-benefit). You also need a workspace to use [file integrity monitoring](file-integrity-monitoring-overview) in Plan 2. If you do set up a Log Analytics workspace for the free data ingestion benefit, you need to [enable Defender for Servers Plan 2](data-ingestion-benefit#configure-a-workspace) directly on it.

### What if I have Defender for Servers enabled on a workspace but not on a subscription?

The [legacy method for onboarding servers to Defender for Servers Plan 2](quickstart-onboard-machines) using a workspace and the Log Analytics agent is no longer supported or available in the portal. To ensure that machines that are currently connected to the workspace remain protected, do the following:

- **On-premises and multicloud machines**: If you previously onboarded on-premises and AWS/GCP machines using the legacy method, [connect these machines to Azure](/en-us/azure/azure-arc/servers/deployment-options) as Azure Arc-enabled servers to the subscription with Defender for Servers Plan 2 enabled.
- **Selected machines**: If you used the legacy method to enable Defender for Servers Plan 2 on individual machines, we recommend that you enable Defender for Server Plan 2 on the entire subscription. Then you can exclude specific machines using [resource-level configuration](plan-defender-for-servers-select-plan).

### Does disabling Defender for Servers Plan 2 automatically remove the plan from my workspace?

Disabling the Defender for Servers Plan 2 on your subscription doesn't automatically disable the plan on your workspace. If Defender for Servers Plan 2 is enabled on a workspace, you need to manually disable it in the workspace settings to stop data collection and turn off the feature.

Learn how to [disable the Defender for Servers plan](tutorial-enable-servers-plan#disable-defender-for-servers-on-a-subscription).

## Defender for Endpoint integration

### Which Microsoft Defender for Endpoint plan is supported in Defender for Servers?

Defender for Servers Plan 1 and Plan 2 provides the capabilities of [Microsoft Defender for Endpoint Plan 2](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint), including endpoint detection and response (EDR).

### Do I need to buy a separate anti-malware solution for my machines?

No. With Defender for Endpoint integration in Defender for Servers, you'll also get malware protection on your machines. In addition, Defender for Servers Plan 2 provides [agentless malware scanning](agentless-malware-scanning).

On new Windows Server operating systems, Microsoft Defender Antivirus is part of the operating system and will be enabled in *active mode*. For machines running Windows Server with the Defender for Endpoint unified solution integration enabled, Defender for Servers deploys [Defender Antivirus](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-antivirus-windows) in *active mode*. On Linux, Defender for Servers deploys Defender for Endpoint including the anti-malware component, and set the component in *passive mode*.

### How do I switch from a non-Microsoft EDR tool?

Full instructions for switching from a non-Microsoft endpoint solution are available in the Microsoft Defender for Endpoint documentation: [Migration overview](/en-us/windows/security/threat-protection/microsoft-defender-atp/switch-to-microsoft-defender-migration).

### What's the "MDE.Windows" / "MDE.Linux" extension running on my machines?

When you turn on the Defender for Servers plan in a subscription, the native Defender for Endpoint integration in Defender for Cloud automatically deploys the Defender for Endpoint agent on supported machines in the subscription as needed. Automatic onboarding installs the MDE.Windows/MDE.Linux extension.

If the extension isn't showing, check that the machine meets the [prerequisites](enable-defender-for-endpoint#prerequisites), and that Defender for Servers is enabled.

Important

If you delete the **MDE.Windows**/**MDE.Linux** extension, it won't remove Microsoft Defender for Endpoint. Learn about [offboard Windows servers from Defender for Endpoint](/en-us/defender-endpoint/configure-server-endpoints#offboard-windows-servers).

## Machine support and scanning

### What types of virtual machines do Defender for Servers support?

Review [Windows](support-matrix-defender-for-servers#windows-machine-support) and [Linux](/en-us/defender-endpoint/microsoft-defender-endpoint-linux) machines that are supported for Defender for Endpoint integration.

### How often does Defender for Cloud scan for operating system vulnerabilities, system updates, and endpoint protection issues?

System updates interpretation occurs every 12 hours and every 24 hours for agentless endpoint protection platform.

Defender for Cloud typically scans for new data every hour, and refreshes security recommendations accordingly.

### What is endpoint protection platform (EPP)?

Microsoft Defender for Servers, EPP refers to the core set of security capabilities that protect endpoints (like servers) from threats. These capabilities are typically delivered through Microsoft Defender for Endpoint.

When you enable Microsoft Defender for Servers, it integrates with Microsoft Defender for Endpoint to provide EPP capabilities. This integration allows Defender for Cloud to access data about vulnerabilities, installed software, and alerts from your endpoints.

### How are VM snapshots collected by agentless scanning secured?

Agentless scanning protects disk snapshots according to Microsoft's highest security standards. Security measures include:

- Data is encrypted at rest and in-transit.
- Snapshots are immediately deleted when the analysis process is complete.
- Snapshots remain within their original AWS or Azure region. EC2 snapshots aren't copied to Azure.
- Isolation of environments per customer account/subscription.
- Only metadata containing scan results is sent outside the isolated scanning environment.
- All operations are audited.

### What is the auto-provisioning feature for vulnerability scanning with a "bring your own license" (BYOL) solution? Can it be applied on multiple solutions?

Defender for Servers can scan machines to see if they have an EDR solution enabled. If they don't, you can use Microsoft Defender Vulnerability Management that's integrated by default into Defender for Cloud. As an alternative, Defender for Cloud can deploy a supported non-Microsoft BYOL vulnerability scanner. You can only use a single BYOL scanner. Multiple non-Microsoft scanners aren't supported.

### Does the integrated Defender for Vulnerability Management scanner find network vulnerabilities?

No, it only finds vulnerabilities on the machine itself.

### Why do I get the message "Missing scan data" for my VM?

This message appears when there's no scan data for a VM. It takes around an hour or less to scan data after a data collection method is enabled. After the initial scan, you might receive this message because there's no scan data available. For example, scans don't populate for a VM that's stopped. This message might also appear if scan data hasn't populated recently.

### Why is a machine shown as not applicable?

The list of resources in the **Not applicable** tab includes a **Reason** column

| Reason | Details |
| --- | --- |
| **No scan data available on the machine** | There aren't any compliance results for this machine in Azure Resource Graph. All compliance results are written to Azure Resource Graph by the Azure machine configuration extension. You can check the data in Azure Resource Graph using the [sample Resource Graph queries][(/azure/governance/policy/samples/resource-graph-samples?tabs=azure-cli#azure-policy-guest-configuration). |
| **Azure machine configuration extension isn't installed on the machine** | The machine is missing the extension, which is a prerequisite for assessing compliance against the Microsoft Cloud Security Baseline. |
| **System managed identity isn't configured on the machine** | A system-assigned, managed identity must be deployed on the machine. |
| **The recommendation is disabled in policy** | The policy definition that assesses the OS baseline is disabled on the scope that includes the |