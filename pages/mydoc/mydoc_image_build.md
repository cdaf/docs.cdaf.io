---
title: imageBuild
tags: [containers, tasks]
keywords: containers, tasks, oci
last_updated: May 15, 2022
summary: Build one or Docker images from either a named directory or the current working directory 
sidebar: mydoc_sidebar
permalink: mydoc_image_build.html
folder: mydoc
---

This helper script supports the creation of docker images, and conditionally, the pushing of that image to a registry.

# Container Build Configuration

To execute, define the containerBuild definition and runtimeImage (if not supplied, containerImage will be used) to **CDAF.solution**. Note: complete definitions are provided in the GitHub samples for [Windows](https://github.com/cdaf/windows/tree/master/samples/imageBuild) and [Linux](https://github.com/cdaf/linux/tree/master/samples/imageBuild).

## Windows

    constructor=TasksLocal
    imageBuild=& $AUTOMATIONROOT/remote/imageBuild.ps1 ${SOLUTION}_${REVISION} ${BUILDNUMBER} $runtimeImage $constructor
    runtimeImage=mcr.microsoft.com/windows/servercore/iis

## Linux

    constructor=TasksLocal
    imageBuild=$AUTOMATIONROOT/remote/imageBuild.sh ${SOLUTION}_${REVISION} ${BUILDNUMBER} $runtimeImage $constructor
    runtimeImage=nginx

If the constructor is not supplied, a image will be built for each directory in the current working directory.

# Registry Push

To include a push to a registry, add the following to **CDAF.solution** for DockerHub

    CDAF_REGISTRY_URL=DOCKER-HUB
    CDAF_REGISTRY_TAG=repo/${SOLUTION}:$BUILDNUMBER
    CDAF_REGISTRY_USER=pat
    CDAF_REGISTRY_TOKEN=${ACCESS_TOKEN}

Or for another registry provider or a self-hosted registry

    CDAF_REGISTRY_URL=myregistry.io/repo
    CDAF_REGISTRY_TAG=${CDAF_REGISTRY_URL}/${SOLUTION}:$BUILDNUMBER
    CDAF_REGISTRY_USER=pat
    CDAF_REGISTRY_TOKEN=${ACCESS_TOKEN}

> See GitHub samples for [Windows](https://github.com/cdaf/windows/tree/master/samples/imageBuild) and [Linux](https://github.com/cdaf/linux/tree/master/samples/imageBuild) dockerfile and additional properties.

{% include links.html %}
