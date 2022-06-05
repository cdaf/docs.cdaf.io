---
title: containerBuild
tags: [containers, tasks]
keywords: containers, tasks
last_updated: May 15, 2022
summary: Perform a Build Task from within a Container
sidebar: mydoc_sidebar
permalink: mydoc_container_build.html
folder: mydoc
---

# Master of Build Success

The containerBuild option allows the execution of the build process from within a container. Unlike toolsets which reference a image that is used to create the build container, CDAF uses a Dockerfile, for the following advantages:

- Build Prerequisites can be defined in code, without being limited to available published images
- Once constructed the image image cache provides improved performance, without having to use a image registry
- Working directory and user home directory are volume mounted, to allow caching of build dependencies, e.g. Maven, node_modules

# Container Build Configuration

To execute the build within a container, add the containerBuild definition and containerImage to **CDAF.solution**. Note: complete definitions are provided in the GitHub samples for [Windows](https://github.com/cdaf/windows/tree/master/samples/containerBuild) and [Linux](https://github.com/cdaf/linux/tree/master/samples/containerBuild).

## Windows

    containerBuild=& ${AUTOMATIONROOT}/processor/containerBuild.ps1 $SOLUTION $BUILDNUMBER $REVISION $ACTION
    containerImage=mcr.microsoft.com/windows/server:ltsc2022

## Linux

    containerBuild=$AUTOMATIONROOT/processor/containerBuild.sh $SOLUTION $BUILDNUMBER $REVISION $ACTION
    containerImage=ubuntu:20.04

## Build Time Variables

To supply variables to the build process, prefix with *CDAF_CB_* (see [CDAF Environment Variables][mydoc_environment_variables]) and the variables will be mapped into the build container.

> See GitHub samples for [Windows](https://github.com/cdaf/windows/tree/master/samples/containerBuild) and [Linux](https://github.com/cdaf/linux/tree/master/samples/containerBuild) for dockerfile and additional properties.

{% include links.html %}
