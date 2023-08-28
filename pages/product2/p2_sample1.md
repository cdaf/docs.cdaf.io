---
title: Install Vagrant
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_sample1.html
---

## Sample Content

Vagrant and Oracle VirtualBox or Microsoft Hyper-V

## VirtualBox

Oracle VirtualBox and Vagrant

Note: on Windows Server 2012 R2 need to manually install x86 (not 64 bit) C++ Redistributable.

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
    
# Vagrant Boxes

Vagrant box images available here https://app.vagrantup.com/cdaf are build initially for Hyper-V using AtlasBase.ps1. This is cloned in VirtualBox and then both images are prepared using AtlasImage.ps1. Finally the images are packaged on the Hyper-V and VirtualBox hosts using AtlasPackage.ps1. The resulting .box files are uploaded to Vagrantup.

## Related Material

The following links have contributed to the construction of the Atlas scripts

 * https://www.vagrantup.com/docs/virtualbox/boxes.html
 * http://www.hurryupandwait.io/blog/in-search-of-a-light-weight-windows-vagrant-box
 * http://huestones.co.uk/node/305
 * https://stackoverflow.com/questions/39469452/installing-removed-windows-features/46985832#46985832

{% include links.html %}
