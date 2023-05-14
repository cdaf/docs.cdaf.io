---
title: Solution Properties
tags: [feature_configuration]
keywords: solutionName, productName, artifactPrefix, productVersion, containerBuild, containerImage, imageBuild, runtimeImage, constructor, defaultBranch, CDAF_HOME_MOUNT, CDAF_REGISTRY_URL, CDAF_REGISTRY_TAG, CDAF_REGISTRY_USER, CDAF_REGISTRY_TOKEN, gitRemoteURL, gitUserNameEnvVar, gitUserPassEnvVar, gitCustomCleanup
last_updated: May 4, 2022
summary: CDAF Configuration Properties.
sidebar: mydoc_sidebar
permalink: mydoc_solution_properties.html
folder: mydoc
---

## Solution Property File

CDAF.solution : file to identify a directory as the automation solution directory where the key configuration files are placed. This file is used as the bases of the manifest.txt file while is included in the resulting CI artefact package.

See solution/CDAF.solution in CDAF automation directory.

## Solution Properties

| Variable                  | Description
|---------------------------|------------
| solutionName              | Required. Do not include spaces.
| productName               | Solution description, this can contain spaces.
| artifactPrefix            | Generate a self-extracting package script, example 0.0, mutually exclusive to productVersion
| productVersion            | Do a self-extracting package script, example 0.0.0
| containerBuild            | Dependency injection for running container based build execution
| containerImage            | Image to be used in the container based build execution
| containerDeploy           | Execute deployment from within a container, uses the storeForRemote artefact definition
| imageBuild                | Dependency injection for creating a container image after CI process, see the Image Registry properties below
| runtimeImage              | Image to used in the runtime image created by imageBuild
| constructor               | Directory in which container images are constructed, default action will traverse and build in all directories
| defaultBranch             | Used to determine feature branch functionality, default is master
| defaultEnvironment        | Default environment to use for [CDAF Feature Branch Environments post](https://blog.cdaf.io/posts/2022-02-20-feature-branch-environments/), defaults to DOCKER
| processSequence           | Deployment Process Sequence, defaults to localTasks, remoteTasks and finally containerTasks

## Environment Variable Substitution

The following properties can be used in place of environment variables 

| Variable                  | Description
|---------------------------|------------
| CDAF_HOME_MOUNT           | to disable volume mount for containerDeploy set to 'no'
| CDAF_ERROR_DIAG           | Dependency injected custom call if error occurs in [Execution Engine][mydoc_execution_engine]

### Image Registry

These properties are used to push the image created by imageBuild.

| Variable                  | Description
|---------------------------|------------
| CDAF_REGISTRY_URL         | Image registry URL, example myregistry.local
| CDAF_REGISTRY_TAG         | Image tab, example myregistry.local/group/mysolution:111
| CDAF_REGISTRY_USER        | Registry user, example registryuser
| CDAF_REGISTRY_TOKEN       | Registry token, example xyzx9234sxsrwcqw34

### Git Clean-up Properties

To clean-up Git branches and docker images, the following properties are used.

| Variable                  | Description
|---------------------------|------------
| gitRemoteURL              | https://gitserver.local/mysolution.git
| gitUserNameEnvVar         | gituser
| gitUserPassEnvVar         | secret-pat
| gitCustomCleanup          | & $AUTOMATIONROOT/buildandpackage/clean.ps1 or $AUTOMATIONROOT/buildandpackage/clean.sh

> Next: [Sensitive Data Strategies][mydoc_sensitive_data_strategies]

{% include links.html %}
