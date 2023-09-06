---
title: Vagrant on Windows
keywords: sample
summary: Vagrant with Oracle VirtualBox or Microsoft Hyper-V
sidebar: product2_sidebar
permalink: p2_sample1.html
---

# Vagrant

CDAF Vagrant boxes support VirtualBox and Hyper-V. Previously Hyper-V on a workstation did not have a native NAT network support, however, it now does, making it more functionally equivalent to VirtualBox. Using Administrator PowerShell session.

    . { iwr -useb https://raw.githubusercontent.com/cdaf/windows/master/install.ps1 } | iex
    ./automation/provisioning/base.ps1 vagrant

## VirtualBox

Oracle VirtualBox

    ./automation/provisioning/base.ps1 virtualbox

## Hyper-V

Install from the Windows features

    Dism /online /enable-feature /all /featurename:Microsoft-Hyper-V

# Create Desktop Environment

To create a desktop environment, navigate to the solution root and run:

    vagrant up
    
## Continuous Delivery Testing

Once the environment is running access the build server an execute the CD emulation. Note: On a Linux host bash Python WINRM can be used to provide native PowerShell access.

    vagrant powershell buildserver
    cd C:\vagrant
    .\automation\cdEmulate.bat

## Direct PowerShell Access

To access the buildserver using native remote PowerShell.
Allow credential delegation, on-off step needed on the host when using VirtualBox/Vagrant. 

    ./automation/provisioning/runner.bat CredSSP.ps1 client

Once delegation configured, the build emulation can be executed.

    $securePassword = ConvertTo-SecureString 'vagrant' -asplaintext -force
    $cred = New-Object System.Management.Automation.PSCredential ('vagrant', $securePassword)
    enter-pssession 127.0.0.1 -port 15985 -Auth CredSSP -credential $cred
    cd C:\vagrant
	.\automation\cdEmulate.bat

## Cleanup and Destroy

If change made that need to be checked in, clean the workspace:

	.\automation\cdEmulate.bat clean

Once finished with the environment, destroy using:

    vagrant destroy -f

{% include links.html %}
