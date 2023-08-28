---
title: dockerPush
tags: [containers]
keywords: containers, CDAF_PUSH_REGISTRY_URL, CDAF_PUSH_REGISTRY_TAG, CDAF_PUSH_REGISTRY_USER, CDAF_PUSH_REGISTRY_TOKEN
last_updated: Aug 28, 2023
summary: Docker Image Push Utility
sidebar: mydoc_sidebar
permalink: mydoc_docker_push.html
folder: mydoc
---

Using the same logic after [imageBuild][mydoc_image_build], this utility script provides simple login and push logic.

The script can be called passing arguments

```
./dockerPush.ps1 $TARGET_TAG cdaf/${SOLUTION} "${artifactPrefix}.${BUILDNUMBER} latest" $DOCKERHUB_TOKEN cdaf
```

This example uses an environment variable (complete list follows) to set the URL. The registry in this example does not require authentication.

```
export CDAF_PUSH_REGISTRY_URL=hub.private.registry
./dockerPush.sh ${SOLUTION}_master_target:${BUILDNUMBER} ${SOLUTION} ${BUILDNUMBER}
```

Available environment variables

| Variable                  | Description
|---------------------------|------------
| CDAF_PUSH_REGISTRY_URL    | Image registry URL, example myregistry.local (do not set for dockerhub)
| CDAF_PUSH_REGISTRY_TAG    | Image tag(s), can being single value `latest` or list `latest ${BUILDNUMBER}` (default is `latest`)
| CDAF_PUSH_REGISTRY_USER   | Registry user, example registryuser (if not set, default is '.')
| CDAF_PUSH_REGISTRY_TOKEN  | Registry token, example xyzx9234sxsrwcqw34

{% include links.html %}
