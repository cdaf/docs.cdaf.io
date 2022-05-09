---
title: Remote Tasks
tags: [getting_started, tasks]
keywords: agent, runner, server
last_updated: Mar 5, 2022
summary: Tasks run in a remote context. This approach is less common with the license barriers to installing deployment agents, and the client oriented nature of modern agents, making the need for push deployments less common.
sidebar: mydoc_sidebar
permalink: mydoc_basics_remote_tasks.html
folder: mydoc
simple_map: true
map_name: usermap
box_number: 5
folder: mydoc
---

Like Local Tasks, Remote Tasks use the same execution engined as [build tasks][mydoc_basics_build_tasks], but at deploy time, rather than build time. Remote Tasks are executed in the local context of a *remote* host/server. Remote Tasks are suited to situations where the agent is *not* installed on the server where tasks are to be performed and instead the deployment is pushed, i.e. to an application server in the DMZ which can only be accessed by Remote PowerShell or SSH.

The Remote Task is executed in a local context, so all the processes described in [Local Tasks][mydoc_basics_local_tasks], however, how the deployment package is made available to the execution engine differs, along with pre-execution steps to make execution on the remote host possible.

## SSH/SCP or Remote PowerShell with custom file transfer

Remote PowerShell for Windows or SSH/SCP for Linux are the protocols used to tranfer the Remote Task package to the remote host for execution. PowerShell does not have an file transort protocol (Windows is typically reliant on SMB) so a CDAF feature has be provided to allow a file transfer mechanism similar to SCP in Linux.

## Nested Package

When using Remote Tasks, a reduced set of CDAF helper scripts are packed into a nested compressed file. This file is transferred to the remote host and then unpacked. Once unpacked, the properties for the current release environment are transferred to remote host, and then the deployment is executed.

## Remote Task Configuration

The default authentication for transferring the remote files is pre-shared keys for Linux and domain service principke for Windows, however, alternative authentication methods are supported.

```
context  target     deployHost   remoteUser
remote   VAGRANT    linux.local  adminuser
```

### Windows PowerShell Authentication Options

The simplest authentication option is to use username and password, do not store the password in source control, instead use a variable.

> Environment variables are the recommended approach because this allows execution on a desktop or in a pipeline.

```
context  target     deployHost          remoteUser           remotePass
remote   VAGRANT    windows.mshome.net  windows-1\adminuser  $env:CDAF_PS_USERPASS
```

> Next: [Execution Engine][mydoc_execution_engine]

{% include links.html %}
