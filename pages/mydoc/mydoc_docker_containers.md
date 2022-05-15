---
title: Docker Containers
tags: [containers]
keywords: containers, tasks
last_updated: July 3, 2016
summary: CDAF Image and Container Helpers, intended for self-hosted agents.
sidebar: mydoc_sidebar
permalink: mydoc_docker_containers.html
folder: mydoc
---

Some CI/CD pipeline toolsets support native capability (GitLab, BitBucket) to execute with a container. In other some cases, (CircleCI, Travis) all pipeline activity can only be executed within containers.

For toolsets which do not support this functionality, but do allow for self-hosted agents or where a self-hosted agent is preferred/mandated i.e. execution within a private network, the CDAF container helpers can provide consistency for construction, execution and housekeeping.

Even with a toolset uses containers, if they support docker-in-docker, the CDAF container helpers can still be utilised.

{% include links.html %}
