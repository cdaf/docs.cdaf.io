---
title: Local Tasks
tags: [getting_started, tasks]
keywords: agent, runner, server
last_updated: Mar 4, 2022
summary: "Tasks run in a local context."
sidebar: mydoc_sidebar
permalink: mydoc_basics_local_tasks.html
folder: mydoc
---

Local Tasks use the same execution engined as [build tasks][mydoc_basics_build_tasks], but at deploy time, rather than build time. Local Tasks are executed in the local context of the host/server. Local Tasks are suited to situations where the agent is installed on the server where tasks are to be performed, or the server that the agent is installed has the tools required to perform tasks on a remote target, i.e. a service offering with a command line interface, such as Kubernettes, Azure or AWS.

> The CDAF capabilities with [containers][mydoc_docker_containers] cater for more sophisticated uses in the local context and the alternative [container tasks][mydoc_container_tasks] execution approach.

The local task context one of the most important features for repeatable release deployment is the ability to detokenise files. Tokenised configuration files reduce the risk of structural drift of settings files in source control, while making the release targets scalable, i.e. making it easier to add another test or user acceptance environment.

The environment which is passed to the relase package is the default file name to be used for detokenisation.

``` powershell
Write-Host "Detokenise the settings for this environment`n"
DETOKN aspdotnet.SetParameters.xml

Write-Host "Use Web Deploy to deploy the Aware application`n"
.\aspdotnet.deploy.cmd /Y /M:localhost
```

{% include links.html %}
