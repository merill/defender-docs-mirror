---
layout: Conceptual
title: Defender for Endpoint integration in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/integration-defender-for-endpoint
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
description: Learn about how Microsoft Defender for Endpoint and Microsoft Defender Vulnerability Management integrate with Defender for Cloud to enhance security.
ms.topic: concept-article
ms.date: 2026-06-17T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 83b60015-fb32-da34-8ea2-399cfd8f05e8
document_version_independent_id: 00ce9dbd-f73d-f6a2-6ec2-600f4a286391
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/integration-defender-for-endpoint.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/integration-defender-for-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/integration-defender-for-endpoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 54c67a4e-8865-00cb-1f50-d5b56eb9c3bf
---

# Defender for Endpoint integration in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Endpoint and Microsoft Defender Vulnerability Management integrate natively with Defender for Cloud to provide:

- **Integrated security capabilities**: Security capabilities provided by Defender for Endpoint, Defender Vulnerability Management, and Defender for Cloud come together to provide end-to-end protection for machines protected by the Defender for Servers plan.
- **Licensing**: Defender for Servers licensing entitles customers with the same benefits on their servers as Defender for Endpoint Plan 2 provides on client endpoints. Licensing is charged per hour instead of per user, reducing costs by protecting VMs only when they're in use.

    - If you already have licenses for Microsoft Defender for Endpoint for Servers and also use Defender for Servers, request the billing discount to avoid double billing. For steps, see [Can I get a discount if I already have a Microsoft Defender for Endpoint license?](faq-defender-for-servers#can-i-get-a-discount-if-i-already-have-a-microsoft-defender-for-endpoint-license-).
- **Agent provisioning**: Defender for Cloud can automatically provision the Defender for Endpoint sensor on supported machines connected to Defender for Cloud.
- **Unified alerts**: Alerts and vulnerability data from Defender for Endpoint appear in Defender for Cloud in the Azure portal. You can move to the Defender portal to drill down for detailed alert information and context.

## Security capabilities

Defender for Cloud integrates security capabilities provided by Defender for Endpoint and Defender Vulnerability Management.

- **Vulnerability management**: Provided by [Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management).

    - Features include an [inventory of known software](/en-us/defender-vulnerability-management/tvm-software-inventory), [continuous vulnerability assessment and insights](/en-us/defender-vulnerability-management/tvm-weaknesses), [secure score for devices](/en-us/defender-vulnerability-management/tvm-microsoft-secure-score-devices), [prioritized security recommendations](/en-us/defender-vulnerability-management/tvm-security-recommendation), and [vulnerability remediation](/en-us/defender-vulnerability-management/tvm-remediation).
    - Integration with Defender Vulnerability Management also provides [premium features](/en-us/defender-vulnerability-management/defender-vulnerability-management-capabilities) in Defender for Servers Plan 2.
- **Attack surface reduction**: Use of [attack surface reduction rules](/en-us/defender-endpoint/attack-surface-reduction) to reduce security exposure.
- **Next-generation protection** providing [antimalware and antivirus protection](/en-us/defender-endpoint/next-generation-protection).
- **Endpoint detection and response (EDR)**: EDR [detects, investigates, and responds to advanced threats](/en-us/defender-endpoint/overview-endpoint-detection-response), including [advanced threat hunting](/en-us/defender-xdr/advanced-hunting-overview), and [automatic investigation and remediation capabilities](/en-us/defender-xdr/m365d-autoir).
- **Threat analytics**. [Get threat intelligence data](/en-us/defender-xdr/threat-analytics) provided by Microsoft threat hunters and security teams, augmented by intelligence provided by partners. Security alerts are generated when Defender for Endpoint identifies attacker tools, techniques, and procedures.

## Integration architecture

Defender for Endpoint automatically creates a tenant when you use Defender for Cloud to monitor your machines.

Defender for Endpoint stores collected data in the tenant's geo-location as identified during provisioning.

- Customer data, in pseudonymized form, might also be stored in the central storage and processing systems in the United States.
- After you configure the location, you can't change it.
- If you have your own license for Defender for Endpoint and need to move your data to another location, [contact Microsoft support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) to reset the tenant.

### Resource discovery and onboarding status

Defender for Cloud can discover machines independently of Microsoft Defender for Endpoint onboarding.

Machines that exist in Azure, Azure Arc–enabled environments, or connected multicloud accounts (AWS, GCP) are identified by Defender for Cloud through its native resource discovery processes. These machines can appear in the Defender for Endpoint device inventory even before the Defender for Endpoint sensor is installed and reporting.

In this state, devices may show Defender for Cloud as the discovery source and a status of **Can be onboarded**, indicating that the machine is known to Defender for Cloud but isn’t yet onboarded to Defender for Endpoint. Onboarding occurs only after the Defender for Endpoint sensor is deployed and successfully reports to the service.

## Move between subscriptions

You can move Defender for Endpoint for servers between subscriptions in the same tenant or between different tenants.

- **Move to a different subscription in the same tenant**: To move your Defender for Endpoint for servers extension to a different subscription in the same tenant, delete either the `MDE.Linux` or `MDE.Windows` extension from the virtual machine. Defender for Cloud will automatically redeploy it.
- **Move subscriptions between tenants:** If you move your Azure subscription between Azure tenants, some manual preparatory steps are required before Defender for Cloud deploys Defender for Endpoint. For full details, [contact Microsoft support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).

## Health status for Defender for Endpoint

Defender for Servers provides visibility to the Defender for Endpoint agents installed on your VMs.

### Prerequisites

You must have either:

- Defender for Servers P2 enabled.  or,
- Defender cloud security posture management (Defender CSPM) enabled with Defender for Servers Plan 1 enabled.

### Visibility into health issues in Defender for Servers

Defender for Servers provides visibility into two main types of health issues:

- **Installation Issues**: Errors during the agent's installation.
- **Heartbeat Issues**: Problems where the agent is installed but not reporting correctly.

In some situations, Defender for Endpoint doesn't apply to certain machines, such as when a client operating system is installed. These devices need coverage from a Defender for Endpoint user license, such as Microsoft 365 E5. This status is also shown as described in the last query.

Defender for Servers shows specific error messages for each issue type. These messages explain the problem. When available, you'll also find instructions to fix the issue.

Health status updates every four hours. This ensures the issue reflects the state from the last four hours.

To see Defender for Endpoint health issues, use the security explorer as follows:

- To find all the unhealthy virtual machines (VMs) with the issues mentioned, run the query shown in the following screenshot:

    [![Screenshot of query of unhealthy virtual machines.](media/integration-defender-for-endpoint/unhealthy-virtual-machines-query.png)](media/integration-defender-for-endpoint/unhealthy-virtual-machines-query.png#lightbox)
- Another way to access this data is shown in the following screenshot:

    [![Screenshot of alternate query of unhealthy virtual machines.](media/integration-defender-for-endpoint/unhealthy-virtual-machines-alternate-query.png)](media/integration-defender-for-endpoint/unhealthy-virtual-machines-query.png#lightbox)
- To find all the healthy VMs where Defender for Endpoint works correctly, run the query shown in the following screenshot:

    [![Screenshot of query of healthy virtual machines.](media/integration-defender-for-endpoint/healthy-virtual-machines-query.png)](media/integration-defender-for-endpoint/healthy-virtual-machines-query.png#lightbox)
- To get the list of VMs where Defender for Endpoint isn't applicable, run the query shown in the following screenshot:

    [![Screenshot of query of virtual machines where Defender for Endpoint isn't applicable.](media/integration-defender-for-endpoint/not-applicable-virtual-machines-query.png)](media/integration-defender-for-endpoint/not-applicable-virtual-machines-query.png#lightbox)