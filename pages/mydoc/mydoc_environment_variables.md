---
title: Environment Variables
tags: [feature_configuration]
keywords: CDAF_BRANCH_NAME, CDAF_DOCKER_REQUIRED, CDAF_DELIVERY, CDAF_ERROR_DIAG, CDAF_HOME_MOUNT, CDAF_IGNORE_WARNING, CDAF_OVERRIDE_TOKEN, CDAF_SKIP_CONTAINER_BUILD, CONTAINER_IMAGE, CDAF_CB_, CDAF_CD_
last_updated: May 4, 2022
summary: CDAF Control Variables.
sidebar: mydoc_sidebar
permalink: mydoc_environment_variables.html
folder: mydoc
---

## Control Variables

The following environment variables are available

| Variable                  | Description
|---------------------------|------------
| CDAF_BRANCH_NAME          | Used by entry.ps1/entry.sh <br/>Override the branch name, primarily to test CI behaviour for non-default branch, i.e. main
| CDAF_CORE                 | CDAF helper script path
| CDAF_DOCKER_REQUIRED      | [containerBuild][mydoc_container_build] will attempt to start Docker if not running and will fail if it cannot, rather than falling back to native execution
| CDAF_DELIVERY             | The default target environment for cdEmulate.sh, defaults are <br/>LINUX, or<br/> WINDOWS for on-domain or WORKGROUP for off-domain
| CDAF_ERROR_DIAG           | Dependency injected custom call if error occurs in [Execution Engine][mydoc_execution_engine]
| CDAF_HOME_MOUNT           | to disable volume mount for containerDeploy set to 'no', note: this can be overridden a solution level, using CDAF_HOME_MOUNT as property
| CDAF_IGNORE_WARNING       | If messages are logged to standard error, the [Execution Engine][mydoc_execution_engine] will log but not halt, however is this is set to yes, processing will halt <br/>yes or no, default is yes
| CDAF_OVERRIDE_TOKEN       | Default marker for DETOKN or PROPLD in [Execution Engine][mydoc_execution_engine] is %, i.e. %key_name%, the markers can be changed using this environment variable
| CDAF_SKIP_CONTAINER_BUILD | [containerBuild][mydoc_container_build] will not be performed if this environment variable is set to any value
| CONTAINER_IMAGE           | Override containerImage in [containerBuild][mydoc_container_build] & [imageBuild][mydoc_image_build]
| CDAF_CB_{variable_name}   | Prefix used in [containerBuild][mydoc_container_build] to supply local variables into the build time container
| CDAF_CD_{variable_name}   | Prefix used in [containerDeploy][mydoc_container_deploy] to supply local variables into the deploy time container
| CDAF_IB_{variable_name}   | Prefix used in [containerBuild][mydoc_image_build] to supply during image construction

## Image Registry

These override [Solution Properties][mydoc_solution_properties] properties. They are used to push the image created by dockerBuild to pull a base image from a private registry.

| Variable                  | Description
|---------------------------|------------
| CDAF_SKIP_PULL            | Skip updating of image
| CDAF_PULL_REGISTRY_URL    | Image registry URL, example myregistry.local (do not set for dockerhub)
| CDAF_PULL_REGISTRY_USER   | Registry user, example registryuser (if not set, default is '.')
| CDAF_PULL_REGISTRY_TOKEN  | Registry token, example xyzx9234sxsrwcqw34

These override [Solution Properties][mydoc_solution_properties] properties. They are used to push the image created by imageBuild to push to a private registry.

| Variable                  | Description
|---------------------------|------------
| CDAF_REGISTRY_URL         | Image registry URL, example myregistry.local (do not set for dockerhub)
| CDAF_REGISTRY_TAG         | Image tag(s), can being single value `latest` or list `latest ${BUILDNUMBER}`
| CDAF_REGISTRY_USER        | Registry user, example registryuser (if not set, default is '.')
| CDAF_REGISTRY_TOKEN       | Registry token, example xyzx9234sxsrwcqw34

These override [Solution Properties][mydoc_solution_properties] properties. They are used to push the image created by dockerPush to push to a private registry.

| Variable                  | Description
|---------------------------|------------
| CDAF_PUSH_REGISTRY_URL    | Image registry URL, example myregistry.local (do not set for dockerhub)
| CDAF_PUSH_REGISTRY_TAG    | Image tag(s), can being single value `latest` or list `latest ${BUILDNUMBER}` (default is `latest`)
| CDAF_PUSH_REGISTRY_USER   | Registry user, example registryuser (if not set, default is '.')
| CDAF_PUSH_REGISTRY_TOKEN  | Registry token, example xyzx9234sxsrwcqw34

> Next: [Sensitive Data Strategies][mydoc_sensitive_data_strategies]

{% include links.html %}
