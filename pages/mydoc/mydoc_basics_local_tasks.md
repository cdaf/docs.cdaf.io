---
title: Local Tasks
tags: [getting_started, tasks]
keywords: agent, runner, server
last_updated: Mar 4, 2022
summary: Tasks run in a local context.
sidebar: mydoc_sidebar
permalink: mydoc_basics_local_tasks.html
folder: mydoc
simple_map: true
map_name: usermap
box_number: 4
folder: mydoc
---

Local Tasks use the same execution engined as [build tasks][mydoc_basics_build_tasks], but at deploy time, rather than build time. Local Tasks are executed in the local context of the host/server. Local Tasks are suited to situations where the agent is installed on the server where tasks are to be performed, or the server that the agent/runner is installed has the tools required to perform tasks on a remote target, i.e. a service offering with a command line interface, such as Kubernetes, Azure or AWS.

> The CDAF capabilities with [containers][mydoc_docker_containers] cater for more sophisticated uses in the local context and the alternative [container tasks][mydoc_container_tasks] execution approach.

## Example Task

The default tasks that are run in the local context are `tasksRun.tsk` and `tasksRunLocal.tsk`. These are placed in your solution root.


### Linux

``` bash
echo 'DETOKN ./output/runtime.sh' > .cdaf/tasksRunLocal.tsk
echo '' >> .cdaf/tasksRunLocal.tsk
echo './output/runtime.sh' >> .cdaf/tasksRunLocal.tsk
```

### Windows

``` powershell
Set-Content .\.cdaf\tasksRunLocal.tsk 'DETOKN .\output\runtime.ps1'
Add-Content .\.cdaf\tasksRunLocal.tsk ''
Add-Content .\.cdaf\tasksRunLocal.tsk '.\output\runtime.ps1'
```

## Continuous Delivery Emulation (CD)

Execute the CD emulation

    cdEmulate.sh

or for windows

    cdEmulate

Two steps are performed, first the deployable artefact is detokenised

```
Found %property%, replacing with Local Context
Found %integer%, replacing with 1
```

Then executed to verify the environment specific properties.

```
Deploy 1, property set to : Local Context
```

This now completes an end-to-end example of CDAF, from configuration management, build & package through to deployment. Following are some common additional configuration elements, and the final step covers the increasingly less common pattern of [Remote tasks][mydoc_basics_remote_tasks].

## Alternate Tasks

If you require a variety of tasks, you can explicitly define them, which will ignore any tasksRun.tsk and tasksRunLocal.tsk in your solution root. Please your task files in directorie named either ``custom`` or ``customLocal`` in your solution root.

To map your configuration to the alternate tasks, you must use the column name ``deployTaskOverride``.

```
context  target  deployTaskOverride     databaseFQDN        dBpassword
local    TEST    simple-db-deploy.tsk   db1.nonprod.local   $db1Pass
local    UAT     simple-db-deploy.tsk   $db2Pass
local    PROD    cluster-db-deploy.tsk  $prodPass
```

> Next: [Remote tasks][mydoc_basics_remote_tasks]

{% include links.html %}
