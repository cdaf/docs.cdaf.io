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

Local Tasks use the same execution engined as [build tasks][mydoc_basics_build_tasks], but at deploy time, rather than build time. Local Tasks are executed in the local context of the host/server. Local Tasks are suited to situations where the agent is installed on the server where tasks are to be performed, or the server that the agent is installed has the tools required to perform tasks on a remote target, i.e. a service offering with a command line interface, such as Kubernettes, Azure or AWS.

> The CDAF capabilities with [containers][mydoc_docker_containers] cater for more sophisticated uses in the local context and the alternative [container tasks][mydoc_container_tasks] execution approach.

## Example Task

The default tasks that are run in the local context are tasksRun.tsk and tasksRunLocal.tsk. There are placed in your solution root.

``` powershell
Write-Host "Detokenise the settings for this environment`n"
DETOKN aspdotnet.SetParameters.xml

Write-Host "Use Web Deploy to deploy the Aware application`n"
.\aspdotnet.deploy.cmd /Y /M:localhost
```

## DETOKN : Detokenise File

The local task context one of the most important features for repeatable release deployment is the ability to detokenise files. Tokenised configuration files reduce the risk of structural drift of settings files in source control, while making the release targets scalable, i.e. making it easier to add another test or user acceptance environment.

The environment which is passed to the relase package is used to match to the ``target`` defined in [configuration management][mydoc_configuration_management] for detokenisation. The properties file before the DETOKN operation

``` xml
<?xml version="1.0" encoding="utf-8"?>
<parameters>
  <setParameter name="IIS Web Application Name" value="Default Web Site/wol" />
  <setParameter name="aspdotnetEntities.config Connection String" value="metadata=res://*/Models.aspdotnet.csdl|res://*/Models.aspdotnet.ssdl|res://*/Models.aspdotnet.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=%databaseFQDN%;initial catalog=aspdotnetapp;integrated security=True;multipleactiveresultsets=True;application name=EntityFramework&quot;" />
</parameters>
```

For this properties.cm example

```
context  target  databaseFQDN        dBpassword
local    TEST    db1.nonprod.local   $db1Pass
local    UAT     db2.nonprod.local   $db2Pass
local    PROD    cluster.prod.local  $prodPass
```

If the release is deployed to test, i.e. ``./release.ps1 TEST``, the resulting properties file will have ``source=%databaseFQDN%`` replaced by ``source=db1.nonprod.local``. 

``` xml
<?xml version="1.0" encoding="utf-8"?>
<parameters>
  <setParameter name="IIS Web Application Name" value="Default Web Site/wol" />
  <setParameter name="aspdotnetEntities.config Connection String" value="metadata=res://*/Models.aspdotnet.csdl|res://*/Models.aspdotnet.ssdl|res://*/Models.aspdotnet.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=db1.nonprod.local;initial catalog=aspdotnetapp;integrated security=True;multipleactiveresultsets=True;application name=EntityFramework&quot;" />
</parameters>
```

## Alternate Tasks

If you require a variety of tasks, you can explicitely define them, which will ignore any tasksRun.tsk and tasksRunLocal.tsk in your solution root. Please your task files in directorie named either ``custom`` or ``customLocal`` in your solution root.

To map your configuration to the alternate tasks, you must use the column name ``deployTaskOverride``.

```
context  target  deployTaskOverride     databaseFQDN        dBpassword
local    TEST    simple-db-deploy.tsk   db1.nonprod.local   $db1Pass
local    UAT     simple-db-deploy.tsk   $db2Pass
local    PROD    cluster-db-deploy.tsk  $prodPass
```

> Next: [Remote tasks][mydoc_basics_remote_tasks]

{% include links.html %}
