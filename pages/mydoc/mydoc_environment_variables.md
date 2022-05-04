---
title: Environment Variables
tags: [feature_config]
keywords: controls
last_updated: May 4, 2022
summary: CDAF Control Variables.
sidebar: mydoc_sidebar
permalink: mydoc_environment_variables.html
folder: mydoc
---

## Control Variables

The following environment 

| Variable                  | Description
|---------------------------|------------
| CDAF_BRANCH_NAME          | Used by entry.ps1/entry.sh <br/>Override the branch name, primarily to test CI behaviour for non-default branch, i.e. main
| CDAF_DOCKER_REQUIRED      | [containerBuild][mydoc_container_build] will attempt to start Docker if not running and will fail if it cannot, rather than falling back to native execution
| CDAF_DELIVERY             | The default target environment for cdEmulate.sh, defaults are <br/>LINUX, or<br/> WINDOWS for on-domain or WORKGROUP for off-domain
| CDAF_ERROR_DIAG           | Dependency injected custom call if error occurs in [Execution Engine][mydoc_execution_engine]
| CDAF_IGNORE_WARNING       | If messages are logged to standard error, the [Execution Engine][mydoc_execution_engine] will log but not halt, however is this is set to yes, processing will halt <br/>yes or no, default is yes
| CDAF_OVERRIDE_TOKEN       | Default marker for DETOKN or PROPLD in [Execution Engine][mydoc_execution_engine] is %, i.e. %key_name%, the markers can be changed using this environment variable
| CDAF_SKIP_CONTAINER_BUILD | [containerBuild][mydoc_container_build] will not be performed if this environment variable is set to any value

> Next: [Sensistive Data Strategies][mydoc_sensitive_data_strategies]

{% include links.html %}
