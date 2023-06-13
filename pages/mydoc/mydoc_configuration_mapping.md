---
title: Configuration Mapping
tags: [feature_configuration]
keywords: deployTaskOverride
last_updated: May 5, 2022
summary: Configuration Mapping to Execution Engine.
sidebar: mydoc_sidebar
permalink: mydoc_configuration_mapping.html
---

## Configuration Mapping to Execution Engine

The [local][mydoc_basics_local_tasks] and [remote][mydoc_basics_remote_tasks] configuration will trigger a task execution based on each unique declaration of context and target, using the corresponding default task `tasksRunLocal.tsk` and `tasksRunLocal.tsk`.

```
context  target  deployHost
remote   UAT     vm.example.com
local    UAT     vm.example.com
remote   PROD    vm.example.com
local    PROD    vm.example.com
```

Customer tasks can be defined for directories `customLocal` and `customRemote` respectively, or `custom` if shared.

```
context    target  deployTaskOverride
local      DOCKER  docker-compose-test.tsk
remote     UAT     on-premise-deploy.tsk
remote     PROD    on-premise-deploy.tsk
container  PUSH    publish-production-ertefact.tsk
```

Note that `container` override tasks are made available in the `customRemote` directory.

> Next: [Execution Engine][mydoc_execution_engine]

{% include links.html %}
