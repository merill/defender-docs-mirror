---
layout: Conceptual
title: Reference table for all deprecated security recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/recommendations-reference-deprecated
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
description: This article lists all Microsoft Defender for Cloud deprecated security recommendations that help you harden and protect your resources.
ms.topic: reference
ms.date: 2026-06-23T00:00:00.0000000Z
ms.custom: generated
ai-usage: ai-assisted
locale: en-us
document_id: 4bcb64b0-bc94-f117-5211-7e435deab387
document_version_independent_id: b2f14d18-1470-94b0-7c22-16aa772e060b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/recommendations-reference-deprecated.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/recommendations-reference-deprecated
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/recommendations-reference-deprecated.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 93075d7b-487a-342c-c4ce-9ba612e400d6
---

# Reference table for all deprecated security recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

This article lists all the deprecated security recommendations in Microsoft Defender for Cloud.

## Azure deprecated recommendations

### Access to App Services should be restricted

**Description & related policy**: Restrict access to your App Services by changing the networking configuration, to deny inbound traffic from ranges that are too broad. (Related policy: [Preview]: Access to App Services should be restricted).

**Severity**: High

### Endpoint protection health issues on machines should be resolved

**Description**: Resolve endpoint protection health issues on your virtual machines to protect them from latest threats and vulnerabilities. See the documentation for the [endpoint protection solutions supported by Defender for Cloud](supported-machines-endpoint-solutions-clouds#supported-endpoint-protection-solutions-) and the [endpoint protection assessments](endpoint-protection-recommendations-technical). (No related policy)

**Severity**: Medium

### Endpoint protection should be installed on machines

**Description**: To protect machines from threats and vulnerabilities, install a supported endpoint protection solution. Learn more about how endpoint protection for machines is evaluated in [Endpoint protection assessment and recommendations in Microsoft Defender for Cloud](endpoint-protection-recommendations-technical). (No related policy)

**Severity**: High

### Install Azure Security Center for IoT security module to get more visibility into your IoT devices

**Description & related policy**: Install Azure Security Center for IoT security module to get more visibility into your IoT devices.

**Severity**: Low

### Java should be updated to the latest version for function apps

**Description & related policy**: Periodically, newer versions are released for Java software either due to security flaws or to include additional functionality. Using the latest Java version for function apps is recommended to benefit from security fixes, if any, and/or new functionalities of the latest version. (Related policy: Ensure that 'Java version' is the latest, if used as a part of the Function app).

**Severity**: Medium

### Java should be updated to the latest version for web apps

**Description & related policy**: Periodically, newer versions are released for Java software either due to security flaws or to include additional functionality. Using the latest Java version for web apps is recommended to benefit from security fixes, if any, and/or new functionalities of the latest version. (Related policy: Ensure that 'Java version' is the latest, if used as a part of the Web app).

**Severity**: Medium

### Monitoring agent should be installed on your machines

**Description & related policy**: This action installs a monitoring agent on the selected virtual machines. Select a workspace for the agent to report to. (No related policy)

**Severity**: High

### PHP should be updated to the latest version for web apps

**Description & related policy**: Periodically, newer versions are released for PHP software either due to security flaws or to include additional functionality. Using the latest PHP version for web apps is recommended to benefit from security fixes, if any, and/or new functionalities of the latest version. (Related policy: Ensure that 'PHP version' is the latest, if used as a part of the WEB app).

**Severity**: Medium

### Pod Security Policies should be defined to reduce the attack vector by removing unnecessary application privileges (Preview)

**Description & related policy**: Define Pod Security Policies to reduce the attack vector by removing unnecessary application privileges. It is recommended to configure pod security policies so pods can only access resources which they are allowed to access. (Related policy: [Preview]: Pod Security Policies should be defined on Kubernetes Services).

**Severity**: Medium

### Public network access should be disabled for Cognitive Services accounts

**Description**: This policy audits any Cognitive Services account in your environment with public network access enabled. Public network access should be disabled so that only connections from private endpoints are allowed. (Related policy: [Public network access should be disabled for Cognitive Services accounts](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f0725b4dd-7e76-479c-a735-68e7ee23d5ca)).

**Severity**: Medium

### Python should be updated to the latest version for function apps

**Description & related policy**: Periodically, newer versions are released for Python software either due to security flaws or to include additional functionality. Using the latest Python version for function apps is recommended to benefit from security fixes, if any, and/or new functionalities of the latest version. (Related policy: Ensure that 'Python version' is the latest, if used as a part of the Function app).

**Severity**: Medium

### Python should be updated to the latest version for web apps

**Description & related policy**: Periodically, newer versions are released for Python software either due to security flaws or to include additional functionality. Using the latest Python version for web apps is recommended to benefit from security fixes, if any, and/or new functionalities of the latest version. (Related policy: Ensure that 'Python version' is the latest, if used as a part of the Web app).

**Severity**: Medium

### The rules for web applications on IaaS NSGs should be hardened

**Description & related policy**: Harden the network security group (NSG) of your virtual machines that are running web applications, with NSG rules that are overly permissive with regard to web application ports. (Related policy: The NSGs rules for web applications on IaaS should be hardened).

**Severity**: High

### Your machines should be restarted to apply system updates

**Description & related policy**: Restart your machines to apply the system updates and secure the machine from vulnerabilities. (Related policy: System updates should be installed on your machines).

**Severity**: Medium

### MFA should be enabled on accounts with owner permissions on subscriptions

**Description**: Multifactor authentication (MFA) should be enabled for all subscription accounts with owner permissions to prevent a breach of accounts or resources. (Related policy: [MFA should be enabled on accounts with owner permissions on your subscription](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2faa633080-8b72-40c4-a2d7-d00c03e80bed)).

**Severity**: High

### MFA should be enabled on accounts with read permissions on subscriptions

**Description**: Multifactor authentication (MFA) should be enabled for all subscription accounts with read privileges to prevent a breach of accounts or resources. (Related policy: [MFA should be enabled on accounts with read permissions on your subscription](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2fe3576e28-8b17-4677-84c3-db2990658d64)).

**Severity**: High

### MFA should be enabled on accounts with write permissions on subscriptions

**Description**: Multifactor authentication (MFA) should be enabled for all subscription accounts with write privileges to prevent a breach of accounts or resources. (Related policy: [MFA should be enabled accounts with write permissions on your subscription](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f9297c21d-2ed6-4474-b48f-163f75654ce3)).

**Severity**: High

### Containers should only use allowed AppArmor profiles

**Description**: Containers running on Kubernetes clusters should be limited to allowed AppArmor profiles only. AppArmor (Application Armor) is a Linux security module that protects an operating system and its applications from security threats. To use it, a system administrator associates an AppArmor security profile with each program. (Related policy: [Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f511f5417-5d12-434d-ab2e-816901e72a5e)).

**Severity**: High

**Type**: Kubernetes data plane

### Kubernetes clusters should not grant CAPSYSADMIN security capabilities

**Description**: To reduce the attack surface of your containers, restrict CAP\_SYS\_ADMIN Linux capabilities. For more information, see https://aka.ms/kubepolicydoc. (No related policy)

**Severity**: High

**Type**: Kubernetes data plane

### Services should listen on allowed ports only

**Description**: To reduce the attack surface of your Kubernetes cluster, restrict access to the cluster by limiting services access to the configured ports. (Related policy: [Ensure services listen only on allowed ports in Kubernetes cluster](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f233a2a17-77ca-4fb1-9b6b-69223d272a44)).

**Severity**: Medium

**Type**: Kubernetes data plane

### Usage of host networking and ports should be restricted

**Description**: Restrict pod access to the host network and the allowable host port range in a Kubernetes cluster. Pods created with the hostNetwork attribute enabled will share the node's network space. To avoid compromised container from sniffing network traffic, we recommend not putting your pods on the host network. If you need to expose a container port on the node's network, and using a Kubernetes Service node port does not meet your needs, another possibility is to specify a hostPort for the container in the pod spec. (Related policy: [Kubernetes cluster pods should only use approved host network and port range](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f82985f06-dc18-4a48-bc1c-b9f4f0098cfe)).

**Severity**: Medium

**Type**: Kubernetes data plane

### Usage of pod HostPath volume mounts should be restricted to a known list to restrict node access from compromised containers

**Description**: We recommend limiting pod HostPath volume mounts in your Kubernetes cluster to the configured allowed host paths. If there's a compromise, the container node access from the containers should be restricted. (Related policy: [Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f098fc59e-46c7-4d99-9b16-64990e543d75)).

**Severity**: Medium

**Type**: Kubernetes data plane