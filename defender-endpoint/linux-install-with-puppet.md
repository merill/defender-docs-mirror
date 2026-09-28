---
layout: Conceptual
title: Deploy Microsoft Defender for Endpoint on Linux with Puppet - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-install-with-puppet
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: gopkr
description: Describes how to deploy Microsoft Defender for Endpoint on Linux using Puppet.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: install-set-up-deploy
ms.subservice: linux
ms.date: 2026-05-21T00:00:00.0000000Z
locale: en-us
document_id: b3182afc-a3a9-0ea3-ec00-6fbcff9de11e
document_version_independent_id: b3182afc-a3a9-0ea3-ec00-6fbcff9de11e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-install-with-puppet.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-install-with-puppet
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-install-with-puppet.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 63a99a3e-f4c1-fc13-6a38-d131dcf96cbd
---

# Deploy Microsoft Defender for Endpoint on Linux with Puppet - Microsoft Defender for Endpoint | Microsoft Learn

You can deploy [Defender for Endpoint on Linux](microsoft-defender-endpoint-linux) by using a variety of tools and methods. This article describes how to deploy Defender for Endpoint on Linux using Puppet. To use another method, refer to the Related content section.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

Important

This article contains information about third-party tools. This is provided to help complete integration scenarios, however, Microsoft does not provide troubleshooting support for third-party tools.  Contact the third-party vendor for support.

## Prerequisites and system requirements

Before you get started, see [Prerequisites for Defender for Endpoint on Linux](mde-linux-prerequisites) for a description of prerequisites and system requirements.

In addition, for Puppet deployment, you need to be familiar with Puppet administration tasks, have Puppet configured, and know how to deploy packages. Puppet has many ways to complete the same task. These instructions assume availability of supported Puppet modules, such as *apt* to help deploy the package. Your organization might use a different workflow. For more information, see [Puppet documentation](https://puppet.com/docs).

## Download the onboarding package

Download the onboarding package from Microsoft Defender portal.

Warning

Repackaging the Defender for Endpoint installation package is not a supported scenario. Doing so can negatively impact the integrity of the product and lead to adverse results, including but not limited to triggering tampering alerts and updates failing to apply.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/) then navigate to **System** &gt; **Settings** &gt; **Endpoints** &gt; **Device management** &gt; **Onboarding**.
2. In the first drop-down menu, select **Linux Server** as the operating system. In the second drop-down menu, select **Your preferred Linux configuration management tool** as the deployment method.
3. Select **Download onboarding package** and save the file as `WindowsDefenderATPOnboardingPackage.zip`.
4. Extract the contents of the archive using the following command:

    ```
    unzip WindowsDefenderATPOnboardingPackage.zip
    ```

    The expected output is:

    ```
    Archive:  WindowsDefenderATPOnboardingPackage.zip
    inflating: mdatp_onboard.json
    ```

## Create a directory structure

You need to create a directory structure for deploying Defender for Endpoint on Linux to devices managed by a Puppet server. This example makes use of the `apt` and `yumrepo` modules available from `puppetlabs`, and assumes that the modules are installed on your Puppet server.

1. Under the **modules** folder if your Puppet installation, create the folders `install_mdatp/files` and `install_mdatp/manifests`. The **modules** folder is typically located at `/etc/puppetlabs/code/environments/production/modules` on your Puppet server.
2. Copy the `mdatp_onboard.json` file created earlier to the `install_mdatp/files` folder.
3. Create an `init.pp` file that contains the deployment instructions:

    ```bash
    pwd
    ```

    ```console
    /etc/puppetlabs/code/environments/production/modules
    ```

    ```bash
    tree install_mdatp
    ```

    ```console
    install_mdatp
    ├── files
    │   └── mdatp_onboard.json
    └── manifests
        └── init.pp
    ```

## Create a Puppet manifest

There are two ways to create a manifest file:

- Use an installer script; or
- Configure your repositories manually.

#### Create a manifest to deploy Defender for Endpoint using an installer script

1. Download the installer bash script. Pull the [installer bash script](https://github.com/microsoft/mdatp-xplat/blob/master/linux/installation/mde_installer.sh) from Microsoft GitHub Repository or use the following command to download it.

```bash
wget https://raw.githubusercontent.com/microsoft/mdatp-xplat/refs/heads/master/linux/installation/mde_installer.sh /etc/puppetlabs/code/environments/production/modules/install_mdatp/files/
```

1. Add the following content to the `install_mdatp/manifests/init.pp` file. You can also download the file directly from [GitHub](https://github.com/microsoft/mdatp-xplat/blob/master/linux/installation/third_party_installation_playbooks/puppet.install_mdatp_simplified.init.pp)

```bash

# Puppet manifest to install Microsoft Defender for Endpoint on Linux.
# @param channel The release channel based on your environment, insider-fast or prod.

class install_mdatp (
  $channel = 'prod',
) {
  # Ensure that the directory /tmp/mde_install exists
  file { '/tmp/mde_install':
    ensure => directory,
    mode   => '0755',
  }

  # Copy the installation script to the destination
  file { '/tmp/mde_install/mde_installer.sh':
    ensure => file,
    source => 'puppet:///modules/install_mdatp/mde_installer.sh',
    mode   => '0777',
  }

  # Copy the onboarding script to the destination
  file { '/tmp/mde_install/mdatp_onboard.json':
    ensure => file,
    source => 'puppet:///modules/install_mdatp/mdatp_onboard.json',
    mode   => '0777',
  }

  # Install MDE on the host using an external script
  exec { 'install_mde':
    command     => "/tmp/mde_install/mde_installer.sh --install --channel ${channel} --onboard /tmp/mde_install/mdatp_onboard.json",
    path        => '/bin:/usr/bin',
    user        => 'root',
    logoutput   => true,
    require     => File['/tmp/mde_install/mde_installer.sh', '/tmp/mde_install/mdatp_onboard.json'], # Ensure the script is copied before running the installer
  }

}
```

Note

The installer script also supports other parameters such as channel, realtime protection, version, custom location installation etc. To select from the list of available options, check help: `./mde_installer.sh --help`

#### Create a manifest to deploy Defender for Endpoint by configuring repositories manually

Add the following content to the `install_mdatp/manifests/init.pp` file. You can also download it from [GitHub](https://github.com/microsoft/mdatp-xplat/blob/master/linux/installation/third_party_installation_playbooks/puppet.install_mdatp_manual.init.pp).

```bash
# Puppet manifest to install Microsoft Defender for Endpoint on Linux.
# @param channel The release channel based on your environment, insider-fast or prod.

class install_mdatp::configure_debian_repo (
  String $channel,
  String $distro,
  String $version ) {
  # Configure the APT repository for Debian-based systems

  $release = $channel ? {
    'prod'  => $facts['os']['distro']['codename'],
    default => $channel
    }
  
  apt::source { 'microsoftpackages':
    location => "https://packages.microsoft.com/${distro}/${version}/prod",
    release  => $release,
    repos    => 'main',
    key      => {
      'id'     => 'BC528686B50D79E339D3721CEB3E94ADBE1229CF',
      'server' => 'keyserver.ubuntu.com',
    },
  }
}

class install_mdatp::configure_redhat_repo (
  String $channel,
  String $distro,
  String $version) {
  # Configure the Yum repository for RedHat-based systems
  
  yumrepo { 'microsoftpackages':
    baseurl  => "https://packages.microsoft.com/rhel/${version}/prod",
    descr    => 'packages-microsoft-com-prod',
    enabled  => 1,
    gpgcheck => 1,
    gpgkey   => 'https://packages.microsoft.com/keys/microsoft.asc',
  }
}

class install_mdatp::install {
  # Common configurations for both Debian and RedHat
  
  file { ['/etc/opt', '/etc/opt/microsoft', '/etc/opt/microsoft/mdatp']:
    ensure  => directory,
    owner   => 'root',
    group   => 'root',
    mode    => '0755',
  }

  file { '/etc/opt/microsoft/mdatp/mdatp_onboard.json':
    source  => 'puppet:///modules/install_mdatp/mdatp_onboard.json',
    owner   => 'root',
    group   => 'root',
    mode    => '0600',
    require => File['/etc/opt/microsoft/mdatp'],
  }

  # Install mdatp package
  package { 'mdatp':
    ensure  => installed,
    require => [
      File['/etc/opt/microsoft/mdatp/mdatp_onboard.json'],
    ],
  }
}

class install_mdatp (
  $channel = 'prod'
) {
  # Include the appropriate class based on the OS family
  
  $distro = downcase($facts['os']['name'])
  $version = $facts['os']['release']['major']
  
  case $facts['os']['family'] {
    'Debian': {
      class { 'install_mdatp::configure_debian_repo':
        channel => 'prod',
        distro => $distro,
        version => $version
        } -> class { 'install_mdatp::install': }
    }
    'RedHat': {
      class { 'install_mdatp::configure_redhat_repo':
        channel => 'prod',
        distro => $distro,
        version => $version,
        } -> class { 'install_mdatp::install': }
    }
    default: { fail("${facts['os']['family']} is currently not supported.")}
  }
}

```

Note

Defender for Endpoint on Linux can be deployed from one of the following channels: **insiders-fast, insiders-slow, prod**. Each channel corresponds to a Linux software repository. The choice of the channel determines the type and frequency of the updates that are offered to your device. Devices in `insiders-fast` are the first ones to receive updates and new features in preview, followed by `insiders-slow`, and lastly by `prod`. Note your distribution and version and identify the closest entry for it under `https://packages.microsoft.com/config/[distro]/[version]`.

Warning

Switching the channel after the initial installation requires the product to be reinstalled. To switch the product channel: uninstall the existing package, re-configure your device to use the new channel, and follow the steps in this document to install the package from the new location.

## Include the manifest inside the site.pp file

Include the manifest described earlier in this article in your `site.pp` file:

```bash
cat /etc/puppetlabs/code/environments/production/manifests/site.pp
```

```console
node "default" {
    include install_mdatp
}
```

Enrolled agent devices periodically poll the Puppet Server and install new configuration profiles and policies as soon as they're detected.

## Monitor your Puppet deployment

On the agent device, you can also check the deployment status by running the following command:

```bash
mdatp health
```

```console
...
healthy                                 : true
health_issues                           : []
licensed                                : true
org_id                                  : "[your organization identifier]"
...
```

- `healthy`: Confirm that Defender for Endpoint is successfully deployed and operational.
- `health_issues`: States the issues which caused the healthy status to become false.
- `licensed`: Confirms that the device is tied to your organization.
- `orgId`: Your Defender for Endpoint organization identifier.

## Troubleshoot installation issues

If you experience any installation issues, for self-troubleshooting, follow these steps:

1. For information on how to find the log that's generated automatically when an installation error occurs, see [Log installation issues](linux-resources#log-installation-issues).
2. For information about common installation issues, see [Installation issues](linux-support-install).
3. If health of the device is `false`, see [Defender for Endpoint agent health issues](health-status).
4. For product performance issues, see [Troubleshoot performance issues](linux-support-perf).
5. For proxy and connectivity issues, see [Troubleshoot cloud connectivity issues](linux-support-connectivity).

To get support from Microsoft, open a support ticket, and provide the log files created by using the [client analyzer](overview-client-analyzer).

## How to configure policies for Microsoft Defender on Linux

To configure antivirus and EDR settings, see the following articles:

- [Defender for Endpoint security settings management](/en-us/intune/intune-service/protect/mde-security-integration) describes how to configure settings in the Microsoft Defender portal. (*This method is recommended*.)
- [Set preferences for Defender for Endpoint on Linux](linux-preferences) describes settings you can configure.

## Operating system upgrades

When upgrading your operating system to a new major version, you must first uninstall Defender for Endpoint on Linux, install the upgrade, and then reconfigure Defender for Endpoint on Linux on your device.

## Uninstallation

Create a module `remove_mdatp` similar to `install_mdatp` with the following contents in `init.pp` file:

```bash
class remove_mdatp {
    package { 'mdatp':
        ensure => 'purged',
    }
}
```