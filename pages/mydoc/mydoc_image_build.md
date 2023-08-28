---
title: imageBuild
tags: [containers, tasks]
keywords: containers, tasks, oci, CDAF_REGISTRY_URL, CDAF_REGISTRY_TAG, CDAF_REGISTRY_USER, CDAF_REGISTRY_TOKEN
last_updated: May 15, 2022
summary: Build one or Docker images from either a named directory or the current working directory 
sidebar: mydoc_sidebar
permalink: mydoc_image_build.html
folder: mydoc
---

This helper script supports the creation of docker images, and conditionally, the pushing of that image to a registry.

# Container Build Configuration

To execute, define the buildImage definition. Note: complete definitions are provided in the GitHub samples for [Windows](https://github.com/cdaf/windows/tree/master/samples/imageBuild) and [Linux](https://github.com/cdaf/linux/tree/master/samples/imageBuild).

> The following samples have the default process commented out, and can be used to define a custom process.

## Windows

    buildImage=cdaf/windows
    # imageBuild=& "$AUTOMATIONROOT/remote/imageBuild.ps1" ${SOLUTION}_${REVISION} ${BUILDNUMBER}

## Linux

    buildImage=cdaf/linux
    # imageBuild="$AUTOMATIONROOT/remote/imageBuild.sh" ${SOLUTION}_${REVISION} ${BUILDNUMBER}

## Immutable Deploy in Construction

If a custom docker file is not supplied, the default dockerfile will execute the IMMUTABLE release in the image construction process.

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

# Custom Image & Process

For samples of more complex usage see the GitHub samples for [Windows](https://github.com/cdaf/windows/tree/master/samples/imageBuild-custom-image) and [Linux](https://github.com/cdaf/linux/tree/master/samples/imageBuild-custom-image) dockerfile and additional properties.

{% include links.html %}
