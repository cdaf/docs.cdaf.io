---
title: containerDeploy
tags: [containers, tasks]
keywords: containers, tasks, runtimeFiles
last_updated: May 15, 2022
summary: Perform a Deployment Task from within a Container
sidebar: mydoc_sidebar
permalink: mydoc_container_deploy.html
folder: mydoc
---

Like [containerBuild][mydoc_container_build], containerDeploy provides both image build and container task execution. The common use for container deploy where a command line interface is required.

# Master of Deployment Success

The containerDeploy option allows the execution of the deploy process from within a container. Unlike toolsets which reference a image that is used to create the deploy container, CDAF uses a Dockerfile, for the following advantages:

- Deploy Prerequisites can be defined in code, without being limited to available published images
- Once constructed the image image cache provides improved performance, without having to use a image registry

# Container Deploy Configuration

To execute the deploy within a container, add the containerDeploy definition and runtimeImage (if not supplied, containerImage will be used) to **CDAF.solution**. Note: complete definitions are provided in the GitHub samples for [Windows](hhttps://github.com/cdaf/windows/tree/master/samples/containerDeploy) and [Linux](https://github.com/cdaf/linux/tree/master/samples/containerDeploy).

> The following samples have the default process commented out, and can be used to define a custom process.

## Windows

    runtimeImage=cdaf/windows
    # containerDeploy=& ${WORK_DIR_DEFAULT}/containerDeploy.ps1 "${TARGET}" "${RELEASE}" "${SOLUTION}" "${BUILDNUMBER}" "${REVISION}" -imageDir cli

## Linux

    containerImage=cdaf/linux
    # containerDeploy=${WORK_DIR_DEFAULT}/containerDeploy.sh "${TARGET}" "${RELEASE}" "${SOLUTION}" "${BUILDNUMBER}" "${REVISION}" cli

## Deploy Time Variables

To supply variables to the build process, prefix with *CDAF_CD_* (see [CDAF Environment Variables][mydoc_environment_variables]) and the variables will be mapped into the build container.

> See GitHub samples for [Windows](https://github.com/cdaf/windows/tree/master/samples/containerDeploy) and [Linux](https://github.com/cdaf/linux/tree/master/samples/containerDeploy) for dockerfile and additional properties.

# Custom Image

The default directory used for container deploy is _containerDeploy_, if this is not found, the default `Dockerfile` is used, with the default runtime files. If you have your own `Dockerfile` in _containerDeploy_, or a custom directory specified in `CDAF.solution` _containerDeploy_ property, then that will be used.

# Runtime Files

The release.sh file is included in the default image, however, if using a default image, this needs to be explicitly defined in `CDAF.solution` _runtimeFiles_ property. This can be a space separated list of files.

    runtimeFiles=$WORKSPACE_ROOT/release.sh

# Runtime Retain

To skip image clean-up, set `CDAF.solution` _runtimeRetain_ property.

    runtimeRetain=yes

{% include links.html %}
