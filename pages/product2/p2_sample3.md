---
title: Docker on Windows
keywords: sample
summary: Virtualised and Native Docker Execution on Wiondows
sidebar: product2_sidebar
permalink: p2_sample3.html
---

# docker-desktop

Typically Combined with Windows Subsystem for Linux (WSL) for working with Linux containers, not required for Windows containers.

```
Dism /online /enable-feature /all /featurename:Microsoft-Hyper-V /NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName Containers -All -NoRestart
. { iwr -useb https://raw.githubusercontent.com/cdaf/windows/master/install.ps1 } | iex
./automation/provisioning/base.ps1 'docker-desktop wsl2' -autoReboot yes
curl.exe -L https://aka.ms/wsl2kernel -o wsl_update_x64.msi
.\automation\provisioning\installMSI.ps1 wsl_update_x64.msi
shutdown /r /t 0
```

# Native Windows Containers

Native Windows Containers can only run the same version as the host operating system, e.g. Windows Server 2019 Container cannot be run on Windows Server 2022 host, or vice versa.

```
. { iwr -useb https://raw.githubusercontent.com/cdaf/windows/master/install.ps1 } | iex
./automation/provisioning/installDocker.ps1
```

# CDAF Image for Windows Server 2022

Get latest image

    docker pull cdaf/windows

Verify image capabilities

    docker run cdaf/windows powershell capabilities

Execute Emulation

    docker run --volume "$(pwd)\:C:/solution/workspace" cdaf/windows

Interactive Terminal (-it) in container

    docker run -it --volume "$(pwd)\:C:/solution/workspace" cdaf/windows powershell

Agent in Default Pool with hostname as agent name

    docker run -d cdaf/windows powershell C:\\solution\\register-and-run.ps1 $ORG_URL $POOL_TOKEN

Agent in named Pool with agent name (useful to recycle the container and replace the existing agent)

    docker run -d cdaf/windows powershell C:\\solution\\register-and-run.ps1 $ORG_URL $POOL_TOKEN pool-name windows-agent

Deployment Group

    docker run -d cdaf/windows powershell C:\\solution\\register-and-run.ps1 $ORG_URL $GROUP_TOKEN project@deployment-group windows-target-1

# CDAF Image for Windows Server 2019

> note: the tools installed are designed to align with Azure DevOps agent capabilities

Get latest image

    docker pull cdaf/windows-ado-agent

Verify image capabilities

    docker run cdaf/windows-ado-agent powershell capabilities

Emulate CDAF build in your workspace

    docker run --volume "$(pwd)\:C:/solution/workspace" cdaf/windows-ado-agent

Interactive Terminal (-it) in container

    docker run -it --volume "$(pwd)\:C:/solution/workspace" cdaf/windows-ado-agent powershell

Agent in Default Pool with hostname as agent name

    docker run -d cdaf/windows-ado-agent powershell C:\\solution\\register-and-run.ps1 $ORG_URL $POOL_TOKEN

Agent in named Pool with agent name (useful to recycle the container and replace the existing agent)

    docker run -d cdaf/windows-ado-agent powershell C:\\solution\\register-and-run.ps1 $ORG_URL $POOL_TOKEN pool-name windows-agent

Deployment Group

    docker run -d cdaf/windows-ado-agent powershell C:\\solution\\register-and-run.ps1 $ORG_URL $GROUP_TOKEN project@deployment-group windows-target-1

{% include links.html %}
